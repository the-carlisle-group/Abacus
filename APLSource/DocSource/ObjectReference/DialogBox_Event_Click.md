# DialogBox Click Event

The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:==========|:=====|
|Event     | `'Click'`                               |  
|Component | The DialogBox instance                  |
|Document  | The associated document                 |
|Button    | The button HTMLElement clicked          |
|ButtonCaption| The button caption                   |

The `Click` event is fired when a button is clicked.

The `OnClick` property may specify one callback for all buttons,
or a different callback for each button.

The result of callbacks attached to this evcent must return a `0` or a `1`.
A `0` indicates that the dialog box should be closed, a `1` indicates
it should remain open.

If no callback function is specified, the dialog box is closed.
