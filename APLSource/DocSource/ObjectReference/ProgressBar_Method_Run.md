# ProgressBar Run Method

Runs a function under a progress bar.

~~~
(C R)←I F Run S
~~~

`Run` is an operator.
`I` is a progress bar instance.
`F` is a function to be executed on each iteration.
`S` is an appropriate right argument to `F`. 

`I` is passed as a left argument to `F`.
This allow `F` to update the [Status]() property,
inquire about the current [Iteration]() number,
specify when to [Exit](), etc.

`C` is a return code of either `"Resume"`, '"Cancel"', or '"Truncate"`.
This is the same set of values as the result of the [Update]() method.
A value of `'Resume'` indicates all iterations completed. 

`R` is an array of the explicit results of `F`, one for each completed iteration.
