# JavaScript Closures (Functions)

Closures are one of the **most powerful features of JavaScript functions**.

A **closure** happens when a function **remembers variables from its outer scope even after the outer function has finished executing**.

Closures exist because JavaScript uses **lexical scoping**.

---

# Basic Closure Example

```javascript
function outer() {
  let message = "Hello from outer function";

  function inner() {
    console.log(message);
  }

  return inner;
}

const fn = outer();
fn();
```

**Output**

```javascript
Hello from outer function
```

Even though `outer()` has finished executing, the function `inner()` still has access to `message`.

This behavior is called a closure.

## How Closures Work

When `outer()` runs:

1. Variable `message` is created

2. `inner()` function is returned

3. JavaScript keeps `message` in memory

4. When `fn()` runs later, it still accesses `message`

So the function closes over its outer variables.

## Real World Example: Counter

Closures are often used to maintain state.

```javascript
function createCounter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const counter = createCounter();

counter();
counter();
counter();
```

**Output**

```javascript
1;
2;
3;
```

The `count` variable persists between function calls.

## Closures for Data Privacy

Closures can create private variables.

```javascript
function createUser() {
  let password = "super-secret";

  return {
    getPassword() {
      return password;
    },
  };
}

const user = createUser();

console.log(user.getPassword());
```

**Output**

```javascript
super-secret
```

You cannot access `password` directly:

```javascript
console.log(user.password); // undefined
```

Closures help protect internal data.

## Closures in Event Handlers

Closures are commonly used with event handlers.

```javascript
function setupButton(buttonId) {
  let count = 0;

  document.getElementById(buttonId).addEventListener("click", function () {
    count++;
    console.log("Clicked:", count);
  });
}

setupButton("myButton");
```

The event handler remembers the `count` variable.

## Common Interview Question

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

**Output**

```javascript
4;
4;
4;
```

Why?

Because `var` is function scoped and all callbacks share the same variable.

Solution using `let`:

```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

**Output**

```javascript
1;
2;
3;
```

`let` creates a new block scope each iteration.

## Where Closures Are Used

Closures are widely used in:

- `React hooks`

- `Event listeners`

- `Callbacks`

- `Module patterns`

- `State management`

- `Memoization`

- `Currying`

## Summary

Closures occur when:

- `A function is defined inside another function`

- `The inner function accesses variables from the outer scope`

- `The inner function remembers those variables even after the outer function finishes`

Closures allow:

- `State persistence`

- `Data privacy`

- `Powerful functional programming patterns`

Closures are a core concept every JavaScript developer must understand.\*\*\*\*

