# HTMLDocument RunUnderRoot Method

Runs a function under the root thread from a child thread.

~~~
    R←RunUnderRoot F A
~~~

This is a static method that does not require an HTMLDocument instance.

`F` is the fully qualified name of a function.
`A` is an appropriate right argument to `F`
`R`  is `0`.

The result of function `F` is not used.
