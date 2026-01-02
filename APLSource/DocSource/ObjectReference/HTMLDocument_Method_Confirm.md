# HTMLDocument Confirm Method

Displays a confirmation box and waits for a response.

~~~
R←I Confirm [T [M [B]]]
~~~

`I` is an HTMLDocument instance.
`T` is the title, a character vector. It defaults to "Confirm".
`M` is the message, character vector or list. It defaults to "Continue?"
`B` is a list of button captions. It defaults to `'Yes'` `'No'`.
R is the button caption of the selected option, or an empty vector if
Escape is pressed.  
