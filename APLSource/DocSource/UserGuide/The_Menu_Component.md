# The Menu Component

The [Menu]() component supports creating context (or popup) menus,
menu bars, hamburger menus, and dropdown menus. 

## Menubars and Hamburger Menus 

Menubars and hamburger menus use the same structure:
all of the top level items are submenus. Let's look
at a simple example: 

~~~
   BuildMenu←{
        M←A.Menu
        m←M.New''
        File←m M.New 'File'  
        _←File M.NewItem 'Open'
        _←File M.NewItem 'Save'
        Edit←m M.New 'Edit'  
        _←Edit M.NewItem 'Cut'
        _←Edit M.NewItem 'Copy'
        _←Edit M.NewItem 'Paste'
        m
   }
~~~

We will be calling functions repeatedly from `#.Abacus.Main.Menu`
which we assign to `M` for convenience.

We start be creating a parentless toplevel menu object `m`,
using the `New` function. 
We then create a `File` menu under it, again using the `New`
function, this time with a parent `File`.
Then, under the `File` submenu, we create two menu items using
the `NewItem` function. 

The `BuildMenu` function then returns the main menu component `m`.
Menu creation must be encapsulated in a function that returns 
the menu component.

To add a menubar which will display the menu to the document:   

~~~
     mb←p M.NewMenuBar 'BuildMenu'
~~~

Where `p` is the parent (often a <header> element) and
the right argument is the name of the function that builds
and returns the menu component. 
This returns a new menu element (not a component)
whose class is `MenuBar`.

To add a hamburger menu button which will display the menu:

~~~
     hm←p M.NewHamburgerMenu 'BuildMenu'
~~~

This returns a new button element whose class is `HamburgerMenu`.

## Dropdown Menus

A dropdown menu may be be created in a similar way. Usually
placed in a toolbar, these are traditionally composed of a simple list of menu items
with no submenus:

~~~
 BuildMenu←{
        M←A.Menu
        m←M.New'My drop down'
        _←m M.NewItem 'Do this'
        _←m M.NewItem 'Do that'
        _←m M.NewItem 'Do the other'
        m
   }
~~~

And then added to the document: 

~~~
       dm←p M.NewDropDown 'BuildMenu'
~~~

## Context Menus

A context menu is created and displayed in your own callback function,
usually attached to the `onContextMenu` event.
A context menu is usually associated with another element
called the anchor element, and the menu is displayed near the anchor.

The menu is constructed just as it is above for 
a menu bar or hamburger menu, but is not required to be
encapsulated in a function, though it is good practice to do so.
In addition, a context menu will often have menu items in addition to 
submenus in the root, where a menubar root must consist only of submenus. 
In your callback, the menu is created and displayed using
the `ShowContextMenu` function:                           

~~~
     m←BuildMenu 0
     m M.ShowContextMenu a
~~~

If a zero is supplied rather than an anchor element, then the 
popup menu is displayed in the center of the screen.
