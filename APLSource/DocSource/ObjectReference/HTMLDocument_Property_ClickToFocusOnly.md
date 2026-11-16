# HTMLDocument ClickToFocusOnly Property

Boolean property that controls how an out-of-focus application responds to a mouse click.

The default value, `0`, indicates **click-through** behavior. This means that the mouse click
will both bring the application into focus **and** pass the click to any underlying element like
a button.   

A value of `1` provides **click-to-focus-only** behavior. This means that the mouse click
will bring the application into focus only, and a second click would be required to activate
any underlying element.
