# Properties

> **In our JavaScript universe, both variables and properties act like "wires".** However, the wires of properties _start from objects_ rather than from our code (i.e., variables)

![sherlock wire diagram](https://res.cloudinary.com/dg3gyk0gu/image/upload/v1584416479/just-javascript-email-images/jj07/sherlock_props.png)

- Properties don't _contain_ values - they _point_ at them.
- Multiple cases of wires, which always point at values.
  - Further development of our "thinking in wires" mode.

## Reading a Property

We read properties with "dot notation":

```js
console.log(sherlock.age); // 64
```

`sherlock.age` is just an _expression_, our JS questions.

- answered by following the wires ( sherlock -> object -> age property)

## Property Names

- Names are case-sensitive
- Names can't be duplicated on the same object

## Assigning a Property

Like variables, we just want to make sure we're assigning _values_ to properties.

- Follow the wires from the left to values on the right.

## Missing Properties

What happens here?

```js
let sherlock = { surname: "Holmes", age: 64 };
console.log(sherlock.boat); // ?
```

JS follows 3 rules (simplified for now):

1. Check the value before the dot (in this case, `sherlock`)

2. If that value is `null` or `undefined`, throw an error

3. Check if a property exists with that name in the object

   a. If it does exist, answer with the value

   b. If it does _not_ exist, answer with `undefined`

Following those rules, if we add in this next call, here is the result:

```js
let sherlock = { surname: "Holmes", age: 64 };
console.log(sherlock.boat); // undefined
console.log(sherlock.boat.name); // TypeError!
```

## Summary

- Properties are wires - similar to variables, they point at values. However, property values start from objects
- Properties have names, belonging to particular objects. The same name can be repeated on the same object
- Assignment in 3 steps:

1. Figure out which wire is on the left
2. Figure out which value is on the right.
3. Point that wire to that value.

- `obj.property` expression calulcation in 3 steps:

1. which value is on the left
2. If `null` or `undefined`, throw an error.
3. If property exists, result is the value the wire points to.
4. If property doesn't exist, result is `undefined`.
