# ConfirmBox Object

## Description

A modal confirmation box. 

## Commentary

The confirm box provides a modal confirmation box with multiple buttons. 


   cb←A.ConfirmBox.New '
      d Show

The HTMLDocument [Confirm]() method provides a shortcut to the confirm box component,

~~~
      r←d A.Confirm ''
~~~

The confirm box waits in APL for the user to select an option.  
