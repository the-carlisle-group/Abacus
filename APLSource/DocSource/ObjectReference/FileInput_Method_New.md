# FileInput New Method

Creates a new FileInput component — a TextInput with a button to browse for a file.

~~~
R←{PN} New W
~~~

`PN` is an optional parent element, a name, or a `(parent name)` pair; if omitted, the
name is taken from the variable the result is assigned to. `W` is a namespace (or shortcut
list) of properties — see the FileInput properties. `R` is the new FileInput.

## Examples

~~~
      fi←A.FileInput.New'File:'
~~~
