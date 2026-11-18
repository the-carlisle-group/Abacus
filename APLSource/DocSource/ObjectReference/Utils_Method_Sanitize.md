# Utils Sanitize Method

Escapes text so that it can be embedded in a single-quoted JavaScript string: carriage returns are
dropped and each `'` becomes `&#39;`.

~~~
    R←Sanitize X
~~~

`X` is a simple character vector. A nested argument is not supported, so flatten first.
`R` is the escaped text.
