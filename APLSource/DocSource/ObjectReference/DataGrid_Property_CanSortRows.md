# DataGrid CanSortRows Property

Boolean scalar. Determines if the user may sort the rows of the grid.

If [ReadOnly]() is `1`, sorting is virtual. The `Value` properties
of [DataGridColumn]() objects are not changed.

If `ReadOnly` is `0`, then the sorting is physical, 
and `Value` properties of the `DataGridColumn` objects are changed.

The [SortDirection]() property of the [DataGridColumn]() object
may be used to specify an initial order,
or to query the sort order. 
