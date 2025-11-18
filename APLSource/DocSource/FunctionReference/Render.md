# Render

Converts a DOM node into HTML, formatted for display purposes. 

~~~
R←Render X
~~~

`X` is an HTMLElement (a document node).
`R` is a simple character vector with linefeeds.


`Render` is implemented as:

~~~
 Render←{
     ⎕XML⍣2 DOM2HTML ⍵
 }
~~~

## Examples

~~~
      A.Render A.New 'div' 'Hello world!'
<div>Hello world!</div>
      d←A.NewDocument 'Hello World'
      A.Render d
<html lang="en">
  <head>
    <meta charset="utf-8"></meta>
  </head>
  <body>Hello World</body>
</html>
~~~
