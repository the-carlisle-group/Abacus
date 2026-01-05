# DataGrid Autofocus Property

Boolean flag indicating that the DataGrid should get the focus
as soon as it is initialized. Defaults to `0`.

On startup, the [SetComponentFocus]() method will set the focus for most objects.
The DataGrid, however, is not configured until after the startup
callback runs (there are no cells to focus on) so this property should be used instead.
