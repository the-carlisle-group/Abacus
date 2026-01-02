# AlertBox Object

## Description

A modal message box.

## Commentary

The alert box provides a modal message box with a single OK button.
You may specify the title of the box as well as a message.  

The HTMLDocument [Alert]() method provides a shortcut to the alert component,
allowing you to specify only the message (the title will default to 'Alert');

~~~
      d A.Alert 'File saved.'
~~~

The alert box does not wait in APL for the user to click OK.
Normally, the alert box is called on the last line of a callback function.  
