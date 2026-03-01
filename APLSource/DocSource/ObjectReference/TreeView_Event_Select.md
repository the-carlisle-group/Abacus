# TreeView Select Event

The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:=========|:=====|
|Event     | 'Select`              |  
|Component | The TreeView instance |
|Document  | The associated document|

The assocaiated `OnSelect` property takes two parameters:

|Name      |Value|
|:=========|:=====|
|CallbackFunction   | The callback function |  
|DebounceDelay       | The debounce delay in milliseconds|
