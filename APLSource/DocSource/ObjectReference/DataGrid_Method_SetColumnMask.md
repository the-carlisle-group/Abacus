# DataGrid SetColumnMask Method

Sets the [ColumnMask]() property.

~~~
R←I SetColumnMask X
~~~

`I` is a DataGrid instance. `X` is a list of column names.
`R` is `0`.

If `X` is an empty vector, all columns are displayed. Names not found
are ignored.

This method should be used to set the `ColumnMask` property after
the application is up and running.
