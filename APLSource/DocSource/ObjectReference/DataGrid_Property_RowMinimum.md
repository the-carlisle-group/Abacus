# DataGrid RowMinimum Property

The `RowMinimum` property specifies the minimum number
of rows the grid should display, regardless of data size.
Only applicable if [ReadOnly]() is `1`.

This just gives nice grid lines when the grid is empty or very small.
When deleting rows, a new empty row is appended if necessary to keep the minimum. 

The default is `10`.

It is left up to the application to remove any undesired trailing empty rows.
