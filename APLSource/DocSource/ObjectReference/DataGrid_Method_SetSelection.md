# DataGrid SetSelection Method

Sets the current selection.

~~~
R←I SetSelection UL BR
~~~

`I` is the DataGrid instance. `UL` is the cell address of the upperleft
corner. `BR` is the cell address of the bottom right corner.
A cell address is a row index and column index, or a row index
and column name. An index of `¯1` indicates the maximum row or column index.
`R` is resulting value of the [Selection]() property, which is always
given in explicit row and column indices of the cell addresses, regardless
of how it is set. 

To select a 3 by 4 set of cells at the starting at the 5th row and
column of the grid:


~~~
      G SetSelection (4 4) (6 7)
~~~

To select the first 5 rows:

~~~
      G SetSelection (0 0) (4 ¯1)
~~~

To select the entire grid:

~~~
      G SetSelection (0 0) (¯1 ¯1)  
~~~

To select the entire column named 'Balance'

~~~
      G SetSelection  (0 'Balance')  (¯1 'Balance')
~~~
