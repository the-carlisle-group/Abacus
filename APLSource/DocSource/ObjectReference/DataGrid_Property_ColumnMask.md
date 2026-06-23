# DataGrid ColumnMask Property

The ColumnMask property is a list of column names to be displayed.
The list indicates both a restiction and an ordering. 
This allows the application to present different views of the data
without changing the [Columns]() property.

An empty list (the default) indicates that all columns should be displayed
in the order given by the `Columns` property.

The [SetColumnMask]() or [SetMask]() method should be used to change this property
after the application is up. 

It is only applicable when [ReadOnly] is `1`.

See also [RowMask]().
