# Components

An Abacus component is an HTMLElement, some child elements, some CSS, and some
behavior. Components may be as simple as the [CheckBox](), or as complex as the [DataGrid]().

> Abacus components are not Web Components. There is no shadow DOM. 

A component is implemented as a namespace. Lets's examine the code
in the `NumberInput` component.

First, every component must have a `New` function:

~~~
 New←{
     ⍺←0
     d←(⍺ A.New'div')⎕NS(
         'Name' ''
         'Label' ''
         'Value' 0
         'Format' 'I10'
         'OnChange' ''
     )A.Default ⍵
     _←d.⎕DF 'NumberInput'
     d.class←'NumberInput'
     g.Class←⎕THIS
     l←d A.New'label'd.Label
     l.for←d.Name
     i←d A.New'input'
     i.id←p.Name
     d.Onchange←A.FQP'OnChange'
     _←d InitValue d.Value
     d
 }
~~~

The left argument to `New` is an optional parent element.
The right argument is an array of property names and values (similar to `⎕WC`),
or a namespace. However they are supplied, the property names and values are injected into
the root element of the component, `d` in this case. By inspection, we can see
the properties and default values of this component. All components begin this way.

Propeteries are simple variables. There are no getter and setter functions, so
sometimes initializion or refresh functions are provided. 

The `Name` property uniquely identifies the component within some document node.
Unlike the HTML `id` attribute, it does not need to be unique within the document as a whole.
All components must have a `Name` property. This component has 3 additional
properties: `Label`, `Value`, and `Format`.

The `NumberInput` component is a `<div>` containing a `<label>` and an `<input>`.
We capture the JavaScript `change` event, and call `OnChange` back in APL: 

~~~
OnChange←{
     d←⍵.CurrentTarget
     v←Parse ⍵.Value
     f←d.Format Format v
     _←d SetValue Parse f
     ⍵ A.Execute'OnChange'
 }
~~~

The right argument to OnChange, provided by Abacus, inludes a wealth of information from the browser.
The `CurrentTarget` is the component itself, and the `Value` property is the value from the `<input>` element.
We defined the <input> element as type=text, so we convert the text into a number using `Parse`   

In addition to properites and methods, components may expose events. 
The NumberInput component exposes a [Change]() event, with an implied 'OnChange' 
property.  After the built-in OnChange function does what it needs to do,
it calls the user-supplied event handler for the change event. This function is  
supplied an event message as its right argument, and the object instance
as its left argument.  


The `Parse` and `Format` functions are fairly trivial:

~~~
Parse←{
     ⊃1⊃⎕VFI ⍵/⍨⍵∊⎕D,'.'
 }

 Format←{
     ' '~⍨,⍺ ⎕FMT ⍵
 }
~~~

Finally, we have a `CSS` function to provide component-specific CSS:

~~~
CSS←{
     Rule←A.NewRule
     ⍝ ************************
     s←Rule'.NumberInput'
     s.display←'flex'
     s.flex_direction←'column'
     s.gap←'.5rem'
     ⍝ ************************
     r←s Rule'input'
     r.text_align←'right'
     ⍝ ************************
     A.UnNestCSS s
 }
~~~
