# HTMLElement GetComponent Method

Gets a component by Name under a specific node.

~~~
      R←I GetComponent X
~~~

`I` is an HTMLElement instance. `X` is the value of the `Name` property of a component.
`R` is the component (also an HTMLElement instance).

If the component is not found under the specified node, an error is signalled.

Component name are not required to be unique document wide. If more than one component
has the same name under the specified node, and error is signalled. 
