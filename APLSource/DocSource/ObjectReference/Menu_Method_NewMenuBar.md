# Menu NewMenuBar Method

Creates a menu bar.

~~~
  I←NewMenuBar F
~~~

`F` is a function that returns a [menu](Menu).
`I` is a menu whose class is MenuBar.

 The argument `F` is a string containing the fully qualified path of the 
 menu building function. This function is executed once when the menu bar is
 initialized in order to extract the top-level items. It is then executed
 every time a top-level menu is displayed, allowing for dynamic setting of item states
 like [Checked]() or [Disabled]().
 
 The right argument passed to the menu function is the document, providing
 access to any state needed to set the menu.

