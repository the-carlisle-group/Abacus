# DataGrid CellChange Event

The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:==========|:=====|
|Event     | 'BeforeCellChange`                      |  
|Component | The DataGrid instance                   |
|Document  | The associated document                 |
|ActiveCell| The ActiveCell                          |
|OldValue  | The current value of the cell           |
|NewValue  | The new value of of cell                |


The CellChange event is reported after a cell value changes
due to manually editing a single cell, or a set of cells changes
due to a cut/copy/paste operation.

This event may not be modified in any way.

This event is useful for logging or updating other parts of the UI
when the grid values change.
 
Use the [BeforeCellChange]() event to intercept the change before
it happens.
