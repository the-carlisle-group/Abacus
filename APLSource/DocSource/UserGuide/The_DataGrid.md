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

All of DataGridColumn properties are optional, but either the [Type]() or [Value]() property
must be specified. If no types are defined, they are inferred from the values, and if no values
are supplied then they default to empty columns.  If both are supplied they must be in agreement.
It is good practive to explicilty define your types.



## Column Types

The DataGrid comes with a set of built-in column types. These include:

### Char

Char values are provided, stored, and returned as a character matrix.
The [MaxLength]() property determines the maximum width of the matrix.

**VarChar**  VarChar values are provided, stored and returned as a vector of vectors.
The [MaxLength]() property determines the maximum length of any value.

**Int** Integer values are provided as a simple vector. 

**Dec[X]**  Decimal values are provided as a simple vector.

**Float** Float values are provided as a simple vector.

**Date** Dates are stored as a simple vector of integers in the form of YYYYMMDD.

**CheckBox** Checkbox values are stored as a Boolean vector.

**Select** The select type provides a fixed list of choices, set by the [List]() property. 
Select values are stored as a character matrix.


Both Char and VarChar types support auto-complete, via the [List]() property. 




## Custom Column Types

In most cases the built-in column types should suffice. However, column types are fully defined
by the [OnFormat](), [OnParse](), and optionally, an [OnValidate]() handler functions.
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


