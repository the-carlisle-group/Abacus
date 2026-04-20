# Testing

Abacus provides a UI testing framework built on top of
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

Typically a test function will instigate some action in the HTMLRenderer,
like button click, and then examine the state of the APLDOM (the APL side)
and perhaps also some state in the HTMLRenderer.

The [RunTests]() function (in #.Abacus.Main) initializes and 
executes the test suite. It establishes two global variables in the test suite
namespace: `Document`, which remains unchanged, and `Element` which specifies
the current, focused element. `Element` is initially set to `Document` 

The initialization process injects several utility functions 
into the test space. These include:

|Function|Description|
|:======|:==================|
|[Focus](FunctionReference/Focus)|Focus on a partiular element by `id` or `Name`|
|[Click](FunctionReference/Click)|Focus and click on an element by `id` or `Name`|
|[Press](FunctionReference/Press)|Press a key on an the focused element|
|[Enter](FunctionReference/Enter)|Enter a text string on an the focused element| 
|[On](FunctionReference/Enter)|Specfies the focused element for in-lining with `Press` and `Enter`)
|[GetElement](FunctionReference/GetElementFromBrowser)| Get an element from the APLDOM| 
|[GetElementFromBrowser](FunctionReference/GetElementFromBrowser)| Get an element from the browser by id| 

These functions are document-aware. Tests can of course use any function in Abacus as well. 

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
     Click'Reset':
     Assert Document._Count=0:
     Click'Increment':
     Assert Document._Count=1:
     Click'Increment':
     Click'Increment':
     Assert Document._Count=3:
     0
 }
~~~

It is useful, though not required, to start each test function with the idiom:

~~~
      ⎕TID=0:∇&0
~~~

This is because tests must be run in a thread, separate from the root.
The `RunTests` function threads test functions automatically, but if we want to 
run a single test independently it must be threaded or the system will hang.
This idiom ensures that a test is not run
in the root thread.

The `Click` function is injected into the test
suite namespace by the test framework. As the name implies, it fires a click
on an element. It is document-aware, so it knows
what document to search for either an `id` or a `Name`.
The result of `Click` is always `0`, and since we are in using a dfn, we must
either assign it, or use the naked guard to continue execution.
You can of course use a trad function to avoid both the superfluous
assingment and the naked guard.

The `Document` reference is avaiable globally in the test suite namespace,
for easy access and verifying state.

The `Assert` function is provided by `Provanto`. An assertion is also
followed by a naked guard for the same reason as above.
`Assert` returns a `0` if the condition is true, else it signals an error.

Now lets look at `Test2`:

~~~
Test2←{
     ⎕TID=0:∇&0
     Click'Reset':
     Click'Increment':
     Click'Increment':
     Click'Increment':
     Assert ContentIs'Counter value is 3':
     Click'Increment':
     Click'Increment':
     Assert ContentIs'Counter value is 5':
     0
 }
~~~

This test makes use of an application-specific helper function:

~~~
ContentIs←{
     n←'click-status'
     se←GetElement n
     ce←GetElementFromBrowser n
     ⍵ ⍵≡⊃¨(ce se).Content
 }
~~~

Here we get the corresponding elements from APLDOM and from 
the HTMLRenderer, and check that the relevant content matches 
the argument. Functions like this make your tests much more readable and maintainable.
