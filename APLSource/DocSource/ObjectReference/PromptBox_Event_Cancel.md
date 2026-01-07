# PromptBox Cancel Event


The event message space supplied as a right argument
to the callback function contains:

|Name      |Value|
|:==========|:=====|
|Event     | `'Cancel'`                              |  
|Component | The PromptBox instance                  |
|Document  | The associated document                 |

The result of the callback function must return a `0` or a `1`.
A `0` indicates that the PrompBox should be closed, a `1` indicates
it should remain open.

If no callback function is specified, the PromptBox is closed.
