# PromptBox Object

## Description

Prompts the user for a simple string.

## Commentary

The prompt box provides a modal dialog box with a single input field
and an OK and Cancel button.

The HTMLDocument [Prompt]() method provides a shortcut to the prompt box component.

The prompt box does not wait in APL for the user to click OK or Cancel,
but relies on the [OnOk]() and [OnCancel]() methods to take action. 
Normally, the prompt box is called on the last line of a callback function.  
