# Understanding `this` in JavaScript

Source: [WTF is this - Understanding the this keyword, call, apply, and bind in JavaScript](https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/) by Tyler McGinnis

## Purpose

`this` lets you decide what object is focal when executing a function or method.

Four rules of `this`:

- Implicit Binding
- Explicit Binding
- new Binding
- window Binding

Main idea: you can't know what the value of this will be for a specific function until that function is invoked.

### Implicit Binding

**Left of the dot rule**

- When you call a function on an object, `this` is implicitly going to be the item to the "left of the dot

Example: Dog object

```javascript
const dog = {
  name: 'Shiloh',
  age: 6,
  greeting: () => {
    console.log(`My name is ${this.name}`);
  }
};

dog.greeting(); // "My name is Shiloh
```

### Explicit Binding

Takes advantage of the protoypal functions `.call`, `.apply`, and `.bind`.

First, let's modify the dog example to take the greeting function and move it outside the dog object.

```javascript
const dog = {
  name: 'Shiloh',
  age: 6
};

function greeting(owner) {
  let greeting = `My name is ${this.name}`);

  if (owner) {
    greeting += (` My owner is ${owner}`);
  }

  return greeting
}
```

#### Function.prototype.call

This takes an argument for the for what will serve as the `this` keyword followed by any additional arguments. Ex:

```javascript
greeting.call(dog, 'Dan'); // My name is Shiloh. My owner is Dan.
```

#### Function.prototype.apply

Same thing as `.call`, but it takes an optional second argument that is an _array_ of arguments that will get passed along to the function in order. Our example uses a single string, but could be changed to include more if we wanted.

```javascript
greeting.apply(dog, ['Dan']); // My name is Shiloh. My owner is Dan.
```

#### Function.prototype.bind

Whereas `.call` and `.apply` immediately invoke the function with the assigned `this` value, `.bind` creates a _new_ function with the `this` keyword set to the argument passed, as well as any arguments passed to it(like `.call`)

```javascript
const newGreetingFn = greeting.bind(dog, 'Dan');

newGreetingFn(); // My name is Shiloh. My owner is Dan.
```

### new Binding

Whenever you invoke a function with the `new` keyword, `this` is bound to the new object being contstructed.

Convention follows that we capitalize our function so that we know it's going to serve as a Constructor function.

```javascript
const Animal = function(color, name, type) {
  this.color = color;
  this.name = name;
  this.type = type;
};

const zebra = new Animal('black and white', 'Zorro', 'Zebra');
```

### window Binding

If you invoke a function using this and none of the above conditions are met (i.e., it doesn't have anything left of the dot, it doesn't use `.call`, `.apply`, or `.bind`, and it doesn't use the `new` keyword), `this` is actually bound to the window object.

Ex:

```javascript
const sayAge = function() {
  console.log(this.age);
};

const me = { age: 25 };

sayAge(); // undefined
window.age = 25;
sayAge(); // 25;
```

Note that if `sayAge` was run in strict mode (`"use strict"`) being included in the function or the current scope, JavaScript won't even let you do this and will throw this error:

`Cannot read property 'age' of undefined`
