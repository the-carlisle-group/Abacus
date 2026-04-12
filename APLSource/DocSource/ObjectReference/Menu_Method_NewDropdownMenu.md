# Menu NewDropdownMenu Method

Creates a dropdown menu.

~~~
  I←NewDropdownMenu F
~~~

`F` is a function that returns a [menu](Menu).
`I` is a menu whose class is DropdownMenu.

The argument `F` is a string containing the fully qualified path of the 
 menu building function. This function is executed
 every time the menu button is clicked, recreating the menu,
 allowing for dynamic setting of item states like [Checked]() or [Disabled]().
 
 The right argument passed to the menu function is the document, providing
 access to any state needed to set the menu.
