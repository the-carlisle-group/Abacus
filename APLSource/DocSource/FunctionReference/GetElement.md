# GetElement

Returns an element from the document in a test-suite.

~~~
R←GetElement X
~~~

`X` is an `id` or `Name`. `R` is the corresponding element
from the global `Document` variable in a test suite.

Note that this function does *not* set the global `Element` variable
like [Focus]() or [On]().

See also [GetElementFromBrowser]().
