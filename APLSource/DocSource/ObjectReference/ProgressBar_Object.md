# ProgressBar Object

## Description

A progress bar.

## Commentary

The ProgressBar object provides a modal form with a 
status message, and optional Cancel, Pause, and Truncate buttons.
In addition, if the number of iterations is known ahaad of time,
a progress bar is displayed.  
 
The ProgressBar object may be applied in two different ways or styles:
imperative and declarative. In addition, either style may have
a determinate or indeterminate number of iterations.

In both cases, the progress bar is created the same way.
In the imperative approach, you insert progress logic into
your code. In the declarative approach, you insert your
code into the progress logic.     

### Imperative Approach

The imperative approach uses the [Update]() method.
For example: 

~~~
   ...
   p←d A.ProgressBar.Create ⊂'Iterations' 10
   t←0
   :For I :in ⍳10
       r←p A.ProgressBar.Update 'Working on iteration',⍕I+1
       :If r≡'Cancel'
           :Return'
       :EndIf
       t+←⎕DL 1 
   :EndFor
   A.ProgressBar.Close p
   ...
~~~

In this case we iterate explicitly 10 times. The `Update` method is called
each time through the loop, setting the [Status]() property.
The result `r` may be inspected each time through the loop, to see
if the user canceled or truncated, and appropriate action taken.
The loop can of course be terminated for any reason whatsoever, regardless
of whether or not the user cancels. 

Finally, the progress bar must be explicitly closed with the [Close]() method


### Declarative Approach

The declarative appoach uses the [Run]() method (an APL operator).
In this case you must provide a function that will be executed on each
iteration. For example:

~~~
   ...
   f←{
      ⍵.Time+←⎕DL 1
      ⍺.Status←'Time: ',⍕t
      ⍺.Exit←t>5
      ⍵.Time
     }
   s←(Time:0)
   p←d ProgressBar.Create ''
   (c r)←p f ProgressBar.Run s
   ...
~~~

If the [Iterations]() property is greater than 0, 
the iteration function `f` will execute for a specific number of iterations
or until the [Exit]() property is set to `1`. Otherwise, if the `Iterations` property
is `0`, the function will execute indefinitely until `Exit` is set to `1`

The `Status` property is explicitly set each time the function executes.

The result `c` is either `'Resume'`, `'Cancel'`, or `'Truncate'`, indicating
that the task ran to completion, or was cancelled, or truncated.
The reult `r` is a vector of results of `f`, one item for each completed iteration.


  
