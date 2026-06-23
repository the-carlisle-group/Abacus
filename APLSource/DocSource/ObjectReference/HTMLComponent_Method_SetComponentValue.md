# HTMLComponent SetComponentValue Method

Sets the `Value` property for a component

~~~
   R←C SetComponentValue V
~~~

where `C` is the component instance and `V` is the value.

or

~~~
   R←D N SetComponentValue V
~~~

where `D` is the document instance, `N` is the component name
and `V` is the value.

`R` is `0`. 

> There is no corresponding `GetComponentValue` method, as the value may be accessed direclty via the `Value` variable without the need for a getter function.

See also [SetComponentValues]() for setting multiple values at once.
