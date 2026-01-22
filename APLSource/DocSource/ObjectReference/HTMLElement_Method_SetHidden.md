# HTMLElement SetHidden Method

Adds or removes the Abacus `hidden` class from an element. 

~~~
      R←I SetHidden B
~~~

> This is an APLDOM to browser DOM synchronized method.

`I` is the HTMLElement instance. `B` is a scalar Boolean, `1` or `0`.
`R` is 0.

The `hidden` class sets the display property to "none".
This takes the element out of flow and may alter the layout.

To make an element invisble without altering the rest of the layout, use the
[SetInvisible]() method. 
