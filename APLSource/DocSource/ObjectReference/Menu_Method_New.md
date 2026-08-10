# Menu New Method

Creates a new Menu — a `<menu>` element. With no parent it is a top-level menu (the root of
a context menu); given a parent menu it is a submenu of that menu.

~~~
R←{P} New W
~~~

`P` is an optional parent menu. If omitted, the result is a top-level menu; if a parent menu
is given, the result is a submenu of it. `W` is a namespace (or shortcut list) of properties
— see the Menu properties. `R` is the new Menu.

## Examples

~~~
      m←A.Menu.New''                   ⍝ root menu (e.g. for a context menu)
      sub←m A.Menu.New(Label:'File')   ⍝ a submenu of m
~~~
