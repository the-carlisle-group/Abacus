# CSS

CSS is constructed in a similar way to HTML.
The [NewRule]() function creates a new [CSSRule] object for a selector:

~~~
     r1←A.NewRule 'h1'
     r2←A.NewRule 'h2,h3'
~~~

> NB: `A←#.Abacus.Main`

Declarations are made by simply assigning values to properties:

~~~
      r1.border←0
      r1.padding_top←'2rem'
      r2.font_size←'1.5rem'
~~~

Properties with dashes, illegal in APL names, should be specified with underscores.
Values may be numeric or text vector.

Rules are composed using the [ComposeRules]() function:

~~~
      A.ComposeRules r1 r2
h1 {                                                                            
    border: 0;                                                                  
    padding-top: 2rem;                                                          
}                                                                               

h2,h3 {                                                                         
    font-size: 1.5rem;                                                          
}                    
~~~

The result of `ComposeRules` is ready to be written to file or embedded in an HTML page.

Rules may be nested by providing the parent rule as a left argument to `NewRule`:

~~~
      pr←A.NewRule '@media print'
      r←pr A.NewRule 'p' 
      r.font_size←'10px'
      A.ComposeRules pr 
@media print {                                            

    p {                                                   
        font-size: 10px;                                  
    }                                                     
}

~~~

Child rules may also be directly assigned:

~~~
      pr←A.NewRule '@media screen'
      pr.Rules←r1 r2 r3
      A.ComposeRules pr 
@media screen {           
                          
    h1 {                  
        border: 0;        
        padding-top: 2rem;
    }                     
                          
    h2,h3 {               
        font-size: 1.5rem;
    }                     
                          
    p {                   
        border: 0;        
    }                     
}
~~~

A parent rule with an empty selector may be used as a collection of rules,
convenient for constructing a set of rules: 

~~~
CreateStyleSheet←{
     s←A.NewRule ''
     r←s A.NewRule 'p' 
     r.padding←'1em 2em' 
     r←s A.NewRule 'code'
     r.font_family←'APL385 Unicode'
     r.background_color←⍵.CodeBackgroundColor
     s
}
~~~

A style sheet may be embedded in an HTML document by specifying a `Style` property in the `html` element of the DOM.
The Style property may be specified as a string (usually the result of `ComposeRules`) or an array of rule objects.
The DOM2HTML function will compose the array of styles and create a style element under the head element when composing
the HTML:

~~~
     r1←A.NewRule 'p'
     r1.Border←0
     r2←A.NewRule 'Body'
     r2.padding←0
     d←A.New 'html'
     h←d A.New 'head'
     b←d A.New 'body'
     p←b A.New 'p' 'Hello world!'
     d.Style←r1 r2 
     A.DOM2HTML d
<!DOCTYPE html>        
<html>                 
  <head>               
    <style>            
      p {                    
          border: 0;         
      }                      
      body {                 
          padding: 0;        
      }                      
    </style>
  </head>    
  <body>               
    <p>Hello world!</p>
  </body>              
</html>
~~~
