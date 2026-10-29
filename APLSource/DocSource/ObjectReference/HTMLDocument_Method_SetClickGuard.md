# HTMLDocument SetClickGuard Method

Sets for how long a click is swallowed after the window comes to the front.

~~~
    R←I SetClickGuard N
~~~

`I` is an HTMLDocument instance. `N` is a number of milliseconds; `0` switches the guard
off. `R` is `0`.

A click on a window that is not at the front activates it, and Windows then passes the
click on to whatever sits under the mouse, which can set off a button or a grid cell
nobody meant to touch. Word and Excel swallow that click, and so does Abacus: while the
window is not at the front, and for 250 milliseconds after it comes back, a press is
taken away from the element under the mouse, and the click that follows it goes the
same way, however long the button is held. The window still comes to the front,
because that happens outside the browser.

Only the mouse is guarded, and of it `mousedown`, `click` and `dblclick`. The keyboard is
not, because a keystroke does not bring a window to the front.
