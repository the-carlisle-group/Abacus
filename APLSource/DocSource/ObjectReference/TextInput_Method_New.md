# TextInput New Method

Creates a new TextInput component — a labelled text entry, with optional autocomplete and
an optional picker button.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the TextInput properties. `R` is the new TextInput.

## Examples

~~~
      ti←A.TextInput.New'Search for:'
      ti←'SearchFor'A.TextInput.New(Label:'Search for:' ⋄ Options:'a' 'cause' '⎕IO')
~~~
