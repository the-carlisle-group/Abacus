# HTMLComponent Object

## Description

An HTMLElement with added content, behavior and CSS.
  

## Commentary

As a component is an HTMLElement, any methods or properties of HTMLElement will work with components.

Components may be extremely complex, like the DataGrid component,
or fairly simple like the Button component. 

This entry in the reference covers aspects that all components have in common.
There is also an entry for each individual component.

A component is defined in a namespace. It must have a `New` function that creates the component
and returns it. It may optionally have a `CSS` function.

A component must have a [Name]() property. This is distinct from the HTML `name` attribute.  
