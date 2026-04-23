# Enter

Enters a value on an input component in a test suite.

~~~
R←Enter X
~~~

`X` is a character vector. `R` is `0`. 

For a [TextInput](), `X` is a character string.

For a [NumericInput](), `X` is a numeric scalar.

For a [DateInput](), `X` is an integer in the form of `YYYYMMDD`.

For a [CheckBox](), this function the toggles the state. In this case, `X` is ignored.

For a [DropList]() or a [RadioGroup](), `X` is a character string that is one of the options.

In all cases, the `OnChange` callback function is fired, just as if a user entered
the data or selected the option.   

The global `Element` variable is an implicit argument.
