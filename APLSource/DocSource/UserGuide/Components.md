# Components

An Abacus component is an HTMLElement, some child elements, some CSS, and some
behavior. Components may be as simple as the [CheckBox](), or as complex as the [DataGrid]().

> Abacus components are not Web Components. There is no shadow DOM. 

A component is implemented as a namespace, with a `New` function or method.
The left argument to `New` is an optional parent element and name.
Either parameter may be provided, or both. Let's create a checkbox component:

~~~
      c←'MyCheckBox' A.CheckBox.New 'Check here' ('Value' 1)
      A.Render c
<div onchange="sendAPLRequest(event)" class="CheckBox">            
  <input checked="checked" type="checkbox"></input>
  <label>Check here</label>
</div>
~~~

The right argument to `New` is a set of properties that may 
be specified by position or by name, and will vary by component.
The checkbox component takes a label, a value, and callback function
for handling changes.

By inspection we see that the checkbox component is implemented as a div containing an
input and label. Each component has an eponymously named class associated with it.

The name should be a valid APL indentifier, and is accessible under the `Name`
property:

~~~
      c.Name
MyCheckBox 
~~~

The component `Name` is strictly a part of the APLDOM, and plays no part
in the browswer DOM. It is not the same as the `name` HTML attribute, 
used when submitting forms, which generally does not play a role in Abacus.  
 
In a function (as oposed to the session),
if we do not specify a name in the left argument to `New`
then Abacus will assign a name by inspecting the left
side of the assignment arrow. That is:

~~~
      MyCheckBox←CheckBox.New 'Check here:'
~~~

is equivalent to:

~~~
     c←'MyCheckBox' CheckBox.New 'Click here:'
~~~

This leads to cleaner and more concise code. 

The component `Name` uniquely identifies the component within some document node.
Unlike the HTML `id` attribute, it does not need to be unique within the document as a whole.
All components must have a `Name`.

Components usually have a `Value` property, which may anything from a simple Boolean
to a large nested matrix.

....more here....  
   

Inline styles can be added to components, just like basic HTML elements:

~~~
     c._color←'yellow'
     A.Render c
<div onchange="sendAPLRequest(event)" class="CheckBox" style="color:yellow">
  <input checked="checked" id="MyCheckBox" type="checkbox"></input>         
  <label for="MyCheckBox">Check here</label>                                
</div>
~~~

## Events

Components may raise events. For each event, the component
will have a corresonding `On[Eventt]` property for 
specifying an event  callback function. For example, the DataGrid
component has a [BeforeCellChange]() event, and thus a corresponding
`OnBeforeCellChange` property. Only the event is documented.

The right argument provided to the event handler is a namespace containing
at least three items:

|Name      |Value|
|:==========|:=====|
|Event     | The event name, e.g. 'BeforeCellChange`|  
|Component | The component that fired the event     |
|Document  | The associated document                |

There will typically be more event-specific items in the event message space. 

If an event name begins with `Before`, then, depending on the specific event,
it may be altered or prevented. A callback function should return a 0 for normal
event processing, and a `1` to cancel the event. To the extent the specific 
event allows it, the event may be altered by having the callback function
reset certain veriables in the event message space. 




