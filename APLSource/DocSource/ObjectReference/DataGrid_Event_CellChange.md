# DataGrid CellChange Event

The CellChange event is reported after a cell value changes
due to manually editing a single cell, or a set of cells changes
due to a cut/copy/paste operation.

This event may not be modified in any way.

This event is useful for logging or updating other parts of the UI
when the grid values change.
 
The event message space, provided as a right argument to the 
event handler function, includes CellIndex, OldValue, and NewValue.
       
Use the [BeforeCellChange]() event to intercept the change before
it happens.
 





