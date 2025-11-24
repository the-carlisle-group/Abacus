# HTMLTable NewTable Method

Creates a new HTML table element.

~~~
R←Render B [H [F]]
~~~

`B` is a matrix of body values.
`H` is a optional matrix of header values. 
`F` is an optional matrix of footer values.
`R` is an HTMLElement object with tag 'table'.

Vectors are taken to be one-row matrices.

## Examples

~~~
      A.NewTable (⍕¨3 2⍴⍳6) ('ColOne' 'ColTwo')
HTMLElement
      A.Render A.NewTable (⍕¨3 2⍴⍳6) ('ColOne' 'ColTwo')
<table>              
  <thead>            
    <tr>             
      <th>ColOne</th>
      <th>ColTwo</th>
    </tr>            
  </thead>           
  <tbody>            
    <tr>             
      <td>0</td>     
      <td>1</td>     
    </tr>            
    <tr>             
      <td>2</td>     
      <td>3</td>     
    </tr>            
    <tr>             
      <td>4</td>     
      <td>5</td>     
    </tr>            
  </tbody>           
</table>             
~~~
