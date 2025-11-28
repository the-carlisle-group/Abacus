# DataGridColumn Object

## Description

Specifies a column for the DataGrid.

## Commentary

A `DataGridColumn` is created as a plain namespace. There is no `New` function or constructor.

To create a new `DataGridColumn` object, simply create a new namespace and 
populate it with desired properties:

~~~
   c←()
   c.Name←'MaturityDate'
   c.Type←'Date'
   c.Value←20501201 20390701 20280301 
~~~
