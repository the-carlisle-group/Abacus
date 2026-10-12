# Utils IsString Method

Tests whether an array is character data.

~~~
    R←IsString X
~~~

`X` is any array.
`R` is 1 when `X` is a simple character array of any width, otherwise 0. A nested array, even one
of character vectors, gives 0.
