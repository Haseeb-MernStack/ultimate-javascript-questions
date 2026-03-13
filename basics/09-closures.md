# Closures in JavaScript

A **closure** is created when a function **remembers and can access variables from its outer scope even after the outer function has finished executing**.

Closures are possible because JavaScript uses **lexical scoping**.

---

# Basic Example

```javascript
function outer() {
  let message = "Hello";

  function inner() {
    console.log(message);
  }

  inner();
}

outer();
```

**Output**:

```javascript
Hello;
```

The inner function can access `message` because it exists in the outer scope.

## Closure Example

A closure happens when the inner function is returned.

```javascript
function outer() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const counter = outer();

counter();
counter();
counter();
```

**Output**:

```javascript
1;
2;
3;
```

Even after `outer()` finishes, the returned function remembers the variable `count`.

This memory is called a closure.

## How Closures Work

When `outer()` runs:

**1.** A variable `count` is created

**2.** The inner function is returned

**3.** The inner function keeps access to `count`

JavaScript keeps the variable in memory because the inner function still needs it.

## Real-World Example: Private Variables

Closures allow you to create private variables.

```javascript
function createUser() {
  let password = "12345";

  return {
    getPassword: function () {
      return password;
    },
  };
}

const user = createUser();

console.log(user.getPassword());
```

**Output**:

```javascript
12345;
```

The `password` variable cannot be accessed directly from outside the function.

## Another Example: Counter Function

Closures are commonly used to maintain state.

```javascript
function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter = createCounter();

console.log(counter());
console.log(counter());
console.log(counter());
```

**Output**:

```javascript
1;
2;
3;
```

## Closures in Loops (Common Interview Question)

Example with `var`:

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

**Output**:

```javascript
4;
4;
4;
```

Why?

Because `var` is function scoped, and all callbacks share the same variable.

Solution using `let`:

```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

**Output**:

```javascript
1;
2;
3;
```

`let` creates a new block scope for each iteration.

## Why Closures Are Important

Closures are widely used in:

- `Data privacy`

- `Event handlers`

- `Callbacks`

- `React hooks`

- `Module patterns`

- `State management`

## Key Points

```javascript
Closures rely on lexical scope

Inner functions remember variables from outer functions

Closures allow data privacy and state persistence

They are widely used in modern JavaScript frameworks
```
