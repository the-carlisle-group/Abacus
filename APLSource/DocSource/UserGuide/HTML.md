# HTML

The following code assumes the Abacus API is instantiated as A, that is:

~~~
      A←#.Abacus.Main 
~~~

The `New` function creates a new HTML element:

~~~
      d←A.New 'html'
~~~

An element and all of its children are composed into HTML
using the DOM2HTML function

~~~
      A.DOM2HTML d  
<!DOCTYPE html>              
<html></html>     
~~~

The 'html' element is special-cased to include the !DOCTYPE declaration.

The `New` function optionally takes a left argument to be 
the parent of the newly created element:

~~~
      hd←d A.New 'head'
      mt←hd A.New'meta'
      b←d A.New'body'
      A.DOM2HTML d
<!DOCTYPE html>                                                                    
<html>                                                                             
  <head>                                                                           
    <meta></meta>                                                                  
  </head>                                                                          
  <body></body>                                                                    
</html>
~~~

Attributes may be directly assigned into an element:

~~~
      mt.charset←'utf-8'
      A.DOM2HTML d
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"></meta>
  </head>
  <body></body>
</html>
~~~

The New function takes an optional second item in its right argument,
to add content to an element at creation time: 

~~~
      h1←b A.New 'h1' 'Introduction'
      A.DOM2HTML d
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"></meta>
  </head>
  <body>
    <h1>Introduction</h1>
  </body>
</html>
~~~

Additional content may be added to an existing element using 
the Add function:

~~~
      _←h1 A.Add ' to Writing HTML'
      A.DOM2HTML d                                                                 
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"></meta>
  </head>
  <body>
    <h1>Introduction to Writing HTML</h1>
  </body>
</html>
~~~ 

Paragraphs with bold and italics may be constructed:

~~~
      p←b A.New 'p' 'This is some text.'
      _←p A.New 'em' 'This is emphasized.'
      _←p A.Add 'This is not.'
      A.DOM2HTML d 
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"></meta>
  </head>
  <body>
    <h1>Introduction to Writing HTML</h1>
    <p>
      This is some text.
      <em>This is emphasized.</em>
      This is not.
    </p>
  </body>
</html>      
~~~

Content is simple text or array of elements. Elements may be constructed
independently of the document and then directly added
to an element:

~~~                      
      ps←A.New¨{'p' ⍵}¨'This is a paragraph.' 'This is another paragraph.'
      b.Content,←ps
      A.DOM2HTML d
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"></meta>
  </head>
  <body>
    <h1>Introduction to Writing HTML</h1>
    <p>
      This is some text.
      <em>This is emphasized.</em>
      This is not.
    </p>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
  </body>
</html>
~~~ 

## Preformatted Text and Preformatted HTML 

The `DOM2HTML` function produces formatted HTML. A side effect of this is the removal of extraneous whitespace and newlines.
This is undesirable for text in pre elements (and perhaps certain other elements). The `EncodePre` function temporarily encodes text that is later decoded by the `DOM2HTML` function, so that whitespace and newlines are preserved exactly as written.

Preformatted HTML text may be inserted by enclosing. For example:

~~~
      A.DOM2HTML New 'p' (⊂⊂'This is a <em>bold</em> word')
<p>This is a <em>bold</em> word</p>
~~~

Note the use `enclose (⊂)` twice. If the string is not enclosed the result will have ampersand encoded values:

~~~  
      A.DOM2HTML New 'p' ('This is a <em>bold</em> word')
<p>This is a &lt;em&gt;bold&lt;/em&gt; word</p>
~~~  

## Working with the DOM

Once an HTML document (or any element, usually with children) is created, the 
elements can be extracted from the DOM tree into a simple vector:  

~~~
       e←A.Elements d
~~~

From this list it is simple to select and modify elements based on any of their
attributes or types, names, ids, or content. For example, to change all h2 and h3
elements to h4:

~~~
       e←A.Elements d 
       h←e/⍨e.Type∊'h2' 'h3'
       h.Type←'h4' 
~~~

However, a couple of additional functions are provided. The `ElementsWhere` function
selects elements where an attribute equals a particular value:  

~~~
       a←d A.ElementsWhere 'Type' 'p'
       c←d A.ElementsWhere 'class' 'myclass'
~~~

The `ElementById` function selects a single element by its id:   

~~~
       zip←d A.ElementById 'zipcode'
       Zip.Content←'33040'
~~~


