# TextArea New Method

Creates a new TextArea component — a labelled multi-line text entry.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the TextArea properties. `R` is the new TextArea.

## Examples

~~~
      ta←A.TextArea.New'Notes:'
      ta←A.TextArea.New(Label:'Notes:' ⋄ Value:'initial text')
~~~
