# Testing

Abacus provides a built-in UI testing framework. It is based on
[Provanto](https://github.com/the-carlisle-group/Provanto),
which must be present in the workspace.

An Abacus test suite is a namespace that contains a `Start` function,
one or more test functions, and optionally, a `Teardown` function.
Test function names begin with the string `Test`. Any significant
application will likely have additional application-specific utility
and convenience functions. 

The `Start` function builds the application and returns a document.
The `Teardown` function does any cleanup in addition to closing
the main application form, which is provided by the framework. 

Typically a test function will instigate some action in the HTMLRenderer
, like button click, and then examine the state of the APLDOM (the APL side)
and perhaps also some state in the HTMLRenderer.

The [RunTests]() function (in #.Abacus.Main) initializes and 
executes the test suite.

The initialization process injects several utility functions 
into the test space. These include:

|Function|Description|
|:======|:==================|
|[Click](FunctionReference/Click)|Click on an element|
|[Press](FunctionReference/Press)|Press a key on an element|
|[Enter](FunctionReference/Enter)|Enter a text string on an input element| 
|[GetElementById](FunctionReference/GetElementById)|Get an element from the APLDOM by id|
|[GetElementByName](FunctionReference/GetElementByName)|Get an element from the APLDOM by name|
|[GetElementFromBrowser](FunctionReference/GetElementFromBrowser)| Get an element from the browser by id| 

These functions are document-aware. 

The `SimpleApp` namespace in Abacus contains a simple application and associated
test suite in the subspace `Tests`. The start function simply starts the
application, returning the document:

~~~
Start←{
     ##.Run 0
 }
~~~

Often a `Start` function will need to more,
perhaps putting an app into a specific state, or even build small app from 
scratch to test a single component. 

To run the tests from within `SimpleApp.Tests`: 

~~~
      #.Abacus.Main.RunTests ⎕THIS
~~~

To intitialize the test suite so that tests may be run individually:

~~~
      ¯1 #.Abacus.Main.RunTests ⎕THIS
~~~

Now we may run and trace `Test1`:

~~~
      Test1 0 
~~~ 

Let's look at `Test1` in detail:  

~~~
Test1←{
     ⎕TID=0:∇&0
     b←GetElementById'increment'
     Assert b._Count=0:
     Click'increment':
     Assert b._Count=1:
     Click'increment':
     Click'increment':
     Assert b._Count=3:
     0
 }
~~~

It is useful, though not required, to start each test function with the idiom:

~~~
      ⎕TID=0:∇&0
~~~

This is because tests must be run in a thread, separate from the root.
The `RunTests` function threads test functions automatically, but if we want to 
run a single test independently it must be threaded.
If not, the system will hang. This idiom ensures that a test is not run
in the root thread.

The `GetElementById` function is test utitlity function, injected into the test
suite namespace by the test framework. It is document-aware, so it knows
what document to search. In addition to returning the element,
it creates a global variable in the test suite namespace named `Element`.
This is so subsequent calls to element-aware functions like `Press` know
what elements to operate on.  

The `Assert` function is provided by `Provanto`. An assertion is
followed by a naked guard. `Assert` returns a `0` if the condition is true,
else it signals an error, so it never returns a `1`, thus there is no 
reason to have anything after the guard.
You can always write your tests using trad functions it the naked guard bothers you. 

Next we run the `Click` function to dispatch a click event on the the element
whose id is `increment`. We could also write `Click b`.
The click function is document-aware, to if we pass an id as its right argument,
it knows what document to search. This function is also run to the left
of a naked guard. This is because in a dfn, every line must return a result,
and have an assignment (or the function terminates)
and we want to avoid superfluous assignments. Once the click is processed
we can assert that the counter has increased.

You can think of the naked guard as a required line-ending for any line
that does not have an assignment. You can of course avoid the guard
by either adding a throw-away assignment, or using a trad function.

Now lets look at `Test2`:

~~~
Test2←{
     ⎕TID=0:∇&0
     Click'increment':
     Click'increment':
     Click'increment':
     Assert ContentIs'Clicked 3 times':
     Click'increment':
     Click'increment':
     Assert ContentIs'Clicked 5 times':
     0
 }
~~~

This test makes use of an application-specific helper function:

~~~
ContentIs←{
     n←'click-status'
     se←GetElementById n
     ce←GetElementFromBrowser n
     ⍵ ⍵≡⊃¨(ce se).Content
}
~~~

Here we get the corresponding elements from APLDOM and from 
the HTMLRenderer, and check that the relevant content matches 
the argument. Functions like this make your tests much more readable and maintainable.
