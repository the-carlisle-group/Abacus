# TreeView Object

## Description

Represents a tree.

## Commentary

The TreeView object is modelled on the `⎕WC` TreeView object. 

The [Items]() property specifies an array of text vectors,
or an array of arbitrary DOM content.  

The [Depth]() property specifies the corresponding depth of each item. 

The TreeView supports debouncing the [Select]() event for keyboard
navigation.
