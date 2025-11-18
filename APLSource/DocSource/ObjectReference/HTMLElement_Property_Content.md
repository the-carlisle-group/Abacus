# HTMLElement Content Property

The `Content` property is an array of HTMLElements and/or simple text vectors.
The Abacus DOM does not have formal text nodes.

Content may be specified when an element is created:

~~~
      e←A.New 'p' 'This is some text'
      A.Render e
<p>This is some text</p>
~~~

Or specified after the fact:

~~~
      e.Content←(A.New 'span' 'Hello') ' world!' 
      A.Render e
<p>
  <span>Hello</span>
  world!
</p>
~~~

The `Add` method may be used to add additional content to an element:

~~~
      e A.Add ' More text.'
#.Abacus.Main.[Namespace]
      A.Render e
<p>
  <span>Hello</span>
  world! More text.
</p>
~~~

