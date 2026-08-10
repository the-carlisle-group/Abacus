# DataGrid New Method

Creates a new DataGrid component.

~~~
R←{P} New W
~~~

`P` is an optional parent element. `W` is a namespace (or shortcut list) of properties — see
the DataGrid properties. `R` is the new DataGrid. The data is supplied through the `Columns`
property (or, after creation, with `SetColumns`).

## Examples

~~~
      g←A.DataGrid.New''
      g←A.DataGrid.New(ReadOnly:1 ⋄ RowNumbers:1)
~~~
