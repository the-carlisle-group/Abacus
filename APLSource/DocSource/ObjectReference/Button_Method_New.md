# Button New Method

Creates a new Button component.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the Button properties. `R` is the new Button.

## Examples

~~~
      b←A.Button.New'Find'
      b←A.Button.New(Caption:'Find' ⋄ Shortcut:'Ctrl+F' ⋄ OnClick:A.FQP'OnFind')
~~~
