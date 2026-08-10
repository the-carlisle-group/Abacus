# Panels New Method

Creates a new Panels component — a (optionally resizable) CSS-grid layout.

~~~
R←{P} New W
~~~

`P` is an optional parent element. `W` is a namespace (or shortcut list) of properties — see
the Panels properties. `R` is the new Panels.

## Examples

~~~
      pn←A.Panels.New(Content:(left right) ⋄ GridTemplateColumns:'1fr' '2fr' ⋄ Resizeable:1)
~~~
