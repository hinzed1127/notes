# Javascript Values

Two kinds of values:

1. Primatives

- Numbers, strings, etc.
- "I can't touch them, but look and refer to them from my code"

2. Objects and Functions

- Can connect to other values, make more of them
- "I can't destroy them"

# Expressions

Think of expressions as javascript _questions_

- "Expressions are javascript questions, with _values_ as the answers"

Ex: `console.log()`

## typeof Expression

Answers a fundamental question: what does javascript treat this input as?

- Javascript has a (suprisingly) small number of distinct types.

# Types of values

- Undefined (`undefined`) - unintentionally missing values
- Null (`null`) - Intentionally missing values
- Booleans (`true`/`false`) - logical operations
- Numbers - math
- Strings - text
- Symbols (uncommon) - hide implementation details
- BigInts (uncommon, new) - Big number math

- Objects (`{}` and others) - group together related data
- Functions (`x => x \* 2`) - used to refer to code

# Homework

1. Imagine you see some code that checks whether a value is a date: typeof(value) === 'date'. Will this code work? Why or why not?
2. Open some JavaScript code that you have been working on and put console.log(typeof(something)) in it, replacing something with different variables in your code. Can you find an example for every value type in the list above? Try to “collect” as many types as you can.
3. One of the values mentioned in this chapter “lies” about its type. Concretely, typeof() will return an incorrect answer for it because of a JavaScript bug that is now too late to fix. Unless you already know it, find this value by trying typeof() for every example in the list above.

## Answers

1.

```javascript
console.log(typeof undefined); // undefined
console.log(typeof null); // object
console.log(typeof true); // boolean
console.log(typeof 3); // number
console.log(typeof "test"); // string
console.log(typeof Symbol("test")); // symbol
console.log(typeof BigInt(9007199254740991)); // bigint
console.log(typeof (() => {})); // function
console.log(typeof {}); // object
```

2. No it won't. Date is not a primitive type. It is represented as an object
3. The `null` value is actually of type `object` (historical reason for why explained [here](https://2ality.com/2013/10/typeof-null.html?ck_subscriber_id=693526947)).
