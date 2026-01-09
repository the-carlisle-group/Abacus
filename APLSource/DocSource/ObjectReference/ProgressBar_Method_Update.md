# ProgressBar Update Method

Updates the progress bar.

~~~
R←I Update X
~~~

`I` is the progres bar instance. `X` is a status message, a simple string.
`R` is `"Resume"`, `"Cancel"`, or `"Truncate"`.

This method increments the [Iteration]() property and sets the [Status]() property.
