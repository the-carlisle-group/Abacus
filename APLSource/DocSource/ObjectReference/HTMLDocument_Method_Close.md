# HTMLDocument Close Method

Closes a desktop application. 

~~~
    R←I Close 0
    R←Close I
~~~

`I` is an HTMLDocument instance. `R` is `0`

This method is typically called inside the callback for [BeforeClose]().  
If a callback is attached to `BeforeClose` this method must be called
to close the application.
