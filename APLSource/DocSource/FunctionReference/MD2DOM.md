# MD2DOM

Converts markdown into HTMLElement objects. 

~~~
R←MD2DOM X
~~~

`X` is a nested vector of markdown.
`R` is an array of HTMLElement objects.

Examples:

~~~
      A.MD2DOM '# Heading' '' 'A paragraph with some code `{(+/⍵)/≢⍵}` for the average.'
 HTMLElement  HTMLElement 
      A.Render A.MD2DOM '# Heading' '' 'A paragraph with some code `{(+/⍵)/≢⍵}` for the average.'
<h1>Heading</h1>
<p>
  A paragraph with some code
  <code>{(+/⍵)/≢⍵}</code>
  for the average.
</p>
~~~
