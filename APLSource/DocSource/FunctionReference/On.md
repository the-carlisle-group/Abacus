# On

Sets the focused or current element in a test suite.

~~~
R←[X] On Y
~~~

`Y` is an `id` or `Name`. `X` is a suitable argument for some other funciton.  
`R` is `X` if provided, else `Y`.

This is a cover for [Focus]() that passes the left argument `X`, or `Y` if `X` is not
provided, back as result `R`. It improves the succintness and readability of test functions.
For example:

~~~
      Press 'Home' On 'MyGrid'
      Enter 'Hello world!' On 'MyTextField'
~~~

`On` may also be used with `Click`, though it is not necessary:

~~~
      Click On 'MyButton'
~~~
