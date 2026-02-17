# DataGrid SetMask Method

Sets the [RowsMask]() and [ColumnMask]() property.

~~~
   R←I SetMask R C
~~~

`I` is a DataGrid instance. `R` is a Boolean vector the same length
as the number of rows in `I`, marking rows to be dislayed.  

`C` is either a Boolean vector, or a list of column names.
If a Boolean, it must be the same length as the number of columns
in `I`, marking columns to be dislayed. If a list of column names,
it indicates the columns to be displayed and their order.

`R` is `0`

This method should be used after the application is up and running and the
DataGrid has been initialized.
