# HTMLElement GetElementById Method

~~~
    R←Y GetElementById X 
~~~

Y is an HTMLElement object. X character vector containing an id.
R is the HTMLElement associated with the id.

Signals an error if the id is not found.

Even though ids are generally unique accross a document, this method
is restricted to seaching only the node represeted by Y.     

