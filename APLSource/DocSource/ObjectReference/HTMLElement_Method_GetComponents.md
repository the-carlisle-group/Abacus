# HTMLElement GetComponents Method

Returns a vector of name/value pairs of all the components under an element.

~~~
      R←I GetComponents ''
      R←GetComponents I 
~~~

I is an HTMLElement instance. R vector of name/value pairs.

For a namespace `S` of components use:

~~~
     S← () ⎕VSET R 
~~~
