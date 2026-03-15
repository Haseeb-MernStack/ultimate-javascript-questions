# JavaScript Event Loop (Deep Dive)

Understanding the **Event Loop** is essential to truly understand **asynchronous JavaScript**.

Most developers can use `async/await`, but **senior JavaScript engineers understand the event loop deeply**.

This concept explains **how JavaScript executes asynchronous code while being single-threaded**.

---

# JavaScript is Single Threaded

JavaScript runs on a **single thread**, meaning it can only execute **one task at a time**.

Example:

```js
console.log("Start");
console.log("Middle");
console.log("End");
```

Output:

```
Start
Middle
End
```

Everything runs **line by line**.

But when asynchronous operations appear (like `setTimeout`, `fetch`, or `Promises`), JavaScript uses the **event loop system**.

---

# Components of the Event Loop

The JavaScript runtime consists of several parts:

```
Call Stack
Web APIs
Callback Queue (Task Queue)
Microtask Queue
Event Loop
```

Flow diagram:

```
Call Stack
   ↓
Web APIs
   ↓
Queues
   ↓
Event Loop
   ↓
Back to Call Stack
```

---

# 1. Call Stack

The **Call Stack** is where JavaScript executes functions.

Example:

```js
function first() {
  second();
}

function second() {
  console.log("Hello");
}

first();
```

Execution order:

```
Call Stack
---------
first()
second()
console.log()
```

After execution, functions are removed from the stack.

---

# 2. Web APIs

Browsers provide **Web APIs** that handle asynchronous operations.

Examples:

- `setTimeout`
- `fetch`
- `DOM events`
- `geolocation`

Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 2000);

console.log("End");
```

Execution:

1. `console.log("Start")`
2. `setTimeout` goes to **Web APIs**
3. `console.log("End")`
4. After 2 seconds → callback goes to **Queue**

Output:

```
Start
End
Timeout
```

---

# 3. Callback Queue (Task Queue)

The **Callback Queue** stores callbacks from:

- `setTimeout`
- `setInterval`
- DOM events

Example:

```js
setTimeout(() => {
  console.log("Timer finished");
}, 0);
```

Even with `0ms`, it **does not run immediately**.

It waits until the **call stack is empty**.

---

# 4. Microtask Queue

The **Microtask Queue** has **higher priority** than the callback queue.

It stores:

- `Promise.then`
- `Promise.catch`
- `Promise.finally`
- `queueMicrotask`

Example:

```js
Promise.resolve().then(() => {
  console.log("Promise resolved");
});
```

Microtasks run **before normal callbacks**.

---

# Execution Order

Priority order:

```
1. Call Stack
2. Microtask Queue
3. Callback Queue
```

The event loop checks:

```
If Call Stack empty → run Microtasks
If Microtasks empty → run Callbacks
```

---

# Example 1 (Classic Interview Question)

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

Output:

```
Start
End
Promise
Timeout
```

Explanation:

1. `Start` → Call stack
2. `setTimeout` → Web API
3. `Promise.then` → Microtask Queue
4. `End` → Call stack
5. Event loop runs **Microtask**
6. Then **Callback queue**

---

# Example 2 (More Complex)

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

Promise.resolve().then(() => {
  console.log("4");
  setTimeout(() => console.log("5"), 0);
});

console.log("6");
```

Output:

```
1
6
3
4
2
5
```

Step-by-step:

```
Call Stack
1
6

Microtasks
3
4

Callback Queue
2
5
```

---

# Event Loop Cycle

The event loop works like this:

```
while(true) {
  if(callStack.isEmpty()) {
    runMicrotasks()

    if(microtasks.empty) {
      runCallbackQueue()
    }
  }
}
```

This happens **thousands of times per second**.

---

# Visual Execution Example

Code:

```js
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => console.log("C"));

console.log("D");
```

Execution timeline:

```
Call Stack
A
D

Microtask Queue
C

Callback Queue
B
```

Final Output:

```
A
D
C
B
```

---

# queueMicrotask()

`queueMicrotask` schedules a microtask manually.

Example:

```js
console.log("Start");

queueMicrotask(() => {
  console.log("Microtask");
});

console.log("End");
```

Output:

```
Start
End
Microtask
```

---

# Event Loop in Node.js

Node.js has additional queues:

- `process.nextTick`
- `setImmediate`
- `timers`
- `poll`
- `check`

Example:

```js
process.nextTick(() => {
  console.log("nextTick");
});

Promise.resolve().then(() => {
  console.log("promise");
});
```

`process.nextTick` runs **before Promise microtasks** in Node.js.

---

# Common Interview Question

What will this output?

```js
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => console.log("C"));

console.log("D");
```

Answer:

```
A
D
C
B
```

Because **microtasks run before callbacks**.

---

# Why Event Loop Matters

Understanding the event loop helps you:

- Debug asynchronous issues
- Avoid blocking the main thread
- Optimize performance
- Understand Promises deeply
- Pass **JavaScript interviews**

---

# Summary

Important concepts:

- JavaScript is **single threaded**
- Asynchronous tasks handled by **Web APIs**
- Event loop manages execution
- Priority order:

```
Call Stack
Microtask Queue
Callback Queue
```

Microtasks always run **before** callbacks.

---
