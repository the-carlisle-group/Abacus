# HTMLComponent Name Property

The `Name` property specifies the name of the component.

> NB: This is not the HTML `name` attribute.  

Unlike ids, `Name` does not need to be unique within the document.
However, the `Name` should be unique within some meaningful context.
For example, some dialog component might have a number of text input components
in it. These text inputs should all have different names. But you might
have multiple instances of the dialog component up at once, and thus the
document as a whole will have duplicate `Name` values, which is fine.  
