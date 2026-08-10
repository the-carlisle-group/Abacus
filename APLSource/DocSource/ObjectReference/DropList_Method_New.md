# DropList New Method

Creates a new DropList component — a labelled drop-down selection.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the DropList properties. `R` is the new DropList.

## Examples

~~~
      dl←A.DropList.New(Label:'Colour:' ⋄ Options:'Red' 'Green' 'Blue')
~~~
