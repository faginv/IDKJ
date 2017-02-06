# Chapter 2: `this` All makes sense now!

## 4 Rules

1. Default binding
2. Implicit binding
  * implicitly lost
3. Explicit binding
  * call(..) and apply(..)
  * hard binding
  * bind(..)
4. new binding

#### Determining `this`

1. Is the function called with `new`? If so, `this` is the newly constructed object.
2. Is the function called with `call` or `apply`, even hidden inside a `bind` hard binding? If so, `this` is the explicitly specified object.
3. Is the function called with a context, otherwise known as an owning or containing object? If so, this is that context object.
4. Otherwise, default the `this`. If in strict mode, pick `undefined`, otherwise pick the `global` object.

#### Binding exceptions

1. Ignored `this`
  * If you pass `null` or `undefined` as a `this` binding parameter to `call`, `apply`, or `bind`, those values are effectively ignored, and instead the default binding rule applies to the invocation.
2. Safer `this`
   ``` JavaScript
   var DMZ = Object.create(null);
   ```
3. Indirection
  * in cases of creating indirect references to functions, when that function reference is invoked, the default binding rule also applies.
4. Softening binding

#### Lexical `this`
In ES6, arrow-functions adopt the `this` binding form the enclosing scope.
The lexical binding of an arrow-function cannot be overridden even with new.
