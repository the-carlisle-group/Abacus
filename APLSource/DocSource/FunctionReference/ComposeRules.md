# ComposeRules

Composes CSS rules into text.

~~~
R←ComposeRules X
~~~

`X` is an array of CSS rule objects.
`R` is a simple character vector with linefeeds containing the CSS.


## Examples:

~~~
       r1←A.NewRule 'h1'
       r1.padding←'2rem'
       r2←A.NewRule 'h2'
       r2.margin←'10px'
       A.ComposeRules r1 r2
h1 {
    padding: 2rem;
}

h2 {
    margin: 10px;
}
~~~
