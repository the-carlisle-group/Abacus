# DataGridColumn Options Property

This property defines the options for `Select` column
or the autocomplete values for `Char` and `VarChar` columns.

It may be a list of items:

~~~
t.Options←'Bach' 'Beethoven' 'Mozart'
~~~

Or, for hierarchical autocomplete, it may be a namespace containing:

|Name |Description|
|:====|:=====|
|`Item`  | A list of simple or fully qualified names.|
|`Depth` | A depth vector if `Item` is a list of simple names. Optional. |
|`Type ` | A type or description corresponding to each item. Optional.|
|`Separator`| Path delimiter. Defaults to `'.'`|

If `Depth` is provided, then `Item` is treated as a list of simple names.

If `Depth` is not provided, then `Item` is treated as a list of fully qualified
names and is parsed according to `Separator` to compute simple names and depth.   

You can force a list of fully qualified names to be treated as a list of
non-hierarchical names by setting `Depth` to `0`.
