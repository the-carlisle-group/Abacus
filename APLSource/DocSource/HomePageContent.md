> Take care of the code, be gentle to the computer, and make beautiful stuff on your screens. -- Håkon Wium Lie 


> We make software the old-fashioned way, we write it.

# Abacus UI

> November 23, 2025: This site is under construction. We have done just enough CSS to make it not entirely heinous. The architecture is minimal. We are focused on adding content, and will return to the looks and functionality in the future. 

Abacus UI is a Dyalog APL framework for building desktop
and web applications under the browser. It aims to solve a seemingly
intractable problem: how to move beyond the venerable Dyalog `⎕WC` 
interface and take advantage of the web browser and all that it offers.

## HTML

At the heart of Abacus is the APL document object model or APLDOM.
The APLDOM provides an easy way to construct and manipulate HMTL documents and fragments.
(No more string catenation!) An APLDOM document may be a standalone object, or synchronized with an 
HTMLRenderer instance, or even a remote browser on a client machine. 

## CSS

Similar to the APLDOM, Abacus provides a CSS object model making it simple to construct
and manipulate CSS in code.  

## Component Library

Abacus comes with a component library. These are carefully crafted objects built with APLDOM
elements that encapsulate HMTL and CSS, covering everything from a simple text input to a high performance DataGrid. 

## Markdown

Abacus has a built-in Markdown to APLDOM (and thus HTML) converter.

## Testing

Abacus has a built-in UI and backend testing framework.
Tests are written in APL and executed in the workspace. This allows for a very
tight code-test-debug loop, all in the comforting confines of the APL session.

## Only APL and the Browser

Abacus uses no third party Javascript frameworks or tools. None, nada, zero, zilch.
Just APL and the browser.
