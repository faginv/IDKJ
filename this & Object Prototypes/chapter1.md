# Chapter 1: `this` or That?

`this` is a special identifier keyword that's automatically defined in the scope of every function.

`this` is neither a reference to the function itself, nor is it a reference to the function's lexical scope.

When a function is invoked, an execution context is created. It contains information about where the function was called from the call-stack, how the function was invoked, what parameters were passed, etc. One of the properties of this record is the `this` reference. `this` will be used for the duration of that function's execution.

`this` is a binding that is made when a function is invoked. What it references is determined by the call-site where the function is called.
