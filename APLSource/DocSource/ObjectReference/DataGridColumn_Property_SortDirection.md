# DataGridColumn SortDirection Property

Integer scalar. A zero indicates no sort, a positive value indicates
ascending order, a negative value indicates descending order.

The magnitude indicates the sort priority; lower absolute value is
higher priority.

For example, if `c` is an array of of 3 DataColumns, to sort the grid
in descending order on the first column, and within that sort in 
ascendening order by the third column, we would write:  

~~~
      c.SortOrder←¯1 0 2
~~~

This property only applies when [ReadOnly]() is `1`.
