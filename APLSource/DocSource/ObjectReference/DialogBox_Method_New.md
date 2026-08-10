# DialogBox New Method

Creates a new DialogBox component — a modal dialog with a header, content and footer buttons.

~~~
R←{D} New W
~~~

`D` is an optional Document. `W` is a namespace (or shortcut list) of properties — see the
DialogBox properties. `R` is the new DialogBox. Show it with `ShowModal` (or `showModal`).

## Examples

~~~
      d←doc A.DialogBox.New(Title:'Confirm' ⋄ MainContent:(A.New'p' 'Are you sure?') ⋄ Buttons:'Yes' 'No')
~~~
