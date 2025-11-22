# Introduction

Abacus is composed of two things: a collection of functions, and a collection of
namespaces representing UI components. Currently all functions and components are found
under `#.Abacus.Main`. In all of the documentation, and in the sample applications,
it is assumed that, in the current namespace, for easy access: 

~~~
      A←#.Abacus.Main 
~~~

It is recommended you do this in your application as well.

Somewhere in the set of functions an object model is struggling to reveal itself.
So some of these functions may be classified as
public instance methods, some as static methods, and the rest as private methods.

Abacus does not use formal Dyalog APL classes. It is possible that at some point in the 
future that will change, but for now objects are represented as plain namespaces.
 
An example will make this clear.

We can use the [New]() function to create a new [HTMLElement]() object.
This returns a plain namespace. It has some variables in it, which act as properties:

~~~
      e←A.New 'div' 'Hello world!'
      e
HTMLElement
      e.Tag 
div
      e.Content
 Hello world! 
~~~

> We use `⎕DF` to set the display format of the HTMLElement namespace. 

We can use the [Add]() function to add some more content:

~~~
      e A.Add ' Good morning!'
HTMLElement
~~~

And we can use the [Render]() function to display the HTML: 

~~~
      e A.Render ''
<div>Hello world! Good morning!</div>
~~~

The `Add`  and `Render` functions take an HTMLElement as their left argument. They thus
behave like instance methods, while the `New` function behaves like a static method.
Instance methdods that take no meaningful right argument may also, for convenience,
be called monadically by placing the instance on the right:

~~~
      A.Render e
<div>Hello world! Good morning!</div>
~~~

Abacus formally documents the HTMLElement object as a class with methods
and properties. Almost all of the other formally documented objects are just
`HTMLElement` objects in disguise, so all of the methods and propertites that
apply to `HTMLElement` will apply to them as well. These objects include [HTMLDocument](),
[HTMLTable](), and all of the [UI components](HTMLComponent). It's pretty simple, there is not that much to learn.

The only objects not based on HTMLDocument are [CSSRule]()  and [Application().

Objects with their properties and instance methods are documented in the [Object Reference]().
Static functions are documented in the [Function Reference]().

