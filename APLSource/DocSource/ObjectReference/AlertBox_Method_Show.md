# AlertBox Show Method

Displays an alert box.

~~~
   R←I AlertBox.Show ''
~~~

or

~~~
   R←AlertBox.Show I
~~~

`I` is the AlertBox instance. `R` is '0'.

This method does not wait, and generally should be the last line of a callback,
with no following code. 

See the HTMLDocument [Alert]() method for easiest use of the AlertBox,
encapsulating the `New` and `Show` methods.
