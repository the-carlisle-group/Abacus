# Panels GridTemplateColumns Property

(Almost) directly specifies the CSS grid-template-columns property.
Specified as a vector of vectors rather than a space
delimited simple character vector.
For example:   

~~~
   g.GridTemplateColumns←'1fr' '2fr' 'auto' 
~~~

If empty (the default), and if [AutoSize]() or [AutoSizeColumns]() is `1`,
then this property is effectively set to `n⍴⊂'auto'`, where n is the number of columns.

If empty, and [AutoSize]() and [AutoSizeColumns]() are both `0`,
then this property is based on the proportions implied by the [GridTemplatAreas] property.
For example if:

~~~
      g.GridTemplateAreas←[ 
                            0 0 0 0
                            1 1 1 2
                            3 3 3 4
                            ]
~~~

Then this property is effectively set to

~~~
  '3fr' '1fr'
~~~

As there are two implied colums, and the first column should take up three quarters
of the available space, and the second column should take up one quarter.

