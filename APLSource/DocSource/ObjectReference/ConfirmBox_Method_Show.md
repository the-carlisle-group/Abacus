# ConfirmBox Show Method

Displays a ConfirmBox. 

~~~
   R←I ConfirmBox.Show ''
~~~

or

~~~
   R←ConfirmBox.Show I
~~~

`I` is the ConfirmBox instance. `R` is a string with the button caption of the selection.
`R` is an empty vector if Escape is pressed.

This method waits in APL for the user to make a selection,

See the HTMLDocument [Confirm]() method for easiest use of the ConfirmBox,
encapsulating the `New` and `Show` methods.
