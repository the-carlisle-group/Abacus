# HTMLComponent Object

An HTMLComponent is an HTMLElement with, usually, child elements, added behavior and CSS.  
Therefore, any methods or properties of HTMLElement will with work with components.

Components may be extremely complex, like the DataGrid component,
or fairly simple like the Button component. 

This entry in the reference covers aspects that all components have in common.
There is also an entry for each individual component.

A component is defined in a namespace. It must have a `New` function that creates the component
and returns it. It may optionally have a `CSS` function.

A component must have a [Name]() property. This is distinct from the HTML `name` attribute.  
