# HTMLElement SetInvisible Method

Adds or removes the Abacus `invisible` class from an element. 

~~~
      R←I SetInvisible B
~~~

> This is an APLDOM to browser DOM synchronized method.

`I` is the HTMLElement instance. `B` is a scalar Boolean, `1` or `0`.
`R` is 0.

The `invisible` class sets the CSS visibility property to "hidden". 
The element will still be in flow, so the layout of the document will not change.

To remove an element from flow use the [SetHidden]() method.
