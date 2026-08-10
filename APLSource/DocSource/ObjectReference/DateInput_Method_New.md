# DateInput New Method

Creates a new DateInput component — a labelled date entry.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the DateInput properties. `R` is the new DateInput.

## Examples

~~~
      di←A.DateInput.New'Date:'
      di←A.DateInput.New(Label:'Date:' ⋄ Value:20260810)
~~~
