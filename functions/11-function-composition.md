# Function Composition in JavaScript

**Function Composition** is a technique where multiple functions are **combined together to produce a new function**.

Instead of writing long, complex functions, we can **compose small reusable functions**.

**Mathematically:**

- f(g(x))

**Meaning:**

- `g(x)` runs first
- its result goes into `f()`

---

# Basic Example

```javascript
function double(x) {
  return x * 2;
}

function square(x) {
  return x * x;
}

const result = square(double(3));

console.log(result);
```

**Output:**

```javascript
36;
```

**Explanation:**

```javascript
double(3) = 6
square(6) = 36
```

## Why Function Composition Is Useful

Function composition helps:

- Break complex logic into small reusable functions

- Improve code readability

- Follow functional programming principles

## Creating a Compose Function

We can create a utility function to compose multiple functions.

```javascript
function compose(f, g) {
  return function (x) {
    return f(g(x));
  };
}
```

**Usage:**

```javascript
function double(x) {
  return x * 2;
}

function addOne(x) {
  return x + 1;
}

const composed = compose(double, addOne);

console.log(composed(5));
```

**Output:**

```javascript
12;
```

**Explanation:**

```javascript
addOne(5) = 6
double(6) = 12
```

## Composition with Arrow Functions

```javascript
const compose = (f, g) => (x) => f(g(x));
```

**Usage:**

```javascript
const double = (x) => x * 2;
const addOne = (x) => x + 1;

const result = compose(double, addOne)(5);

console.log(result);
```

## Composing Multiple Functions

We can compose many functions together.

```javascript
const compose =
  (...functions) =>
  (value) =>
    functions.reduceRight((acc, fn) => fn(acc), value);
```

**Example:**

```javascript
const addOne = (x) => x + 1;
const double = (x) => x * 2;
const square = (x) => x * x;

const transform = compose(square, double, addOne);

console.log(transform(2));
```

**Output:**

```javascript
36;
```

**Explanation:**

```javascript
addOne(2) = 3
double(3) = 6
square(6) = 36
```

## Real World Example

Formatting user data:

```javascript
const trim = (str) => str.trim();
const toLowerCase = (str) => str.toLowerCase();
const capitalize = (str) => str.charAt(0).toUpperCase() + str.slice(1);

const compose =
  (...fns) =>
  (value) =>
    fns.reduceRight((acc, fn) => fn(acc), value);

const formatName = compose(capitalize, toLowerCase, trim);

console.log(formatName("   MALIK "));
```

**Output:**

```javascript
Malik;
```

## Compose vs Pipe

Two common composition styles:

**Method** ---------------- **Order**

compose ---------------- right → left
pipe ---------------- left → right

**Example:**

```javascript
compose(f, g)(x) = f(g(x))
pipe(f, g)(x) = g(f(x))
```

## Libraries That Use Composition

Many JavaScript libraries rely on function composition:

- Redux

- Ramda

- Lodash

- RxJS

**Example from Redux:**

```javascript
compose(applyMiddleware(logger), applyMiddleware(thunk));
```

## Summary

Function composition:

- Combines multiple functions into one

- Encourages small reusable functions

- Improves code readability

- Is widely used in functional programming

**Example:**

```javascript
const compose = (f, g) => (x) => f(g(x));
```

Function composition helps build **clean**, **modular**, and **maintainable JavaScript applications.**
