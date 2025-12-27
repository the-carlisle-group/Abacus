# DataGrid DisplayColumns Property

The DisplayColumns property is a list of column names to be displayed.
This allows the application to present different views of the data
without changing the [Columns]() property.

The [SetDisplayColumns]() method should be used to change this property
after the application is up. 

It is only applicable when [ReadOnly] is `1`.
