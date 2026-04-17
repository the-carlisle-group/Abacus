# RunTests

Runs a test suite.

~~~
R←[A [B]] RunTests T [C] 
~~~

`T` is a test suite namespace. `R` is an optional namespace for
computing code coverage.

`A` may be `¯1`, `0`, or `1`. A `¯1` indicates that the test suite
is only to be initialized. A `0` indicates the tests are to be executed.
without stopping. A `1` indicates that the tests are to be executed
with a stop on any failed or broken test. The default is `0`.

`B` may be `0`, `1` or `2`. A `0` (the default) indicates that
the execution should be as quiet as possible with respect to the session.
Higher values provide additional information.   
