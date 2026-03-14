# IIFE (Immediately Invoked Function Expression)

An **IIFE (Immediately Invoked Function Expression)** is a function that **runs immediately after it is defined**.

It is commonly used to:

- Avoid polluting the global scope
- Create private variables
- Execute code instantly

---

# Basic Syntax

```javascript
(function () {
  console.log("IIFE executed");
})();
```

**Output:**

```javascript
IIFE executed
```

**The function is:**

1. Wrapped in parentheses to create a function expression

2. Immediately executed using `()`

## Arrow Function IIFE

You can also write an IIFE using arrow functions.

```javascript
(() => {
  console.log("Arrow IIFE");
})();
```

## Why Parentheses Are Needed

Without parentheses, JavaScript treats the function as a **function declaration**, not an expression.

**Incorrect:**

```javascript
function () {
  console.log("Hello");
}();
```

This causes an error.

**Correct:**

```javascript
(function () {
  console.log("Hello");
})();
```

## IIFE with Parameters

You can pass arguments to an IIFE.

```javascript
(function (name) {
  console.log("Hello " + name);
})("Malik");
```

**Output:**

```javascript
Hello Malik
```

## Real World Example

IIFE is useful for creating **private variables.**

```javascript
const counter = (function () {
  let count = 0;

  return {
    increment() {
      count++;
      return count;
    },
    decrement() {
      count--;
      return count;
    },
  };
})();

console.log(counter.increment());
console.log(counter.increment());
console.log(counter.decrement());
```

**Output:**

```javascript
1;
2;
1;
```

Here, the variable `count` cannot be accessed directly from outside.

## IIFE Before ES6 Modules

Before ES6 modules existed, developers used IIFEs to create private scopes.

**Example:**

```javascript
(function () {
  const secret = "hidden";

  function reveal() {
    console.log(secret);
  }

  reveal();
})();
```

Variables inside the IIFE do not leak into the global scope.

## Advantages of IIFE

IIFE provides several benefits:

- Prevents global variable pollution

- Creates private scope

- Executes code immediately

- Helps organize code

## Modern JavaScript Note

Today, **ES6 modules** solve many problems that IIFEs were used for.

However, understanding IIFE is still important because:

- Many older codebases use it

- It explains how JavaScript scoping works

- It appears in interviews

## Summary

An IIFE is a function that:

- Is defined and executed immediately

- Creates a private scope

- Prevents global namespace pollution

**Example:**

```javascript
(function () {
  console.log("Executed immediately");
})();
```

IIFEs were widely used before **ES6 modules** and remain an important concept in JavaScript.
