# DataGridColumn FormatString Property

Specifies the `⎕FMT` style format string for numeric columns including types
Int, Float, Dec1, Dec2, Dec3, and Date.

The default format string for each applicable type is:

|Type |Format String|
|:====|:============|
|Int  |`LCI20`      |
|Dec1 |`LK¯1F20.1`  |
|Dec2 |`LK¯2F20.2`  |
|Dec3:|`LK¯3F20.3`  |
|Float|             |
|Date |`BG<9999/99/99>`|

`⎕FMT` produces a matrix, on which the DataGrid then
does a *no-trailing-blank* split on.

The `L` qualifier should be used when `I` or `F` is used,
to left justify (this facilitates stripping extraneous blanks),
as justification is handled by CSS.

The width of the format strings for `I` and `F` formats
should be specified large enough to accomodate the data.
This may be overestimated without ill effect, as
extraneous blanks are removed.  

An empty string (the default for Float) is formatted with: 

~~~
      {⎕PP←16 ⋄ ~∘' '¨↓⍕⍪⍵}
~~~
