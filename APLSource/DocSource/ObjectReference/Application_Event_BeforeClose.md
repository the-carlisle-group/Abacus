# Application BeforeClose Event

For a desktop application, this event occurs
after a user attempts to close the main form or quit the application.
This provides an opportunity to save state or confirm the action.

For a web application, this event occurs when the connection is lost
or closed.

The callback is called monadically; its right argument is the application's
`Document`. The result must be `0` to proceed with the close as requested,
or `1` to keep the window open.

There is no way to prevent a web application from closing.

## Remarks

### Abacus' own modal dialogs may be used here

You can call Abacus' own modal boxes — `Confirm`, `Alert`, `Prompt` — directly
from the `BeforeClose` handler, for example to ask *"Are you sure you want to
close?"*. This is the recommended, cross-platform way to guard a close; there is
no need to fall back on a native, Windows-only message box (`⎕WC 'MsgBox'`).

```apl
Close←{
    ⍝ ⍵ ←→ Document. Return 0 to close, 1 to keep open.
    'Yes'≢⍵ A.Confirm'Close' 'Are you sure you want to close?'
}
```

`Confirm` returns the caption of the button the user chose (`'Yes'`/`'No'`),
or an empty vector if the dialog was dismissed with `Escape`. So `'Yes'≢…`
keeps the window open unless the user explicitly confirms.

### Why this needs care (the deadlock that used to bite)

`Confirm` *blocks* the calling thread on a token (`⎕TGET`) and waits for the
user's click to arrive back over the websocket and release it. For that to
work, the thread that dispatches the incoming click must **not** be the one
that is blocked waiting for it.

The native close notification fires on Abacus' `⎕DQ`/UI thread — the very
thread that also delivers a modal dialog's click. If the `BeforeClose` handler
ran there and put up a `Confirm`, it would block that thread and the click
could never be delivered: the application would **deadlock**. (This is why, in
earlier versions, a `Confirm` in `BeforeClose` hung and a native message box was
used instead.)

Abacus now avoids this automatically: it runs the `BeforeClose` handler on a
**separate thread**, off the UI thread, and only vetoes or performs the close
once the handler has returned. Your handler therefore does not need to do
anything special — it may block on a modal dialog freely. As a consequence the
handler runs *asynchronously*: the window closes a moment after the handler
returns `0`, not synchronously within the notification.
