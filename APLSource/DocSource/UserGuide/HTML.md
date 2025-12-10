# HTML

Constructing and manipulating HTML is foundational to Abacus.
From static web sites to dynamic desktop applications, building
and messing around with HTML is a critical task. We shun templating.
We eschew string catenation. We want to create and operate on HTML
in APL code. This starts with creating HTML elements as objects, which in Abacus
are plain, simple namespaces. 

> Remember: `A←#.Abacus.Main`

The [New]() function creates a new [HTMLElement]() object:

~~~
      e←A.New 'div'
~~~

The [Render]() function constructs the HTML:

~~~
      A.Render e
<div></div>
~~~

We can add content when creating a new element:

~~~
      e←A.New 'div' 'Hello world!'
      A.Render e
<div>Hello world!</div>
~~~

The `New` method accepts two explicit properties [Tag](), and [Content](HTMLElement/Properties/Content),
which, like `⎕WC`, may be specified by position or by name.
HTML attributes may also be specified in the argument to `New`. These
must be specified by name:

~~~
      e←A.New 'div' 'Hello world!'  ('id' 'myid')
      A.Render e
<div id="myid">Hello world!</div>
~~~

HTML attributes for the element may be specified directly by assignment,
after the element has been created:

~~~
      e.class←'myclass'
      A.Render e
<div class="myclass" id="myid">Hello world!</div>
~~~

Attribute names are always lowercase, which distinguishes them from Abacus
properties, like [Tag](),  [Content](), and [Parent](). Use an underscore in place
of a dash when needed:

~~~
      e.data_value←'abc'
      A.Render e
<div class="mydiv" data-value="abc" id="myid"></div>
~~~

Inline styles may be specified by preceeding them with an underscore:

~~~
      e←A.New 'div' ('id' 'myid') ('_width' '7rem')
      A.Render e
<div id="myid" style="width:7rem"></div>
~~~

Like attributes, styles my specified by direct assignment:

~~~
      d←A.New 'div' ('_width' '3rem')
      d._background_color←'red'
      A.Render d
<div style="background-color:red;width:3rem"></div>
~~~

The HTML style attribute takes precedence over using style variables: 

~~~
      e←A.New'div'
      e.style←'color:blue'
      e._color←'red'
      e._width←'3rem'
      A.Render e
<div style="color:blue"></div>
      e.⎕EX'style'
      A.Render e
<div style="color:red;width:3rem"></div>
~~~

You can stuff your own
application specific variables in an element, just like with `⎕WC` objects.
Like attrribute and styles, they may be specified either at create time
or after the fact. Be sure to avoid name conflicts.   
It will always be safe to start with an underscore followed by an uppercase letter:

~~~
      e←A.New'div' ('_MyProperty' 5)
      e._MyOtherProperty←7
      A.Render e
<div></div>
      e._MyProperty+e._MyOtherProperty
12
~~~
