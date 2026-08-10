# Flex New Method

Creates a new Flex component — a flexbox container.

~~~
R←{P} New W
~~~

`P` is an optional parent element. `W` is a namespace (or shortcut list) of properties — see
the Flex properties. `R` is the new Flex.

## Examples

~~~
      f←A.Flex.New(Content:(a b c))
      f←A.Flex.New(Content:(a b) ⋄ _gap:'1rem' ⋄ _align_items:'center')
~~~
