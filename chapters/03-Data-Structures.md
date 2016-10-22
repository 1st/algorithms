# `03` Data structures

Programming language has simple data types, like `int`, `float`, `bool`, `string`.
Also it may contain more complex data types, like `list`, `tuple`, `dict`.

But when we solve our task - it's not very comfortable to work with these elementary data types.
We need something, to operate by more generic and complex data types.
For this purpose we can use data structures, that internally contains simple data types
*(or other composite data structures)*.
For example, we can have data strcutre to describe rectangle - we need to have heigh
and width to work with this object more comfortable. It's why we need data structures - to
make our final task more easy to understand and solve *(we don't need to remember all internals of
each complex data strucure)*.

In many cases we use `class` as a template for our data structure. But class also adds ability
to define operations that are possible to perform with the defined data structure. For example, if we
need to make our rectangle two times larger - we can manipulate by our internal heigh and width
in proper way. And user can be not aware about how does it works internally.
It looks like when you drive a car - you only press pedal of gas to go forward
*(and you don't care how does it work under the hood)*. The same in programming.
