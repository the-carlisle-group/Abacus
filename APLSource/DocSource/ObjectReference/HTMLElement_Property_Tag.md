# HTMLElement Tag Property

The `Tag` property returns the type of the element.
Usually this property is set by the [New]() function and never changed.
However, it may be set after the fact, which is useful for restructuring
existing HTML documents.

## Examples   

~~~
      e←A.New¨'h1' 'h2' 'h3'
      e.Tag
 h1  h2  h3 
      e.Tag←⊂'h4'
      e.Tag
 h4  h4  h4 
~~~


