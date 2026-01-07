# ConfirmBox Object

## Description

A modal confirmation box. 

## Commentary

The confirm box provides a modal confirmation box with multiple buttons. 

The HTMLDocument [Confirm]() method provides a shortcut to the confirm box component,

~~~
      r←d A.Confirm ''
~~~

The confirm box waits in APL for the user to select an option;
APL execution is suspended until the user clicks a button.
This in contrast to the [AlertBox](), [PromptBox](), and [DialogBox]()
elements, which rely on callbacks to take action.
