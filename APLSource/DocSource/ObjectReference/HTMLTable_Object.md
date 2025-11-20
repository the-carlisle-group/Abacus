# HTMLTable Object

## Description

A `table` element with additional functionality.

## Commentary

The HTMLTable object provides functionality for creating and manipulating
HTML table elements. It is an HTMLElement object whose Tag property is `table`,
so all methods and properties that apply to HTMLElement apply also to HTMLTable.

Tables are created with the `NewTable` method:

~~~
      A.Render A.NewTable (2 3⍴⍕¨⍳12)
<table>         
  <tbody>       
    <tr>        
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>       
    <tr>        
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>       
  </tbody>      
</table>        
~~~
