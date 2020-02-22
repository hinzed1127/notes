```javascript
let reaction = "yikes";
reaction[0] = "l";
console.log(reaction);
```

What is the expected output? Write down your exact thought process.

For me:

- Reaction is a string
- `reaction[0]` is the first letter of the string. 'l' is a string, so it remains as such.
- This leads to a final value of '1ikes'

Answer: the final result is still "yikes"

# What happened?

Straightforward answer:

> This code will either print "yikes" or throw an error depending on whether you are in strict mode

## Primitive Values Are Immutable

The false equivalency I made is shown here

```javascript
let arr = [212, 8, 506];
let str = "hello";

console.log(arr[0]); // 212
console.log(str[0]); // 'h'
```

This makes it seem like arrays and strings behave the same. But remember, arrays are actually objects under the hood, whereas strings are strings - that is, they're a primitive type! Therefore, you can't change, or "mutate", them.

```javascript
arr[0] = 420;
console.log(arr); // [420, 8, 506]

str[0] = "j"; // this would throw an error in strict mode
```

If I try the same thing in strict mode, I get this error:

`TypeError: Cannot assign to read only property '0' of string 'yikes'`

Another example of trying go mutate a primitive, thus failing:

```javascript
let fifty = 50;
fifty.shade = "gray"; // fails
```

# Variables as Wires

A (potentially) contradictory example:

```js
let pet = "Narwhal";
pet = "The Kraken";
console.log(pet); // "The Karaken"
```

We're not changing the primitive here, the _variable itself_.

**Variables are not values**

**_Variables point to values_**

Once you define a variable, you can do 2 things:

1. Assign a value to it.
2. Read its value (e.g., `console.log()`)

When you assign a variable, the left side of the assignment is a "wire". The right side is an expression (which can include _literals_ like 2 or 'this string').

Remember, from the last lesson:

> "Expressions are javascript questions, with _values_ as the answers"

expressions can be something that actually needs to be evaluated, like so

```js
pet = count + " Dalmations";
```

or _literals_ - something like `2` or 'The Kraken - values that we literally write down

# Reading a value of a variable

`console.log(pet)` is asking for the current value of pet. The same expression can give different values at different times depending on what `pet`'s value is.

# Nouns and Verbs

- "pass a variable" vs "pass a value"

Example

```js
function double(x) {
  x = x * 2;
}

let money = 10;
double(money);
console.log(money); // 10
```

we're passing the _value_, not the variable. therefore, `money` isn't going to change.

# Recap

- Primitive values are immutable
  - Arrays are _not_ primitive, so we can set their properties
- Variables are not values
  - Variables _point_ to values. We can change what we point variables to.
- Varibles are like wires
- Look out for contradictions. They usually point to depper truths.
