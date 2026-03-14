# Pure Functions in JavaScript

A **Pure Function** is a function that:

1. **Always returns the same output for the same input**
2. **Does not modify external state (no side effects)**

Pure functions are predictable, easier to test, and easier to debug.

---

# Example of a Pure Function

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5
console.log(add(2, 3)); // 5
```

The function always returns the same result for the same **inputs**, and it does not change anything outside the function.

## Example of an Impure Function

```javascript
let total = 0;

function addToTotal(value) {
  total += value;
  return total;
}

console.log(addToTotal(5));
console.log(addToTotal(5));
```

**Output:**

```javascript
5;
10;
```

This is not a pure function because it modifies the external variable `total`.

## Another Impure Function Example

```javascript
function greet() {
  console.log("Hello");
}
```

This function has a side effect (printing to the console), so it is not pure.

## Side Effects

A side effect occurs when a function:

- `Modifies a global variable`

- `Changes external data`

- `Makes an API request`

- `Writes to the DOM`

- `Logs to the console`

**Example:**

```javascript
let count = 0;

function increment() {
  count++;
}
```

This function changes external state, making it impure.

## Converting an Impure Function to a Pure Function

**Impure:**

```javascript
let count = 0;

function increment() {
  count++;
}
```

**Pure:**

```javascript
function increment(count) {
  return count + 1;
}
```

Now the function depends only on its input.

## Real World Example (Array Operations)

Pure functions are commonly used with array methods.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map((num) => num * 2);

console.log(doubled);
```

`map()` returns a new array without modifying the original one.

## Why Pure Functions Are Important

Pure functions provide several advantages:

- `Predictable behavior`

- `Easier testing`

- `No unexpected side effects`

- `Better debugging`

- `Easier parallel processing`

This is why they are heavily used in **functional programming** and **modern frameworks**.

## Pure Functions in React

React components are often designed as pure functions.

**Example:**

```javascript
function Greeting({ name }) {
  return <h1>Hello {name}</h1>;
}
```

The output depends only on the input (**props**).

## Summary

A pure function:

- `Returns the same output for the same input`

- `Does not modify external variables`

- `Has no side effects`

Pure functions help create **clean**, **predictable**, and **maintainable code** in JavaScript applications.
