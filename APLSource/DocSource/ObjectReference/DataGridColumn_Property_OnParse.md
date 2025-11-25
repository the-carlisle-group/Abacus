# DataGridColumn OnParse Property

A function that parses the text entered when editing a cell,
and converts it to the appropriate data type. 
This function takes a simple text string as its right argument,
and the column specification namespace as its left argument.
It must return a 3-item vector containing a boolean to signify success (1) or failure (0),
the parsed value, and an error message.
Like OnFormat, this should rarely need to be specified.
It may be needed if OnFormat is specified in such a way that the default parsing insufficient.
If it is specified, there is the opportunity here to modify the value,
say removing all blanks, uppercasing, or moving a decimal place.
