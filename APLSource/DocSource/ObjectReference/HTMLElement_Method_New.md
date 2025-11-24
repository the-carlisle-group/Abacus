# HTMLElement New Method

Creates a new HTMLElement object.

~~~
R←{Y} New T [C [A]]
~~~

`T` is the tag. `C` is optional content. `A` is optional matrix of attribute
names and values. `Y` is an optional parent element. `R` is the new HTMLElement.

## Examples

~~~
      d←A.New'div'
      A.Render d
<div></div>
      d←A.New'div' 'Hello world!'(2 2⍴'class' 'myclass' 'id' 'myid')
      A.Render d
<div class="myclass" id="myid">Hello world!</div>
~~~

