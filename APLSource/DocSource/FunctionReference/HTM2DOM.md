# HTML2DOM

Converts HTML into an HTMLElement.

~~~
R← HTML2DOM X
~~~

`X` is a string of HTML. R is an HTMLElement.

## Examples

~~~
      e←A.HTML2DOM '<div class="mydiv"><p>Hello world!</p></div>'
      e.class
mydiv
      e.Content.Tag
 p 
      e.Content.Content
  Hello world!  
~~~
