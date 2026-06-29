# DataGridColumn Highlight Property

The `Highlight` property is an integer vector corresponding
to the [Value]() property, indicating that the cell value should be
highlighted in some way. A zero indicates no highlight,
and 1, 2, and 3 offer built-in colors:

|Value|Highlight|
|:====|:========|
|0    |None     |
|1    |Green    |
|2    |Yellow   |
|3    |Red      |

You can set to any integer value over 3 and provide
your own class named `highlightN`, where N is the integer value. 

The `Highlight` property is only applicable if [ReadOnly]() is `1`. 
