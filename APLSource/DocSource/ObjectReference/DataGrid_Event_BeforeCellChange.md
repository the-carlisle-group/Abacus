# DataGrid BeforeCellChange Event

The BeforeCellChange event is reported when cell value
is about to change, and provides an opportunity to 
reject the change, or modify the change in some way.

The event message space, provided as a right argument to the 
event handler function, includes CellIndex, OldValue, and NewValue.

The result of the event handler should be 0 to accept the change,
1 to reject the change.

The `NewValue` property may be modified.

See also the [CellChange]() event.
