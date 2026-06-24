# Components

An Abacus component is an HTMLElement, some child elements, some CSS, and some
behavior. Components may be as simple as the [CheckBox](), or as complex as the [DataGrid]().

> Abacus components are not Web Components. There is no shadow DOM. 

## Creating Components

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

The `New` function will throw an error if an invalid property name
is supplied:

~~~
      CheckBox.New (Label:'Check here' ⋄ VaLue:1)
Invalid parameter name: VaLue
~~~

Component property names always start with an uppercase letter.
Only names that start with an uppercase letter are checked for validity.
Thus names that begin with a lowercase letter (HTML attributes) or an underscore
(a css style) may be provided to the `New` function and will not throw an error.
You can also create custom properties by prefixing their name with a `∆`:

~~~
      CheckBox.New(Label:'Check here' ⋄ Value:1 ⋄ ∆Val:1)
CheckBox
~~~

Once a component is created, you can stuff in anything you want:

~~~
      B←CheckBox.New(Label:'Check here' ⋄ Value:1 ⋄ ∆Val:1)
      B.MyOwnName←0
~~~

By inspection we see that the checkbox component is implemented as a div containing an
input and label. Each component has an eponymously named class associated with it.

Inline styles can be added to components, just like basic HTML elements:

~~~
     c._color←'yellow'
     A.Render c
<div onchange="sendAPLRequest(event)" class="CheckBox" style="color:yellow">
  <input checked="checked" id="MyCheckBox" type="checkbox"></input>         
  <label for="MyCheckBox">Check here</label>                                
</div>
~~~

## Names and Ids

The component's `Name` should be a valid APL identifier, and is accessible under the `Name`
property:

~~~
      c.Name
MyCheckBox 
~~~

The component's `Name` is strictly a part of the APLDOM, and plays no part
in the browswer DOM. It is not the same as the HTML `name` attribute (note the lower case), 
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

All components, like all elements in Abacus, must also have a unique `id` attribute.
Abacus will automatically generate a unique, meaningless, `id` if you do not provide one,
and in most cases that is sufficient.  It is sometimes useful, however, to assign
a meaningful `id` to a component.

## Finding Existing Components

The [GetComponent]() method takes any HTMLElement node and
finds a specific component by name:

~~~
   C←D A.GetComponent 'MyCheckBox'
~~~

The left argument may be the entire document, or some child node.
As component names do not need to be unique, it is up to the programmer
to know where to look for components in case duplicate names exist.
The `GetComponent` function will throw an error if the
name is not found, or if there are duplicate component names under the node.

The [GetComponents]() method returns the names and references to all
of the components below a specified node as a vector of name/value pairs:

~~~
      N R←↓⍉↑A.GetComponents D
~~~

With `⎕VSET` it is trivial to have a namespace of references:

~~~
      S←() ⎕VSET A.GetComponents D
~~~

which then allows, for example:

~~~
      S.MyCheckBox
~~~

## Getting and Setting Values  

Components usually have a `Value` property, which may be anything from a simple Boolean
to a large nested matrix. The `Value` property may be set when the component is created
using the `New` function, but more often than not values will be specified at
a later time. The `Value` property is simply a variable in the root element of the 
components, and may be retreived by simpy dotting into the component:

~~~
       MyCheckBox.Value
~~~

There is no `GetComponentValue` method neccessary.
However, to set it, we must use the [SetComponentValue]() setter function:

~~~
      C A.SetComponentValue V
~~~

where `C` is a component and `V` is a suitable value. If we have component name
in hand rather than a reference, we can still use `SetComponentValue`,
providing the document reference and the name on the left:

~~~
      D 'MyCheckBox' A.SetComponentValue 1
~~~

Multiple component values may be set in one go with the
[SetComponentValues]() function, providing either 
a list of name/value pairs:

~~~
      D A.SetComponentValues (`MyCheckBox1` 1) (`MyCheckBox2`) 
~~~

or a namespace:

~~~
      s←()
      s.MyCheckBox1←1
      s.MyCheckBox2←0
      D SetComponentValues s
~~~

## Events

Components may raise events. For each event, the component
will have a corresonding `On[Event]` property for 
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
