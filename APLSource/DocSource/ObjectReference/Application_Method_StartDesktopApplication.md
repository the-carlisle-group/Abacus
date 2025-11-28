# Application StartDesktopApplication Method

Starts up a desktop application

~~~
  R←[Y] StartDesktopApplication X 
~~~

`Y` is the application object. `X` is 0 or an HTMLDocument. 
`R` is the HTMLDocument object. 

If `Y` is not provided, then `X` must be a document.
In this case, an Application object is created internally,
and may be accessed under the documents Application property.

If `Y` is provided, X should 0, and the document is created using
the OnBuild property function.
