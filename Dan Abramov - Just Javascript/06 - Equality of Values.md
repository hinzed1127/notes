# Equality of Values

3 kinds of equality in JavaScript:

- **Strict Equality**: a === b (triple equals)
- **Loose Equality** a == b (double equals)
- **Same Value Equality**: Object.is(a, b)

## Same Value Equality

Is what is sounds like. `Object.is(a, b)` tells us if a and b are the same value.

```js
console.log(Object.is(2, 2)); // true
console.log(Object.is({}, {})); // false
```

In this sense "Same" means intutively the same type of "Same" that our mental model describes: is this the same value that our variables' lines are pointing to?

Going back to a previous example:

```js
let dwarves = 7;
let continents = "7";
let worldWonders = 3 + 4;

console.log(Object.is(dwarves, continents)); // false
console.log(Object.is(continents, worldWonders)); // false
console.log(Object.is(worldWonders, dwarves)); // true
```

The reason _why_ is `dwarves` and `worldWonders` point to the same value, whereas `continents` does _not_, yielding the results above.

In our mental model, that can be boiled down to this:

> If two values are represented by a single shape in our diagram, it means they aren't really _two_ different values. They are the same _one_ value! This is the same as the case for which `Object.is(a, b)` returns `true`.

This is the main idea the "Counting the Values" tried to nail down.

### But What About Objects?

```js
let banana = {};
let cherry = banana;
let chocolate = cherry;
cherry = {};

console.log(Object.is(banana, cherry)); // false
console.log(Object.is(cherry, chocolate)); // false
console.log(Object.is(chocolate, banana)); // true
```

In the mental model we've built up, this naturally is described.

![wire diagram](https://res.cloudinary.com/dg3gyk0gu/image/upload/v1582119847/just-javascript-email-images/jj06/banana-final.png)

## Strict Equality: a === b

This one is more familiar

```js
console.log(2 === 2); // true
console.log({} === {}); // false
```

There's also !==

## Same Value Equality vs Strict Equality

In almost all cases, `a === b` and `Object.is(a, b)` behave the same way. There are 2 exceptions to this rule:

1. `NaN === NaN` is `false`, even though they're the same value (`Object.is(NaN, NaN)` is true)
2. `-0 === 0` and `0 === -0` are `true`, even through they're different values (`Object.is(0, -0)` is false)

### Special Case 1: NaN

This is largely a historical consequence, so commit it to memory and leave it at that. There's 3 other ways to check if something is `NaN`:

- `Number.isNaN(size)`
- `Object.is(size, NaN)`
- `size !== size`
  - This works because `NaN` is the only value not equal to itself, so only `NaN` could evaluate to true here.

### Special Case 2: -0

Negative zero exists in floating point math, so it is a different _value_. Paradoxically, `0 === -0` and `-0 === 0` are both true. It's unlikely you'll encounter this one, but good to know.

## Loose Equality (Double Equals)

A bit of a bogeyman in JS. Just a few bad examples:

```js
console.log([[]] == ""); // true
console.log(true == [1]); // true
console.log(false == [0]); // true
```

It's relatively uncommon in modern code, so not a huge deal to memorize cases with it.

One common sight still:

```js
if (x == null) {
  /* ... */
}
```

is equivalent to:

```js
if (x === null || x === undefined) {
  /* ... */
}
```

## Recap

3 Types of Equality in JS:

1. Same Value Equality (`Object.is(a,b)`)
   - Matches our concept of sameness established previously
   - Is true when we point to the same value on our diagrams
   - Easiest to explain, verbose to continually write
2. Strict Equality (`a === b`)
   - most common, two edge cases:
   1. `NaN === NaN` is `false`, even though they're the same value (`Object.is(NaN, NaN)` is true)
   2. `-0 === 0` and `0 === -0` are `true`, even through they're different values (`Object.is(0, -0)` is false)
3. Loose Equality (`a == b`)
   - best to avoid
