# Chapter 1: What is Scope?

Where are variables stored?
How does a program find them when it needs them?

Scope: a well-defined set of rules for storing variables in some location and finding those variables at a later time.

## Compiler Theory

JavaScript is a compiled language.

compilation 3 stemps:

1. Tokenizing/Lexing:
2. Parsing:
3. Code-Generation:

Any snippet of JavaScript has to be compiled just before it's executed.

## Understanding Scope

1. Engine: responsible for start-to-finish compilation and execution of our JavaScript program.
2. Compiler: handles all parsing and code-generation.
3. Scope: collects and maintains a look-up list of all the declared identifiers (variables), and enforces a strict set of rules as to how these are accessible to currently executing code.

##### To distict actions are taken for a variable assignment:
1. Compiler declares a variable if not previously declared in the current scope.
2. When executing, Engine looks up the variable in Scope and assigns to it, if found.

## Nested Scope

## Error

* ReferenceError is Scope resolution-failure related.
* TypeError is that Scope resolution was successful but there was an illegal/impossible action attempted against the result.


[Scope & Closures, Chapter 2 Lexical Scope](chapter2.md)
