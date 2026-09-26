# ConfirmBox New Method

Creates a new ConfirmBox.

~~~
    R←{D} New X
~~~

`D` is an optional Document.
`X` is a namespace, or a shortcut list, of properties: see the ConfirmBox properties.
`R` is the new ConfirmBox.

Display it with the [Show]() method. For the simple case use the HTMLDocument [Confirm]()
method, which combines `New` and `Show`.

## Examples

~~~
      cb←doc A.ConfirmBox.New(Title:'Delete' ⋄ Message:'Delete the selected rows?' ⋄ Buttons:'Delete' 'Keep')
~~~
