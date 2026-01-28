# DataGrid DeleteRows Property

Boolean scalar. Allow or disallow to delete rows. The default is `1`.

This property only applies if ReadOnly is `0`.
If ReadOnly is `1`, rows may not be deleted.

Regardless of the value of this property, the application
may delete rows under program control using the [DeleteRows]() method.
