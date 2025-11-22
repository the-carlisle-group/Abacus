# A Simple Application

Let's jump right in and create a very simple desktop application that keeps
track of the number of times a button is clicked. All of the concepts
will be exlained in further detail in subsequent chapters.

You can create a new namepace for the application, or just play around in the
root namespace. Whatever your location remember to execute `A←#.Abacus.Main`
So the Abacus functions can be located.

First we write a little function to build our document, which contains
nothing but a button and a paragraph element:

~~~
BuildClickCounter←{
       bn←A.New 'button' 'Click Me'
       bn.Onclick←A.FQP 'OnIncrement'
       bn._Count←0
       p←A.New 'p' 'Clicked 0 times'
       p.id←'click-status'
       A.NewDocument bn,p 
}
~~~

Note that we have assigned a callback function (also known as an event handler)
to the `onclick` event. Note also that we have made up a variable and stored it in the button itself
to track how many times it has been clicked. Both the name and location of this
variable are arbitrary.

Now we will need to implement the `OnIncrement` function:

~~~
OnIncrement←{
       ⍝ ⍵ Event Message
       d←⍵.Document
       b←⍵.Target
       b._Count+←1
       p←d A.GetElementById 'click-status' 
       p A.SetInnerHTML ⍕'Clicked' b._Count 'times'
}
~~~

Abacus provides callback functions a namespace with all of the information
needed to handle the event. The function implements the counter and updates the document. 

Finally we need to create an Application object to run the app:

~~~
      a←A.NewApplication '' 
      a.BuildFunction←A.FQP 'BuildClickCounter'
      d←a A.StartDesktopApplication ''
~~~

The final result `d` is the [HTMLDocument]() object created by our build function.
And on screen will be the assocated HTMLRenderer form with our application, ready for use. 

Try it out!

Here is all the above code in one contiguous block.
Simply copy this code into your APL session (version 20 or better!)
and hit the enter key:

~~~
A←#.Abacus.Main
BuildClickCounter←{
      bn←A.New 'button' 'Click Me'
      bn.Onclick←A.FQP 'OnIncrement'
      bn._Count←0
      p←A.New 'p' 'Clicked 0 times'
      p.id←'click-status'
      A.NewDocument bn,p 
}
OnIncrement←{
      d←⍵.Document
      b←⍵.Target
      b._Count+←1
      p←d A.GetElementById 'click-status' 
      p A.SetInnerHTML ⍕'Clicked' b._Count 'times'
}
      a←A.NewApplication '' 
      a.BuildFunction←A.FQP 'BuildClickCounter'
      d←a A.StartDesktopApplication ''
~~~
