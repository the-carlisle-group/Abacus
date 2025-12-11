# HTMLElement GetComponentValues Method

Returns all component name/value pairs under an element.

~~~
      R←I GetComponentValues 0
      R←GetComponentValues I
~~~

`I` is an HTMLElement Instance. R is a vector of name/value pairs
for each component found in `I`. 

To get a namespace `S` of values use: 

~~~
      S←() ⎕VSET R
~~~
