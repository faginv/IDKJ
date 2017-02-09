# Chapter 3: Objects

### syntax
* declarative (literal)
* constructed

### Type

##### primitive Types (primary types, or simple primitives)
* string
* number
* boolean
* null
* undefined
* object

##### special object sub-types (complex primitives)
* function ("callable object")
* array
* built-in Objects
  * String
  * Number
  * Boolean
  * Function
  * Array
  * Date
  * RegExp
  * Error

string, number, and boolean primitives, calling a property or method on them, the engine automatically coerces them to their object wrapper form.

`null` and `undefined` have no object wrapper form, only primitive values.
`Date` values can only be created with their constructed object form, as they have no literal form counter-part.

Object, Array, Function, and RegExp objects:
Only use the constructed form if you need the extra options.

Error object is usually created automatically when exceptions are thrown.

 ### Contents

The engine stores values in implementation-dependent ways, and may very well not store them in some object container.
What is stored in the container are these property names, which act as pointers (references) to where the values are stored.

 * "property" access: `.` operator, requires an Identifier compatible property name after it.
 * "key" access: `[ ]` operator, can take basically any UTF-8/unicode compatible string as the name for the property, and can programmatically build up the value of the string.


In objects, property names are always strings. If you use any other value besides a `string` as the property, it will first be converted to a string.

#### computed property names (ES6)
Where you can specify an expression, surrounded by a `[ ]` pair, in the key-name position of an object-literal declaration.

#### Duplicating objects

* deep copy: no clear answer

  one solution is
  ``` JavaScript
  var newObj = JSON.parse(JSON.stringify(someObj));
  ```

* shallow copy

  `Object.assign(..)` (ES6) : any special characteristics of property (like writable) on a source object are not preserved on the target object.
  ``` JavaScript
  var newObj = Object.assign({}, someObj);
  ```

#### Property descriptors

``` JavaScript
var myObject = {
  a: 2
};

Object.getOwnPropertyDescriptor(myObject, "a");

// return Object
// {
//   value: 2,
//   writable: true,
//   enumerable: true,
//   configurable: true
// }
```

`Object.defineProperty(..)`: to add a new property, or modify an existing one (if it's configurable), with the desired characteristics.

``` JavaScript
Object.defineProperty(object1, "b", {
	value: 3,
	writable: true,
  configurable: true,
  enumerable: true
});

// return Object
// {
//    b: 3
// }
```

###### writable

the ability to change the value of a property is controlled by `writable`.
modification of the value silently failed.
In strict mode, get an `TypeError`.

###### configurable

As long as a property is currently configurable, we can modify its descriptors definition, using `defineProperty(..)`.

Regardless of `strict mode`, if you attempt to change the descriptor definition of non-configurable property, get an `TypeError`. Changing `configurable` to `false` is a one-way action and cannot be undone.

`configurable: false` prevents using the `delete` operator to remove an existing property.
`delete` call failed silently.

###### enumerable  

`enumerable` controls if a property will show up in certain object-property enumerations, such as the `for .. in`.


#### Immutability

All approaches create shallow immutability. The contents of any referenced other objects are unaffected.

###### Object Constant

You can create a constant as an object property by combining `writable: false` and `configurable: false`.

###### Prevent extensions

Calling `Object.preventExtensions(..)` prevents an object from having new properties added to it.
In `non-strict mode`, a new property creation fails silently. In `strict mode`, it throws a `TypeError`.

###### Seal

`Object.seal(..)` creates a sealed object. It takes an existing object, calls `Object.preventExtensions(..)` on it, and marks all its existing properties as `configurable: false`.

###### Freeze

`Object.freeze(..)` creates a frozen object. It takes an existing object, calls `Object.seal(..)` on it, and marks all "data accessor" properties as `writable: false`.

#### `[[Get]]`

`myObject.a` is a property access. It performs a `[[Get]]` operation. It first inspects the object for a property of the requested name, and if it finds it, it will return the value accordingly. If it does not find a property, it traverses the `[[Prototype]]` chain. If it cannot through any means come up with a value for requested property, it returns the value `undefined`.

If you reference a variable that cannot be resolved within the applicable lexical scope look-up, a `ReferenceError` is thrown.

#### `[[Put]]`

If the property is present, the `[[Put]]` algorithm will roughly check:
  1. Is the property an accessor descriptor? If so, call the setter, if any.
  2. Is the property a data descriptor with `writable` of `false`? If so, silently fail in `non-strict mode`, or throw `TypeError` in `strict mode`.
  3. Otherwise, set the value to the existing property as normal.

#### Getters & Setters

When you define a property to have either a getter or a setter or both, its definition becomes an "accessor descriptor". The `value` and `writable` characteristics of the descriptor are moot and ignored.

Always declare both getter and setter.

#### Existence

The `in` operator will check to see if the property is in the object, or if it exists at any higher level of the `[[Prototype]]` chain object traversal.

`hasOwnProperty(..)` checks to see if only the Object has the property or not.

###### enumerations

`propertyIsEnumerable(..)` tests if the given property name exists directly on the object and is also `enumerable: true`.

`Object.keys(..)` returns an array of all enumerable properties on only the direct object.

`Object.getOwnPropertyNames(..)` returns an array of all properties on only the direct object.

#### iteration

The `for..in` loop iterates over the list of enumerable properties on an object including its `[[Pototype]]`.

`for` loop is iterating over the indices.

`forEach(..)` iterates over all values in the array, and ignores any callback return values.

`every(..)` keeps going until the end or the callback returns a false value.

`some(..)` keeps going until the end or the callback returns a true value.

`for ..of` (ES6) iterates over the values directly. Arrays have a built-in `@@iterator`.
