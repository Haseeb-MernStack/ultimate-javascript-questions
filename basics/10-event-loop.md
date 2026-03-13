# JavaScript Event Loop

JavaScript is a **single-threaded, non-blocking language**.  
This means it can execute **one task at a time**, but it can still handle asynchronous operations efficiently.

The **Event Loop** is the mechanism that allows JavaScript to perform **asynchronous operations** like:

- API requests
- Timers
- File reading
- Event handling

without blocking the main thread.

---

# How JavaScript Executes Code

JavaScript uses three main components:

1. Call Stack
2. Web APIs
3. Callback Queue

---

# 1. Call Stack

The **Call Stack** is where JavaScript keeps track of function execution.

Functions are pushed into the stack when called and removed when finished.

**Example**:

```javascript
function greet() {
  console.log("Hello");
}

greet();
```

**Execution order**:

```javascript
Call Stack
-----------
greet()
-----------
(empty)
```

## 2. Web APIs

Web APIs are provided by the browser environment.

**Examples**:

- `setTimeout`

- `fetch`

- `DOM events`

These tasks run outside the JavaScript engine.

**Example**:

```javascript
setTimeout(() => {
  console.log("Hello");
}, 1000);
```

The timer runs inside **Web APIs**, not in the call stack.

## 3. Callback Queue

When asynchronous tasks finish, their callbacks go into the **Callback Queue**.

**Example**:

```javascript
setTimeout(() => {
  console.log("Timer finished");
}, 1000);
```

After 1 second, the callback moves into the queue.

## Event Loop

The Event Loop continuously checks:

```javascript
1. Is the Call Stack empty?

2. If yes, move the first task from the Callback Queue to the Call Stack.
```

This process allows JavaScript to handle asynchronous operations.

## Example of Event Loop

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timer");
}, 0);

console.log("End");
```

**Output**:

```javascript
Start;
End;
Timer;
```

**Explanation**:

```javascript
1. Start goes to Call Stack → executed

2. setTimeout moves to Web API

3. End executes

4. Timer callback goes to Callback Queue

5. Event Loop pushes callback to Call Stack

6. Timer executes
```

## Visual Flow

```javascript
Call Stack → Web APIs → Callback Queue
        ↑                     ↓
        ←------ Event Loop ----
```

## Microtasks vs Macrotasks

JavaScript has two queues:

```javascript
1. Microtask Queue

2. Callback (Macrotask) Queue
```

Microtasks have higher priority.

## Microtasks

**Examples**:

- `Promise.then()`

- `queueMicrotask()`

**Example**:

```javascript
console.log("Start");

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Output**:

```javascript
Start;
End;
Promise;
```

## Microtask vs setTimeout

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Output**:

```javascript
Start;
End;
Promise;
Timeout;
```

Because Microtasks run before **Macrotasks**.

## Why the Event Loop Is Important

Understanding the event loop helps developers:

```javascript
Debug asynchronous code

Avoid blocking operations

Understand promises and async/await

Write efficient JavaScript
```

## Key Points

```javascript
JavaScript is single-threaded

Asynchronous tasks run in Web APIs

Event Loop manages task execution

Microtasks run before macrotasks

Event Loop enables non-blocking JavaScript
```
