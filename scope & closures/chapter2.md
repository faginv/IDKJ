# Chapter 2: Lexical Scope

* Lexical Scope: the scope model that JavaScript employs
* Dynamic Scope

Lexical scope is based on where variables and blocks of scope are authored (at lexing time).

Scope look-up stops once it finds the first match.

The lexical scope look-up process only applies to first-class identifiers.

### Cheating Lexical

##### eval
eval(..) is usually used to execute dynamically created code.
It can modify existing lexical scope.

setTimeout(..) and setInterval(..) can   take a string for their respective **first** argument, the contents of which are evaluated as the code of a dynamically-generated function. This is deprecated.

The new Function(..) function-constructor similarly takes a string of code in its **last** argument to turn into a dynamically-generated function. It should be avoided.

##### with
deprecated.
The with statement creates a whole new lexical scope.


[Scope & Closures, Chapter 1 What is Scope?](chapter1.md) < >
[Scope & Closures, Chapter 3 Function vs. Block Scope](chapter3.md)
