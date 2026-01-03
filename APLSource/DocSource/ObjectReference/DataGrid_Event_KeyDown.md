# DataGrid KeyDown Event

The event message supplied as the right argument to
the callback function contains:  

|Name      |Value|
|:==========|:=====|
|Event      | `'KeyDown'`                             |  
|Component  | The DataGrid instance                   |
|Document   | The associated document                 |
|Key        | Key value e.g. `'CtrlShiftF10'`         |

If a callback is assigned to this event, it is executed
before the default handling of the key by the DataGrid.

The callback function must return a `1` or `0`. If `1`, then
the DataGrid ignores the keypress as it is assumed to be
handled by the callback. If the result is `0`, then the keypress
is handled in the normal way.

> The event does not fire if the user is in the process of editing a cell. 
