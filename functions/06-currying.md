# Currying in JavaScript

**Currying** is a functional programming technique where a function with multiple arguments is transformed into a **series of functions**, each taking **one argument at a time**.

**Instead of:**

`f(a, b, c)`

**Currying converts it into:**

`f(a)(b)(c)`

This allows functions to be **reused and composed more easily**.

---

# Basic Example

**Normal function:**

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5
```

**Curried version:**

```javascript
function add(a) {
  return function (b) {
    return a + b;
  };
}

console.log(add(2)(3)); // 5
```

The function takes one argument at a time.

## Using Arrow Functions

Currying can be written more cleanly with arrow functions.

```javascript
const add = (a) => (b) => a + b;

console.log(add(2)(3)); // 5
```

## Example with Three Arguments

**Normal function:**

```javascript
function multiply(a, b, c) {
  return a * b * c;
}

console.log(multiply(2, 3, 4)); // 24
```

**Curried version:**

```javascript
const multiply = (a) => (b) => (c) => a * b * c;

console.log(multiply(2)(3)(4)); // 24
```

## Practical Example

Currying allows partial application.

```javascript
const multiply = (a) => (b) => a * b;

const double = multiply(2);
const triple = multiply(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

**Here:**

- `multiply(2)` creates a double function

- `multiply(3)` creates a triple function

## Why Currying Is Useful

**Currying helps with:**

- `Function reuse`

- `Partial application`

- `Cleaner functional programming`

- `Creating specialized functions`

**Example:**

```javascript
const greet = (greeting) => (name) => `${greeting} ${name}`;

const sayHello = greet("Hello");
const sayHi = greet("Hi");

console.log(sayHello("Malik"));
console.log(sayHi("Ali"));
```

**Output:**

```javascript
Hello Malik
Hi Ali
```

## Currying in Libraries

Currying is commonly used in libraries like:

- `Lodash`

- `Ramda`

- `Redux`

- `Functional programming utilities`

**Example:**

```javascript
const add = (a) => (b) => a + b;

const add10 = add(10);

console.log(add10(5)); // 15
```

## Currying vs Partial Application

- **Currying** transform a function into multiple functions with one argument

- **Partial Application** fix some arguments of a function

**Example:**

```javascript
const multiply = (a) => (b) => a * b;

const double = multiply(2);
```

## Summary

Currying is a technique where:

- A function takes one argument at a time

- Multiple arguments are transformed into nested functions

**Example:**

```javascript
const add = (a) => (b) => a + b;
add(2)(3);
```

Currying helps create **reusable**, **composable**, and **flexible functions** in **JavaScript**.
