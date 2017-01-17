# Chapter 5: Scope Closure

Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

It's not enough to have a scope to close over if that scope is empty.

```JavaScript
for(var i = 1; i <= 5; i++){
  (function(){
    var j = i;
    setTimeout(function timer(){
      console.log(j);
    }, j * 1000);
  })();
}
```

```JavaScript
for(var i = 1; i <= 5; i++){
  (function(j){
    setTimeout(function timer(){
      console.log(j);
    }, j * 1000);
  })(i);
}
```

The use of an IIFE inside each iteration created a new scope for each iteration, which gave out timeout function callbacks the opportunity to close over a new scope for each iteration, one which had a variable with the right per-iteration value in it for us to access.

###### Needs a per-iteration block scope.

```JavaScript
for(var i = 1; i <= 5; i++){
  let j = i;
  setTimeout(function timer(){
    console.log(j);
  }, j * 1000);
}
```

```JavaScript
for(let i = 1; i <= 5; i++){
  setTimeout(function timer(){
    console.log(i);
  }, i * 1000);
}
```

## Modules

#### Modern Modules

> call() and apply() can be used to invoke a function, must have the owner object as first parameter. call() takes the function arguments separately, and apply() takes the function arguments in an array.
> In strict mode, the fist argument becomes the value of **this** in the invoked function, even if the argument is not an object.
> In non-strict mode, if the value of the first argument is null or undefined, it is replaced with the gloabal object.
> http://www.w3schools.com/js/js_function_invocation.asp

```JavaScript
var MyModules = (function Manager(){
  var modules = {};

  function define(name, deps, impl){
    for(var i = 0; i < deps.length; i++){
      deps[i] = modules[deps[i]];
    }
    modules[name] = impl.apply(impl, deps);
  }

  function get(name){
    return modules[name];
  }

  return {
    define: define,
    get: get
  };
})();

MyModules.define("bar", [], function(){
  function hello(who){
    return "Let me introduce: " + who;
  }
  return{
    hello: hello
  }
});

MyModules.define("foo", ["bar"], function(bar){
  var hungry = "hippo";
  function awesome(){
    console.log(bar.hello(hungry).toUpperCase());
  }
  return {
    awesome: awesome
  }
});

var bar = MyModules.get("bar");
var foo = MyModules.get("foo");

console.log(bar.hello("hippo"));
foo.awesome();
```

#### Future Modules

< > [Scope & Closures, Chapter 4 Hoisting](chapter4.md)
