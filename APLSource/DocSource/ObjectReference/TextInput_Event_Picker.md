# TextInput Picker Event

The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:==========|:=====|
|Event     | `Picker`                                |  
|Component | The TextInput instance                  |
|Document  | The associated document                 |
|Value     | The current value                       |

If a callback is attached to this event, then
a button is provided that will execute the callback.
Typically this event is used to launch an aid of some
sort to set the value of text field.   
