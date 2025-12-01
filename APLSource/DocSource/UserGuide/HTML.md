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

Because the HTMLElement instance `e` is just a plain namespace with variables,
we can display it as JSON:

~~~
      ⎕JSON e
{"Content":"","Parent":0,"Tag":"div"}
~~~

HTML attributes for the element may be specified directly by assignment:

~~~
      e.class←'mydiv'
      e.id←'myid'
      A.Render e
<div class="mydiv" id="myid"></div>
      ⎕JSON e
{"Content":"","Parent":0,"Tag":"div","class":"mydiv","id":"myid"}
~~~

Attribute names are always lowercase, which distinguishes them from Abacus
properties, like [Tag](),  [Content](), and [Parent](). Use an underscore in place
of a dash when needed:

~~~
      e.data_value←'abc'
      A.Render e
<div class="mydiv" data-value="abc" id="myid"></div>
~~~

You can stuff your own
application specific variables in an element, just like with `⎕WC` objects.
Use an underscore or an uppercase letter, careful to avoid name conflicts:

~~~
      e._MyProperty←3.14
      A.Render e
<div class="mydiv" data-value="abc" id="myid"></div>
~~~

Content can be added to an element at creation time using the `New` function:

~~~
      c←A.New 'h1' 'Hello world!'
      A.Render c
<h1>Hello world!</h1>
~~~

You can also just directly assign the content property:

~~~
      e.Content←c
      A.Render e
<div class="mydiv" data-value="abc" id="myid">
  <h1>Hello world!</h1>
</div>
~~~
  

      
