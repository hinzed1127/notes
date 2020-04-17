# Counting the Values

## Recap of Exercises

```js
// Part one
let pets = "Tom and Jerry";
feed(pets);
console.log(pets[0]);

// Part two
let pets = ["Tom", "Jerry"];
feed(pets);
console.log(pets[0]);
```

Question for those 2 situations: can we change the `console.log()` output by only changing the `feed` function?

Part 1

- No. We always pass functions values, _not variables_. In this case, the value is a string, ie, a primitive, and therefore, it is immutable and can't be changed.

Part 2

- Yes. The value is still what's being passed, but arrays are an object, so they are mutable. The `feed` function could certainly alter them.

## The Javascript Simulation

Talks about how to think about the relationship between abstract mental models and physical reality.

- **Our mental model won't answer questions like "how is a value represented in the computer memory? This answer changes all the time and (for the most part) shouldn't be as important to us**

  - Think of a string as a _value_, not a "pointer" or "memory address." That definition might be higher-level and not as granular, but **it's good enough for our purposes**.

### Our foundation thus far

- **The foundation of our mental model is a world full of values**
  - Values belong to one of a few built-in types
    - Some of these types are primitives, and therefore **immutable**.
  - Variables are "wires" poining from names to values

## Counting the values

- Counting as a means to distinguish things from one another
  - This is key to understanding Javascript _equality_.

### Undefined

The only possible value for this type is literally `undefined`

- Reading a property for an undefined variable results in a `TypeError`

```js
let person = undefined;
console.log(person.mood); // TypeError!
```

- `undefined` values represent _unintentionally_ missing values. While you could write `undefined` yourself, it naturally occurs in situations where Javascript doesn't know what value you wanted. E.g.,

```js
let bandersnatch;
console.log(bandersnatch); // undefined
```

You could always still point it to another value if you want (or explicitly at undefined).

**Note**: this is not the same as "this variable is not yet defined". That would throw an error:

```js
console.log(jabberwocky); // ReferenceError!
let jabberwocky;
```

Undefined is a primitive, and the only value of its type.

### Null

A sibling of sorts to `undefined`. Also the only value of its own type.

Due, to a historical sidenote, `null` registers as an object:

```js
console.log(typeof null); // "object" (a lie!)
```

- `null` is a primitive, _not_ an object

- Generally, `null` is for _intentionally_ missing values. This convention could lead to something like this:

  - coding mistake -> `undefined`
  - valid missing data -> `null`

### Booleans

Two values: `true` and `false`

#### Mental model thought exercise

Go through this code

```js
let isSad = true;
let isHappy = !isSad;
let isFeeling = isSad || isHappy;
let isConfusing = isSad && isHappy;
```

Big idea in our mental model: even through we have 4 different variables, our mental model only has two values that they _point_ to: 1 true and 1 false.

### Numbers

Big ideas for numbers in JavaScript:

- JS uses floating point math
  - numbers are more precise closer to 0, less so further away
  - causes things like this:
  ```js
  console.log(0.1 + 0.2 === 0.3); // false
  console.log(0.1 + 0.2 === 0.30000000000000004); // true
  ```
- Numbers resulting from invalid math operations like 1 / 0 or 0 / 0 are special. `NaN` is an example.
- `typeof(NaN)` is a number because it's a number value (representing the idea of an "invalid number")

### BigInts

Recent addition to JavaScript. Intended to fill the gap between regular numbers and larger ints that need precision.

### Strings

Strings are primitives of type string:

```js
console.log(typeof "basic string"); // "string"
```

They have some built in properties:

- `.length`
- references that look like arrays (eg, 'basic string'[0] is "b")

However, they are _not_ obects. You can't assign anything to myStringVar[0], because it's immutable.

In our mental model, with respect to memory, each distinct string alread exists and we point to them (this is not completely accurate, but sufficient for now)

### Symbols

Another recent addition to JS. We're saving them for later until covering object and properties better.

### Objects

Non-primitive values (things like arrays, dates, RegExps, etc). Mutatable by default.

```js
let person = { name: "Daniel" };
person.name = "Dan"; // dot notation
person["name"] = "Daniel"; // bracket notation
```

Unlike primitives, every time we use the object literal ,`{}`, we create a brand new object value:

```js
let shrek = {};
let donkey = {};
```

These each have lines to their own `{}`. Same for arrays and other objects. Because JS is a garbage-collected language, these objects never get directly destroyed by us (important to keep in mind w/r/t memory leaks).

### Functions

Same as objects for creation

```js
for (let i = 0; i < 7; i++) {
  let dig = function () {
    // Do nothing
  };
  console.log(dig);
}
```

This creates seven different distance function values. We _create_ objects and functions.
