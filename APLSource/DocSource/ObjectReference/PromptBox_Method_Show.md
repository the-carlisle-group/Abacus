# PromptBox Show Method

Displays a prompt box.

~~~
   R←I PromptBox.Show ''
~~~

or

~~~
   R←PromptBox.Show I
~~~

`I` is the PromptBox instance. `R` is '0'.

This method does not wait, and generally should be the last line of a callback,
with no following code. All action must be handled in the [OnOk]() and [OnCancel]() callback
functions.

See the HTMLDocument [Prompt]() method for easiest use of the AlertBox,
encapsulating the `New` and `Show` methods.
