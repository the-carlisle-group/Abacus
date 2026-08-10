# CheckBox New Method

Creates a new CheckBox component.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the CheckBox properties. `R` is the new CheckBox.

## Examples

~~~
      cb←A.CheckBox.New'Match case'
      cb←'MatchCase'A.CheckBox.New(Label:'Match case' ⋄ Value:1)
~~~
