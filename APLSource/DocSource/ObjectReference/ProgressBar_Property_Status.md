# ProgressBar Status Property

The `Status` property is a simple character vector that specifies the
status to be displayed on the progress form, or it is vector of simple character
vectors that specifies both the number of iterations and the status for each iteration.
This latter case is only applicable when using the [Run](method).  

For the imperative (looping) case,
the [Update]() method sets this property using the value of its right argument.
There is no need to set the property explicitly.      

For the declarative (functional) case, this property should 
be set by the iteration function
where it is used by the [Run]() method to update the progress bar status.
