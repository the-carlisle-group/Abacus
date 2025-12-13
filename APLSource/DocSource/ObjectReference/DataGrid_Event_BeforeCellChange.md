# DataGrid BeforeCellChange Event

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

The BeforeCellChange event is reported when a cell value
is about to change due to user editing, and provides an opportunity to 
reject the change, or modify the change in some way.

The result of the event handler should be 0 to accept the change,
1 to reject the change.

The `NewValue` property may be reassigned.

See also the [CellChange]() event.
