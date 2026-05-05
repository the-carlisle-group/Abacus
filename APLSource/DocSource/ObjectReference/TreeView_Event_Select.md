# TreeView Select Event

The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:=========|:=====|
|Event     | `Select`               |  
|Component | The TreeView instance  |
|Document  | The associated document|

The associated `OnSelect` property takes two parameters:

|Name      |Value|
|:=========|:=====|
|CallbackFunction   | The callback function |  
|DebounceDelay      | The debounce delay in milliseconds|

The `Select` event is fired on a mouse click or keyboard navigation.
Only keyboard events are debounced.
The [ActiveItem]() property reports the the current item index.
