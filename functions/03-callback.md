# Callbacks in JavaScript

A **callback function** is a function that is **passed as an argument to another function** and executed later.

Callbacks allow JavaScript to handle **asynchronous operations** like:

- API requests
- File reading
- Timers
- Event handling

---

# Basic Callback Example

```javascript
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

function sayBye() {
  console.log("Goodbye!");
}

greet("Malik", sayBye);
```

**Output:**

```javascript
Hello Malik
Goodbye!
```

**Here:**

- `sayBye` is passed as a callback

- `greet` executes it after printing the message

## Callback with Anonymous Function

You can pass a function directly.

```javascript
function processUser(name, callback) {
  console.log("Processing user:", name);
  callback();
}

processUser("Malik", function () {
  console.log("User processed successfully");
});
```

**Output:**

```javascript
Processing user: Malik
User processed successfully
```

## Callback with Arrow Function

Modern JavaScript often uses arrow functions.

```javascript
function calculate(a, b, operation) {
  return operation(a, b);
}

const result = calculate(5, 3, (x, y) => x + y);

console.log(result);
```

**Output:**

```javascript
8;
```

## Real World Example: Array Methods

Array methods like `map`, `filter`, and `forEach` use callbacks.

**Example with `map()`:**

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(function (num) {
  return num * 2;
});

console.log(doubled);
```

**Output:**

```javascript
[2, 4, 6, 8];
```

**Using arrow function:**

```javascript
const doubled = numbers.map((num) => num * 2);
```

## Asynchronous Callback Example

Callbacks are widely used for asynchronous tasks.

**Example with `setTimeout`:**

```javascript
console.log("Start");

setTimeout(function () {
  console.log("Timer finished");
}, 2000);

console.log("End");
```

**Output:**

```javascript
Start
End
Timer finished
```

The callback runs after 2 seconds.

## Callback Hell

When callbacks are nested deeply, code becomes hard to read.

**Example:**

```javascript
loginUser(user, function (user) {
  getUserPosts(user.id, function (posts) {
    getPostComments(posts[0], function (comments) {
      console.log(comments);
    });
  });
});
```

This structure is called **Callback Hell** or the **Pyramid** of **Doom**.

**Problems:**

- Hard to read

- Hard to maintain

- Hard to debug

## Solutions to Callback Hell

Modern JavaScript solves this problem using:

- Promises

- Async/Await

**Example with Promise (simplified):**

```javascript
loginUser(user).then(getUserPosts).then(getPostComments).then(console.log);
```

## When Callbacks Are Used

**Callbacks are commonly used in:**

- Node.js APIs

- Event listeners

- Array methods

- Timers

- Asynchronous operations

**Example event listener:**

```javascript
document.addEventListener("click", function () {
  console.log("Page clicked");
});
```

## Summary

**A callback function:**

- Is passed into another function

- Is executed later

- Allows asynchronous behavior

**Callbacks are a core concept in JavaScript and form the foundation for:**

- Promises

- Async/Await

- Event-driven programming
