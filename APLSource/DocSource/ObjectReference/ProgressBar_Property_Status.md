# ProgressBar Status Property

The `Status` property is a simple character vector that specifies the
status, usually set on each iteration. 

For the imperative (looping) case,
the [Update]() method sets this property using the value of its right argument.
There is no need to set the property explicitly.      

For the declarative (functional) case, this property should 
be set by the iteration function
where it is used by the [Run]() method to update the progress bar status.
