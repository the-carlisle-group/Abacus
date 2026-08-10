# NumberInput New Method

Creates a new NumberInput component — a labelled numeric entry.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the NumberInput properties. `R` is the new NumberInput.

## Examples

~~~
      ni←A.NumberInput.New'Count:'
      ni←A.NumberInput.New(Label:'Count:' ⋄ Value:0 ⋄ Format:'I10')
~~~
