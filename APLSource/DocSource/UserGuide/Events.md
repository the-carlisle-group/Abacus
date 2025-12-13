# Events

JavaScript events may be intercepted and reported
back to APL by specifying the `On[event]` property of an element.
For example, to capture the `click` event of a button:

~~~
      b←A.New 'button'
      b.Onclick←A.FQP 'MyCallBack'
~~~

This will execute the 'MyCallBack' function back in APL when the user clicks the button.

The right argument provided to the callback function is
the *event message namespace*, which contains
all of the necessary information to handle the event.
Not all values are applicable to all events.
 
The event message space contains:

|Name            |Value     |
|:============== |:=========|
|Event           |The event name e.g.: 'click'         |
|Document        |The document            |
|CurrentTarget   |The element to which the callback is attached|
|Target          |The element that reported the event|
|Value           |The *value* attribute of the target element| 
|Name            |The *name* attribute of the target element| 
|Key             |The key value, e.g. 'Enter' |
|CtrlKey         |Ctrl key state (Boolean)|
|AltKey          |Alt key state (Boolean) |
|ShiftKey        |Shift key state (Boolean|
|MouseButton     |The button property     |
|MouseButtons    |The buttons property    |

Abacus [components]() may also raise events.
These have event message spaces particular to each component,
but always include Event, Document, and Component, a reference to 
the component that raised the event.      


## Case Sensitivity

Note well the case sensitivity when specifying `Onclick`: the upper case `O` in `On`, while the JavaScript event
name `click` is all lower case. If we were to write:

~~~
      b.onclick←'some string'
~~~

we would be specifying an HTML attribute, and be delegating everything to the browser, which would expect
'some string` to be `JavaScript` to be executed.

Futhermore components will often have events that begin with an upper case letter,
like `Click`, in which case the callback is specified as:   

~~~
     b.OnClick←A.FQP 'MyCallBack'
~~~

Again, note the case sensitivity. 
