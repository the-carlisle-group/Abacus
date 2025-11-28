# DataGridColumn OnValidate Property

A function that provides additional validation to the [OnParse]() function.
This function takes the parsed result as its right argument and the column
specification namespace as its left argument, and then produces a result in the form as OnParse.
This handler is designed more for common usage than [OnFormat]() or [OnParse]().
It is applied after OnParse is called, and we know that we have a valid type for the column.
It allows for both validation and for possible modification of the value (like OnParse),
like uppercasing or scaling.
