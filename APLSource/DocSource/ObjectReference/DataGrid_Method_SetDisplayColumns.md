# DataGrid SetDisplayColumns Method

Sets the [DisplayColumns]() property.

~~~
R←I SetDisplayColumns X
~~~

`I` is a DataGrid instance. `X` is a vector of vectors of column names.
`R` is `0`.

If `X` is an empty vector, all columns are displayed. Names not found
are ignored.

This method should be used to set the DisplayColumns property after
the application is up and running.
