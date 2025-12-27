# The DataGrid Component

The DataGrid component implements a high-performance, virtual HTML table,
suitable for browsing and editing tables large and small.

## Getting Started

First, we must construct an array of [DataGridColumn]() objects that define
both the schema and the data. DataGridColumn objects are just plain namespaces
with some appropriate variables or properties. For example:

~~~
      c←⎕NS¨3⍴⊂''
      c.Name←'FirstName' 'LastName' 'DOB'
      c.Type←'VarChar' 'VarChar' 'Date'
      c.Value←(
                'Johann' 'Wolfgang' 'Ludvig'
                'Bach' 'Mozart' 'Beethoven'
                 19991231 20010101 2250101
                )
~~~

Once we have a collection of column objects,
we can create a new [DataGrid]() object, specifying the [Columns]() property: 

~~~
      g←A.DataGrid.New ⊂'Columns' c
~~~

> NB: When setting DataGrid properties after the creation of the grid, you must set them in the Table subspace, as in `g.Table.ReadOnly←1`. This is an accident of development, and might be temporary, and these properties moved to the root of the grid. 

We can try this out with:

~~~
      d←A.StartDesktopApplication A.NewDocument g
~~~

The `Columns` property is the only DataGrid property that must be supplied by the programmer.
All other properties have a default value.   

All of the DataGridColumn properties are optional, but either the [Type]() or [Value]() property
must be specified. If no types are defined, they are inferred from the values, and if no values
are supplied then they default to empty columns.  If both are supplied they must be in agreement.
It is good practive to explicilty define your types.

When resetting the `Columns` property, the [SetComponentValue]() method should be used:

~~~
      g A.SetComponentValue c
~~~

This sets the `Columns` property and reinitializes the grid.

## The ReadOnly Property

The [ReadOnly]() property fundamentally determines how the DataGrid operates,
and controls the applicabily of many other properties.
When ReadOnly is `0`, the grid supports in-cell editing, cut and paste,
inserting and deleting rows and columns, and moving rows and columns.

While these features are supported when ReadOnly is `0`,
they may be restricted by specifying other properties of the DataGrid
and DataGridColumn objects. For example with ReadOnly set to `0` and
[DeleteColumns]() set `0`,  you can have an editable grid
where the user cannot delete columns. 

All of these changes affect the [Columns]() property of the DataGrid,
and of course the `Value` property of the DataGridColumn objects that
compose it.

When ReadOnly is `1`, none of the above features are supported.
The user may not edit, cut, paste or delete, may not move, add or delete
rows or columns, etc.
However, the user may sort the grid, based on any column or set of columns,
may restrict the rows to be displayed, and may sort and restrict the columns
to be displayed. In other words users may change the view of the data
to suit their needs at the moment. 

None of these changes to the visible values affect the Columns property.

The [SetRowMask]() method allows you to specify the 
the rows to be viewed under program control. 
The [SetDisplayColumns]() method allows you to specify the order and
visibilty of the the columns.

## Column Types

The DataGrid comes with a set of built-in column types. These include:

### Char

Char values are provided, stored, and returned as a character matrix.
The [MaxLength]() property determines the maximum width of the matrix.
Char supports autocomplete functionality via the [List]() property. 


### VarChar

VarChar values are provided, stored and returned as a vector of vectors.
The [MaxLength]() property determines the maximum length of any value.
VarChar supports autocomplete functionality via the [List]() property. 

### Int

Integer values are provided as a simple vector. The [FormatString]()
property controls how the values are displayed. The default format string
is 'CI20.2'

### Dec1, Dec2, Dec3

Decimal values are provided as a simple integer vector with an implied decimal.
The [FormatString]()property controls how the values are displayed. The default
string for Dec3 is `F20.3`, and thus the value `6785` is displayed as `6.785`. 

### Float

Float values are provided as a simple vector. The [FormatString]() property
controls how the values are displayed.

### Date

Dates are stored as a simple vector of integers in the form of YYYYMMDD.

### CheckBox

Checkbox values are stored as a Boolean vector.

### Select

The select type provides a fixed list of choices, set by the [List]() property. 
Select columnvalues are stored as a character matrix.

## Validation

All types are handled by the browser in a basic text input element,
and conversion and validation is done in APL.
Additional validation may be specifiied via the `OnValidate` property. For example,
to specifiy that an integer column should only allow non-negative values,
we would create the following function:

~~~
     MyValidatation←{
              e←⍵<0
              e ⍵ 'Value must be non-negative.' 
     } 

~~~

And assign it to the OnValidate property:

~~~
      g.Table.OnValidate←A.FQP 'MyValidation'
~~~

> Note the use of `A.FQP` which adds the fully qualified path to the event handler

The right argument provided to the validation function is the value to be validated.

The left argument is the corresponding DataGridColumn object.
The DataGridColumn in turn gives access to all columns via its DataGrid property.
Thus validations can ensure things like this "the max of the sum of this column is 100."
In addition, the DataGridColumn object may be used to store any application specific
data needed for validation.

The result of the validate function contains the value that will actually be
used to update the grid. Usually this is just `⍵` passed through.
But this gives you the ability to transform the value in some way. For example,
to allow the user to only enter alphabetical characters, and to ensure uppercase:

~~~
      MyValidatation←{
               m←⎕C ⍵
               e←~∧m∊⎕A
               e m 'Only the letters A..Z accepted.' 
      }
~~~

Validation only applies to manual data entry after the grid has been created.
There is no validation of the column as a whole. The DataGrid expects
your DataGridColumn objects to be properly constructed.


## Custom Column Types

In most cases the built-in column types should suffice. However, column types are fully defined
by the [OnFormat](), [OnParse](), and optionally, the [OnValidate]() handler functions.
This means that you can define new types by simply defining these functions.
For example, we can make up a type named `RGB` which will be stored as a 3 item numeric vector of integers from 0 to 255 by defining:

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

## Events

The grid supports a set of events. For each event there is a corresponding 
property for specifying an event handler.
For example, an event handler may be specified for the [CellChange]() event like so:

~~~
       g.OnCellChange←A.FQP 'MyHandler'
~~~

The right argument provided to the event handler is an event message,
the left argument is a reference to the grid.
