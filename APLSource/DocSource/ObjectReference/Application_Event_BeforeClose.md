# Application BeforeClose Event

For a desktop application, this event occurs
after a user attempts to close the main form or quit the application.
This provides an opportunity to save state or confirm the action.

For a web application, this event occurrs when the connection is lost
or closed.

The left argument to the callback function is the application instance.
The right argument is an event message containing
a reference to the document,

For a desktop application, the result should be set to `0` to proceed with the 
close as requested, or `1` to not close.

There is no way to prevent a web application from closing.
