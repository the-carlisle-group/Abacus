# DataGridColumn OnFormat Property

A function that formats the column for display in HTML.
The default value uses the FormatString with ⎕FMT,
when appropriate, to format the value. 
The right argument provided to the function is the vector of column values to be formatted.
The left argument is the column specification namespace. 
This should rarely need to be specified, as setting FormatString should handle most cases. 
However, there may be times when complete control is desired.


