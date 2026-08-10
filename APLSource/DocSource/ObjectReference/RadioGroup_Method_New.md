# RadioGroup New Method

Creates a new RadioGroup component — a labelled set of radio buttons.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the RadioGroup properties. `R` is the new RadioGroup.

## Examples

~~~
      rg←A.RadioGroup.New(Legend:'Size' ⋄ Labels:('Small' 'Medium' 'Large') ⋄ Options:1 2 3)
~~~
