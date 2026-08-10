# Tabs New Method

Creates a new Tabs component.

~~~
R←{P} New W
~~~

`P` is an optional parent element. `W` is a namespace (or shortcut list) of properties — see
the Tabs properties. `R` is the new Tabs.

## Examples

~~~
      t←A.Tabs.New(TabContent:(page1 page2) ⋄ Captions:'Overview' 'Details' ⋄ OnActivate:A.FQP'OnActivate')
~~~
