# Arrow Functions in JavaScript

Arrow functions are a **shorter syntax for writing functions** introduced in **ES6 (ECMAScript 2015)**.

They provide a **clean and concise way to write functions**, especially for callbacks and functional programming.

---

# Basic Syntax

Traditional function:

```javascript
function add(a, b) {
  return a + b;
}
```

**Arrow function:**

```javascript
const add = (a, b) => {
  return a + b;
};
```

**Shorter version:**

```javascript
const add = (a, b) => a + b;
```

If the function contains only one expression, the `return` keyword is implicit.

## Arrow Function with One Parameter

If a function has only one parameter, parentheses are optional.

```javascript
const square = (x) => x * x;

console.log(square(5)); // 25
```

## Arrow Function with No Parameters

If there are no parameters, parentheses are required.

```javascript
const greet = () => {
  console.log("Hello World");
};

greet();
```

## Returning Objects

When returning an object, wrap it in parentheses.

**Incorrect:**

```javascript
const createUser = () => {
  name: "Malik";
};
```

**Correct:**

```javascript
const createUser = () => ({ name: "Malik" });
```

## Arrow Functions in Arrays

Arrow functions are commonly used with array methods.

Example with `map()`:

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((num) => num * 2);

console.log(doubled);
```

**Output:**

```javascript
[2, 4, 6, 8];
```

## Arrow Functions and `this`

Arrow functions do not have their own `this`.

Instead, they inherit this from the surrounding scope.

**Example:**

```javascript
const user = {
  name: "Malik",
  greet: function () {
    setTimeout(() => {
      console.log("Hello " + this.name);
    }, 1000);
  },
};

user.greet();
```

**Output:**

```javascript
Hello Malik
```

Because the arrow function inherits `this` from `greet`.

## When NOT to Use Arrow Functions

Arrow functions should not be used:

**1. As Object Methods**

```javascript
const user = {
  name: "Malik",
  greet: () => {
    console.log(this.name);
  },
};

user.greet();
```

**Output:**

```javascript
undefined;
```

Because arrow functions do not bind their own `this`.

**2. As Constructors**

Arrow functions cannot be used with `new`.

```javascript
const Person = (name) => {
  this.name = name;
};

const p = new Person("Malik"); // Error
```

## Real World Example (React)

Arrow functions are commonly used in React components.

```javascript
const Button = () => {
  return <button>Click Me</button>;
};
```

## Summary

Arrow functions:

- `Provide shorter syntax`

- `Do not bind their own this`

- `Do not have arguments`

- `Cannot be used as constructors`

- `Are heavily used in callbacks and modern JavaScript`

They are a core feature of modern JavaScript development.
