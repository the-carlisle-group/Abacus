# DataGrid ReadOnly Property

The `ReadOnly` Boolean property specifies whether or not the DataGrid is
read-only or not, and controls the applicability of other properties. The default is 0.

If ReadOnly is `0`, then the following properties are applicable:
[InsertRows](), [DeleteRows](), [InsertColumns](), [DeleteColumns](), 
[MoveRows](), [MoveColumns](), [RenameColumns](), [RowMinimum]().

If ReadOnly is `1`, then the following properies are applicable:
[FilterRows](), [FilterColumns](), [SortRows](), [RowMask](), [DisplayColumns]()
