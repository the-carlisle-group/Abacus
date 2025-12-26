# DataGrid RowMask Property

The `RowMask` property is a Boolean vector corresponding to the number
of data rows, indicating which rows are to be displayed.

It defaults to 1 (with scalar extension), to display all rows.

It is only applicable if [ReadOnly]() is `1`

The [SetRowMask]() method should be used to change this property
after the application is up.
