# MenuItem Click Event

The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:==========|:=====|
|Event     | `Click`                                 |  
|Component | The MenuItem instance                   |
|Menu      | The root menu instance                  |
|Anchor    | The menu anchor element                 |
|Document  | The associated document                 |

When the menu is instantiated as a context menu,
the `Menu` property in the event message is the *root* menu,
which will give you access to any user-defined values
which may be stored there. The `Menu` property is generally not
applicable to menubars, hamburger menus ,and dropdown menus. 
