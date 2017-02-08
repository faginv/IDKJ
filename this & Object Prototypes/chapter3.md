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
