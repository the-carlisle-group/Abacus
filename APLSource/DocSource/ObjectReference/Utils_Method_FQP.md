# Utils FQP Method

Returns the fully qualified name of a callback, which is what the event properties expect.

~~~
    R←{L} FQP Name
~~~

`Name` is the name of the callback function.
`L` is an optional number of levels up the calling stack, 0 by default, meaning the caller itself.
`R` is `Name` qualified with that namespace. A name already starting with `#` is returned unchanged.

## Examples

~~~
      b←A.Button.New(Caption:'Find' ⋄ OnClick:A.Utils.FQP'OnFind')
~~~
