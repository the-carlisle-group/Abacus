# PromptBox New Method

Creates a new PromptBox: a dialog asking for a single value.

~~~
    R←{D} New X
~~~

`D` is an optional Document.
`X` is a namespace, or a shortcut list, of properties: see the PromptBox properties.
`R` is the new PromptBox.

The `Type` property selects the input component used: `Text`, `Date`, `File` or `Number`.
`Options` applies to `Text` only.

Display it with the [Show]() method. For the simple case use the HTMLDocument [Prompt]()
method, which combines `New` and `Show`.
