# The DataGrid Component

The DataGrid component implements a high-performance, virtual HTML table.

## Design Goals

The Abacus DataGrid is primarily designed for the viewing, editing and manipulation of tables.
It is explicitly NOT designed to be a vehicle for presentation, reporting, or spreadsheets. 
This means columns are expected to be the same type and rows are all the same height. Columns
are named, rows are not. (The programmer can of course simulate row names by properly defining
the first column.) The font is uniform across all cells. Cells are never spanned.
The scroll and edit experience is designed to be as close to common spreadsheet
applications as possible.

The Abacus DataGrid is not a general purpose grid like the `⎕WC` grid, but rather a special purpose
grid that one might build on top of `⎕WC` grid.

At the Carlisle Group we have two primary uses that we are coding for. The first is viewing and manipulating
relatively large database tables with millions of rows and/or hundreds, even thousands, of columns.
The second is creating, viewing and editing smaller metadata tables, like table schemas, configuration tables,
and name/value pairs.
 
The DataGrid can easily handle arbitrarily large tables, as long as the raw data values fit in memory.
Out of the box it supports editing individual cells, cell selection and cut/copy/paste. It supports inserting,
deleting, and moving rows and columns. It supports renaming columns. It supports find and replace.

Column types may be Char, Date, Int, Float, DecN, Select, MultiSelect and CheckBox. Other types will
no doubt be added in the future. Adding new types is easy - we just need a function to format the type
for display, verify the type, and possibly edit the type if it cannot be edited in-cell with a simple text string.
In fact, the programmer may effectively add a type by simply defining the appropriate handler functions (see below).   

Char columns support autocomplete.

An additional requirement is friction-free editing of column headers. Most of the time, if the ability to rename columns is
required, then using a menu or shortcut key and having a dialog box pop up is sufficient and desirable. However in some cases
it useful to be able to edit column headers just like regular cells. Related to this is the ability to have multiple row headers
and titles for header rows. 
 

## Implementation

We use the HTML table element. We investigated using just `<div>`s with CSS `display:grid`. Both solutions perform well in terms of scrolling speed, but the table solution had a slight edge. While tables are more complex, they are of course more semantic for the task at hand, though that may not be worth much 
considering that the datagrid is virtualized, and our primary platform is the desktop. More importantly, the structure of  `<table>`, `<thead>`, `<tbody>` etc., is quite useful and would have to be somewhat emulated if a pure `<div>` solution was used. The additional tags are not a deal breaker as we only
render what fits on the screen, plus a little overage. Finally, tables have better grid line and border support than `display:grid`.       
 
## Running the Tests ##

You will need projects Rumba and Provanto to run the grid and the tests. Rumba is not an official dependency of Abacus at this point in time.
To run the tests you then do:

~~~
      )CS #.Abacus
      Main.RunTests Tests.DataGridSuite1 Main.DataGrid
~~~ 
We are still working on some race or timing issues, so sometimes a test will fail for no apparent reason.
You can start the test application but not run the tests by giving a neg 1 left arg:

~~~
      ¯1 Main.RunTests Tests.DataGridSuite1 Main.DataGrid
~~~

You can then run tests one at time:

~~~
      Tests.DataGridQuite.TestCutAndPaste 0
0
~~~

Often a failing test will run fine like this.

## Properties

**User settable properties include:**

`Columns`: a vector of column specification namespaces, containing `Name`, `Type`, Value, etc. (See below)

`ReadOnly`: Boolean. Marks the entire Values area of the DataGrid as read-only. Defaults to `0`. This is the default value of not specified at the column level. 
 
`RowNumbers`: Boolean. Display row numbers or not. Default to `1`.

`InsertRows`: Boolean. Allow or disallow row insertion. If allowed, then rows may also be moved and deleted. Defaults to `1`.

`InsertColumns`: Boolean. Allow or Disallow column insertion. If allowed, then columns may also be moved, renamed, or deleted, unless otherwise
specified at the column level. Defaults to `0`.

`RowMinimum`: Minimum number of rows to display regardless of data size. Only applicable if InsertRows is 1. This just
gives nice grid lines when the grid is empty or very small. When deleting rows, a new empty row is appended if necessary
to keep the minimum 
 

`TopLeftCell`: The row and column index into Values of the upper left corner of the visible grid.

`ActiveCell`: The row and column index into Values of the current cell.

`WindowSize`: Number of full rows and columns visible. (Read-only)


## Column Specification Namespace

The `Columns` property is a vector of column specification namespaces, one for each column. 
    
The column specification namespace contains various properties, all of which default and may be omitted.
Most of the time the programmer will probably want to specify the column name, value,
type, and perhaps a format string here or there. Otherwise the defaults should generally suffice. 

The properties of the column specification namespace are:

**`Name`**: The column name. This defaults to spreadsheet-style column names A, B, C, etc. 

`Type`: The column type. Current supported
types are Char, VarChar, Int, Float, Date, Dec[1,2,3], Select, MultiSelect, and CheckBox. If the type is provided and  
the Value property is provided, they must correspond. If no type and no value is provided, the type defaults to VarChar.
If no type is provided but a Value property is provided, the type is inferred from the value.   

`Value`: The values in the column. Must all be the same length.

`HeaderValues`: Specifies column titles. This defaults to `Name`. For multi-row headers, may be a vector of vectors.

`HeaderRowTitles`: Specifies title or titles in the upper left corner. Defaults to empty/blank.  

`ReadOnly`: the column is read-only. Defaults to the value of the `ReadOnly` flag for whole grid. 

`CanDelete`: The column may be deleted. Defaults to the value of `InsertColumns`. 

`CanRename`: The column may be renamed. Defaults to the value of `InsertColumns`.

`Null`: A null value. For numerics, if a null value is in the domain of the column type, then the FormatString handles how it is displayed.
For example, the Date type uses 0 for null, and formats 0s as blank. 
If the null value is `⎕NULL` or `⍬` or some other value then it will automatically be displayed as blank or empty.
Null values are also used to replace deleted cell contents. For large data sets, try to keep the null value in the domain of the column.

`Default`: A default value for use when inserting a new row. This may or may not be the same as the null value. 

`List`: A list of character vectors for Select and MultiSelect types, and for Char columns that support autocomplete.
  
`FormatString`: A format string (left arg to `⎕FMT`) to be used by the `OnFormat` function. Applicable only to numeric values and dates. Usual use case is that a format string might be specified for Int and Float columns.

`FirstFormatString`: For the first visible row only.  

`OnFormat`: A function that formats the column for display in HTML. The default value uses the `FormatString` with `⎕FMT`, when appropriate, to format the value. The right argument provided to the function is the vector of column values to be formatted. The left argument is the column specification namespace.  This should rarely need to be specified, as 
setting `FormatString` should handle most cases. However, there may be times when complete control is desired.  

`OnParse`: A function that parses the text entered when editing a cell, and converts it to the appropriate data type.
This function takes a simple text string as its right argument, and the column specification namespace as its left argument.
It must return a 3-item vector containing a boolean to signify success (1) or failure (0), the parsed value, and an error message. Like `OnFormat`, this should rarely need to be specified. It may be needed if `OnFormat` is specified in such a way 
that the default parsing insufficient. If it is specified, there is the opportunity here to modify
the value, say removing all blanks, uppercasing, or moving a decimal place.    

`OnValidate` A function that provides additional validation to the `OnParse` function. This function takes the parsed result
as its right argument and the column specification namespace as its left argument, and then produces a result 
in the form as `OnParse`. This handler is designed more for common usage than `OnFormat` or `OnParse`. It is applied after OnParse is called, and we know that we have a valid type for the column. It allows for both validation and for possible
modification of the value (like `OnParse`), like uppercasing or scaling. 

## Column Types

Column types are fully defined by the `OnFormat`, `OnParse`, and `OnValidate` handler functions. This means that you can define new types by simply defining these functions. For example, we can make up a type named `RGB` which will be stored as a 3 item numeric vector of integers from 0 to 255 by defining:

~~~
OnFormatRGB←{
     {1↓,' ','ZI3'⎕FMT ⍵}¨⍵
 }

OnParseRGB←{
     b v←⎕VFI ⍵
     0=≢b:1 v''
     (v≡⌊v)∧(b≡3⍴1)∧∧/(v≥0)∧v≤255:1 v''
     0 0 'Value must be 3 integers from 0 to 255.'
 }
~~~

## Header Specification Namespace

The `Headers` property is a vector of of header specification namespaces,
corresponding to the number of rows in HeaderValues property. 

The properties of the header specification namespace are:

`Title`: A title for the header row. For a typical DataGrid with a one-row header, this is the value placed in the upper left corner of the grid,
above the row numbers. Header row titles will only display if `RowNumbers` is set to `1`.  Defaults to an empty vector.

`ReadOnly`: Indicates whether or not header row titles may be edited in-cell like regular values.
Default to `1`. This is independent of column renaming. It is
left up to the calling application to decide if editing a header row renames the column.   

`List`: A list of char vectors for autocomplete. Only applicable if ReadOnly is `0`.

## Methods

There is only one method: `Refresh`.

Properties are NOT covered by getters and setters, so the `Refresh` method must be run after one or more properties has been changed.

## Events

The DataGrid supports events. Event handlers may be attached to events:

~~~
      g.OnCellChange←'MyFoo'  
~~~

Events always fire and report the state of things after the event has taken place,
unless the event is named Before[event]. For example there is a `CellValueChange` event and
a `BeforeCellValueChange` event.  Note that events are events are explicitly NOT named in the past tense 
in an attempt to signify that they fire after the event has taken place.  

The left argument passed to the event handler is a reference
to the DataGrid. The right argument is the event message namespace. This namespace contains
the name of the event and other values of interest. In some cases there are no other values
of interest as the reference to the DataGrid itself has everything you need to know.

If the event is a "before" event
then the event handler may modify the event message (to a limited extent),
and thus alter aspects of the event that will take place. For example, on a `BeforeCellValueChange`
event, we may want to force the entered text to be uppercase, or have no spaces.
Furthermore, the result of a "before" event handler may return a `0` to let the event occur,
or a `1` to prevent the event. 

Events include:

`Refresh`: Any visible aspect of the DataGrid has changed. This could be editing a cell, scrolling, clicking to move the active cell, selecting cells,
renaming a column, inserting row etc. (We may want a way to throttle this event, or maybe not even implement it.)

`ActiveCellChange`: The current cell location has changed.
  
`Scroll`: The DataGrid has been scrolled in some way. The visible rows and columns have changed. The CellIndex property has changed.

`Resize`: The DataGrid has been resized.  

`CellValueChange`: The value of a cell (the Values property) or range of cells has been changed by in-cell editing or cut/copy/paste.

`BeforeCellValueChange`: A cell or range of cells is about to be changed by in-cell editing or cut/copy/paste.

`RenameColumn`: A column as been renamed. 

`BeforeRenameColumn`: A column is about to renamed.'

`InsertRow`: A new row has been inserted (or added by scrolling down below the last row).

`BeforeInsertRow:` A new row is about to be inserted.

`DeleteRow`: A row has been deleted.

`BeforeDeleteRow`: A row s about to be deleted.

`InsertColumn` A new column has been inserted.

`BeforeInsertColumn`: A new column is about to be inserted.

`DeleteColumn`: A column has been deleted.
 
`BeforeDeleteColumn`: A column is about to be deleted.

`BeforeHeaderValyeChange`:

`HeaderValueChange`:
  

