# ListView New Method

Creates a new ListView component.

~~~
R←{P} New W
~~~

`P` is an optional parent element. `W` is a namespace (or shortcut list) of properties — see
the ListView properties. `R` is the new ListView.

## Examples

~~~
      lv←A.ListView.New(Items:'Apple' 'Pear' 'Plum')
~~~
