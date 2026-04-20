# GetElementFromBrowser

Returns an element from the browser in a test suite. 

~~~
R←GetElementFromBrowser X
~~~

`X` is an `id`. It may *not* be a `Name`. R is an element from the browser, as opposed
to the APLDOM. It is *not* a live reference to the element in the browser and must be retrieved
repeatedly to be up to date.

See also [GetElement]().
