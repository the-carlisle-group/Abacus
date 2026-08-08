# Application BeforeClose Event

For a desktop application, this event occurs when a user
attempts to close the main form or quit the application.
This provides an opportunity to save state or confirm the action.
                                   
The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:==========|:=====|
|Event     | `BeforeClose`                           |  
|Component | The Application instance                |
|Document  | The Document instance                   |

If no callback is provided, the application is closed. 

If a callback function is provided, it must decide whether or not
to close the application. Closing the application
is done explicitly in the callback using the document [Close](HTMLDocument/Methods/Close) method.   

For a web application, this event occurrs when the connection is lost
or closed.  There is no way to prevent a web application from closing.
