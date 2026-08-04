# Race condition: `OnWSReceive` intermittently fails with `VALUE ERROR: Undefined name: id`

This describes a real, reproducible (if intermittent) crash in `#.Abacus.Main`, explains why it happens, and gives a small, correct fix.

## TL;DR

`OnWSReceive` builds `e←Elements d` (every element in the APLDOM) and then evaluates the distributed
reference `e.id`. If any element in `e` has no `id`, that reference throws
`VALUE ERROR: Undefined name: id` and the incoming event is lost.

The offenders are DataGrid table cells (`thead`/`tr`/`th`/`tbody`/`td`). They do get ids — but
`DataGrid.BuildStructure` creates them first and stamps the ids a few lines later, so there is a brief
window in which they are in the tree without ids. 

Because events are dispatched on more than one
thread, an incoming event can land in `OnWSReceive` during that window, walk the un-id'd cells, and
crash. That is the "fails every now and then for no apparent reason".

**Fix:** in `OnWSReceive`, restrict the lookup to id-bearing elements. An element with no `id` can never
be an event target anyway, so excluding it is both robust and correct.

## Symptom

Intermittent, on an ordinary interaction (a click, a resize) with no special cause. Stack:

```
VALUE ERROR: Undefined name: id
OnWSReceive[8]  i←e.id⍳c.CurrentTargetId c.TargetId
                     ∧
```

Seen in an application (Fire) built on Abacus — e.g. on a clean start, pressing "Find" (which populates
a DataGrid). The event that crashes is not the culprit; a lingering/transient un-id'd element is.

## Root cause

Two pieces of `#.Abacus.Main` combine:

1. `OnWSReceive` requires every element to have an `id`.

   ```
    OnWSReceive←{
        …
        e←Elements d
        i←e.id⍳c.CurrentTargetId c.TargetId     ⍝ ← e.id is distributed; one id-less element ⇒ VALUE ERROR
        c.(CurrentTarget Target)←(e,0)[i]
        …
    }
    ```


    `Elements` recurses the whole `Content` tree, so `e` includes the DataGrid's cell elements.

2. `DataGrid.BuildStructure` inserts cells before it stamps their ids.
 
   ```
    BuildStructure←{
        t←⍵
        …
        t.Content←{⍵.Content}A.NewTable(r c⍴⊂'')(t.HeaderRowCount c⍴⊂'')   ⍝ [1] cells now in the tree…
        …
        e←A.Elements t
        e.Document←d
        e.class←⊂''
        _←d A.SetDefaultId e                                              ⍝ [2] …ids assigned only here
        …
    }
   ```

   Between `[1]` and `[2]` the cells exist in the APLDOM without an `id`.

3. Threading makes the window observable

   Abacus dispatches events across threads (the worker `ThreadQueue` thread and the `⎕DQ`/HTMLRenderer callback thread). A grid (re)render running `BuildStructure` on one thread can overlap an incoming event running `OnWSReceive` on another. 

   When `OnWSReceive` evaluates `e.id` while a grid is mid-`BuildStructure`, `e` contains the not-yet-stamped
cells → crash. Hence the intermittency: it depends purely on thread timing, and it correlates with a
DataGrid (re)rendering (e.g. right after a search populates one).

## Evidence

Captured at a live failure, suspended in `OnWSReceive` (where `e` is defined):

```
      c←(0=⊃¨e.⎕NC⊂'id')/e     ⍝ elements with no id
      ≢c
366
      ∪c.Tag
 thead  tr  th  tbody  td
```

366 un-id'd elements, all DataGrid cell tags.

## The fix

In `OnWSReceive`, filter to id-bearing elements before the lookup:

```
 e←Elements d
 e←(0≠⊃¨e.⎕NC⊂'id')/e         ⍝ keep only id-bearing elements
 i←e.id⍳c.CurrentTargetId c.TargetId
 c.(CurrentTarget Target)←(e,0)[i]
```


### Why this is correct, not just defensive

Browser events are routed by `id`: the page's `sendAPLRequest` sends `CurrentTargetId`/`TargetId`, which
are the `id`s of real, addressable elements. An element with no `id` can therefore never be the
`CurrentTarget` or `Target` of an event. Excluding id-less elements from the index search changes no
correct behaviour — it only stops the crash. It also makes `OnWSReceive` robust to any legitimately
id-less element (grid cells being the obvious example), not just this particular race.

## Optional additional hardening (defence in depth)

The `OnWSReceive` fix above fully resolves the crash. 

However, the window could also be closed at the source:

`DataGrid.BuildStructure` (and any similar create-then-stamp code) could assign ids before inserting
the new subtree into the live `Content` tree, so an id-less grid subtree is never observable by a
concurrent `Elements` walk. This is secondary; the `OnWSReceive` filter is the primary, general fix.

