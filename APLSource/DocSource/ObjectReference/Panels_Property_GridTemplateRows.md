# Panels GridTemplateRows Property

(Almost) directly specifies the CSS grid-template-rows property.
Specified as a vector of vectors rather than a space
delimited simple character vector.
For example:   

~~~
   g.GridTemplateRows←'1fr' '2fr' 'auto' 
~~~

If empty (the default), and if [AutoSize]() or [AutoSizeRows]() is `1`,
then this property is effectivley set to `n⍴⊂'auto'`, where n is the number of rows.

If empty, and [AutoSize]() and [AutoSizeRows]() are both `0`,
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
  '1fr' '1fr'  '1fr'
~~~

As there are three implied rows, and each should take up the same amount of space.
