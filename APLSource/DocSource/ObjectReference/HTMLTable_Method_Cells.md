# HTMLTable Cells Property

The Cells property returns a matrix of the `<td>` elements in the table.
Is it currently implemented as a function:

~~~
      t←A.NewTable 2 3⍴⍕¨⍳12
      A.Cells t
 HTMLElement  HTMLElement  HTMLElement 
 HTMLElement  HTMLElement  HTMLElement 
       (A.Cells t).Tag
 td  td  td 
 td  td  td 
      (A.Cells t).Content
  0    1    2  
  3    4    5  
~~~
