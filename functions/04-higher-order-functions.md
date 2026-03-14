# Higher-Order Functions in JavaScript

A **Higher-Order Function (HOF)** is a function that:

1. **Takes another function as an argument**, or
2. **Returns another function**

Higher-order functions are a key concept in **functional programming** and are widely used in modern JavaScript.

---

# Example 1: Function as Argument

```javascript
function greet(name) {
  return "Hello " + name;
}

function processUser(callback) {
  const result = callback("Malik");
  console.log(result);
}

processUser(greet);
```

**Output**

```javascript
Hello Malik
```

**Here:**

- `processUser` is a higher-order function

- `greet` is passed as a callback function

## Example 2: Returning a Function

A higher-order function can also return another function.

```javascript
function multiplier(factor) {
  return function (number) {
    return number * factor;
  };
}

const double = multiplier(2);

console.log(double(5));
```

**Output**

```javascript
10;
```

The function `multiplier` returns another function that multiplies numbers.

## Real-World Example: Array Methods

Many built-in JavaScript methods are higher-order functions.

**Common examples:**

- `map()`

- `filter()`

- `reduce()`

- `forEach()`

**Example: map()**

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(function (num) {
  return num * 2;
});

console.log(doubled);
```

**Output**

```javascript
[2, 4, 6, 8];
```

`map()` takes a callback function, making it a higher-order function.

**Example: filter()**

```javascript
const numbers = [1, 2, 3, 4, 5];

const evenNumbers = numbers.filter((num) => num % 2 === 0);

console.log(evenNumbers);
```

**Output**

```javascript
[2, 4];
```

**Example: reduce()**

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((total, num) => total + num, 0);

console.log(sum);
```

**Output**

```javascript
10;
```

## Why Higher-Order Functions Are Important

Higher-order functions help developers:

- Write cleaner code

- Avoid code duplication

- Follow functional programming principles

- Work effectively with arrays and asynchronous logic

## Practical Example

Instead of repeating logic:

```javascript
function double(numbers) {
  const result = [];

  for (let num of numbers) {
    result.push(num * 2);
  }

  return result;
}
```

You can use `map()`:

```javascript
const result = numbers.map((num) => num * 2);
```

This is shorter, cleaner, and easier to maintain.

## Summary

A **Higher-Order Function** is a function that:

- Accepts another function as an argument

- Returns a function

**Examples in JavaScript:**

- `map()`

- `filter()`

- `reduce()`

- `setTimeout()`

- `addEventListener()`

Higher-order functions are a core concept in modern **JavaScript** development.
