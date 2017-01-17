# Chapter 4: Hoisting

``` JavaScript
var a = 2;
```

JavaScript thinks of it as two statements: ``var a;`` and  ``a = 2;``

The declaation is processed during the compilation phase.
The assignment is left in place for the execution pahse.

Function declarations are hoisted. But function expressions are not.

Functions are hoisted first, and then variables.

Multiple/duplicate function declarations do override previous ones.

it's best to avoid declaring functions in blocks.

[Scope & Closures, Chapter 3 Function vs. Block Scope](chapter3.md) < >
[Scope & Closures, Chapter 5 Scope Closure](chapter5.md)
