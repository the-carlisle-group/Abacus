# Focus

Sets the focused or current element in a test suite.
This function is instantiated in the test suite by [RunTests]().

~~~
R←Focus X
~~~

`X` is the `id` or `Name` of the element. `R` is `0`.

This function sets a global variable in the test-suite namespace named,
`Element` for subsequent use by [Press](), [Enter](), or other
functions.
 
The focused element may or may not have the actual focus in the browser.
