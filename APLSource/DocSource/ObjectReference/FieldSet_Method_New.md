# FieldSet New Method

Creates a new FieldSet component — a bordered group of controls with an optional legend.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the FieldSet properties. `R` is the new FieldSet.

## Examples

~~~
      fs←A.FieldSet.New(Content:(cb1 cb2) ⋄ Legend:'Options' ⋄ Border:1)
~~~
