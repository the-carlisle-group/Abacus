# Panels GridTemplateAreas Property

The GridTemplateAreas property is matrix that graphically specifies
how the grid items should be layed out.
Grid items may be identified by index (just the order they appear in 
the content) or by id.

For example, if there are 4 elements in the [Content]() property,
then:

~~~
     g.GridTemplateAreas←[
                           0 0 1
                           2 3 3
                           2 3 3
                        ]
~~~

lays out the four elements as shown.

In this example there are only 2 implied grid rows. The 
doubling up indicates that the second row should be twice the size of
the first row explicit row sizes are not specified.

If the property elides elements they will be hidden.

The items may be placed in any order, but must make up rectangular areas. 

This property does not map directly to the eponymously named CSS grid property 
grid-template-areas, though it is analagous.
