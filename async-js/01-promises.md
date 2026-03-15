# Promises in JavaScript

JavaScript is **single-threaded**, but it can perform asynchronous operations using **Promises**, **async/await**, and the **event loop**.

Promises are a modern way to handle asynchronous operations in JavaScript.

---

# What is a Promise?

A **Promise** is an object that represents the **eventual completion or failure of an asynchronous operation**.

Think of a promise like a **real-life promise**:

- **Pending** → waiting
- **Fulfilled** → success
- **Rejected** → failure

**Example scenario:**

You order food from a restaurant.

- Order placed → `pending`
- Food delivered → `fulfilled`
- Order cancelled → `rejected`

---

# Promise States

A Promise has **three states**:

| State     | Meaning                          |
| --------- | -------------------------------- |
| Pending   | Initial state                    |
| Fulfilled | Operation completed successfully |
| Rejected  | Operation failed                 |

Once a promise is **fulfilled or rejected**, it becomes **settled** and cannot change.

---

# Creating a Promise

**Syntax:**

```js
const promise = new Promise((resolve, reject) => {
  // async task
});
```

**Example:**

```js
const myPromise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Operation successful");
  } else {
    reject("Operation failed");
  }
});
```

## Consuming a Promise

Promises are consumed using:

- `.then()`

- `.catch()`

- `.finally()`

**Example:**

```js
myPromise
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log("Promise finished");
  });
```

**Output:**

```js
Operation successful
Promise finished
```

## Example: Asynchronous Task

Simulating an API call:

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data received");
    }, 2000);
  });
}

fetchData().then((data) => {
  console.log(data);
});
```

**Output after 2 seconds:**

```js
Data received
```

## Promise Chaining

Promises can be chained.

**Example:**

```js
fetchData()
  .then((data) => {
    console.log(data);
    return "Processing data";
  })
  .then((result) => {
    console.log(result);
  });
```

**Output:**

```js
Data received
Processing data
```

Each `.then()` returns a new promise.

## Promise Error Handling

Errors can be handled using `.catch()`.

**Example:**

```js
const promise = new Promise((resolve, reject) => {
  reject("Something went wrong");
});

promise
  .then((res) => {
    console.log(res);
  })
  .catch((err) => {
    console.log(err);
  });
```

**Output:**

```js
Something went wrong
```

## Promise.finally()

`finally()` runs regardless of success or failure.

**Example:**

```js
fetchData()
  .then((data) => console.log(data))
  .catch((err) => console.log(err))
  .finally(() => console.log("Done"));
```

## Promise Static Methods

JavaScript provides useful static methods.

## Promise.all()

Runs multiple promises in parallel.

```js
const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3]).then((values) => {
  console.log(values);
});
```

**Output:**

```js
[1, 2, 3];
```

If any **promise fails**, the entire operation fails.

## Promise.race()

Returns the first settled promise.

```js
const p1 = new Promise((res) => setTimeout(res, 2000, "slow"));
const p2 = new Promise((res) => setTimeout(res, 500, "fast"));

Promise.race([p1, p2]).then(console.log);
```

**Output:**

```js
fast;
```

## Promise.allSettled()

Waits for **all promises**, regardless of success or failure.

```js
Promise.allSettled([Promise.resolve("Success"), Promise.reject("Error")]).then(
  console.log,
);
```

**Output:**

```js
[
  { status: "fulfilled", value: "Success" },
  { status: "rejected", reason: "Error" },
];
```

## Promise.any()

Returns the first **fulfilled** promise.

```js
Promise.any([
  Promise.reject("Error 1"),
  Promise.resolve("Success"),
  Promise.resolve("Another success"),
]).then(console.log);
```

**Output:**

```js
Success;
```

## Common Mistakes

**1. Callback inside `.then()`**

Bad:

```js
fetchData().then((data) => {
  setTimeout(() => console.log(data), 1000);
});
```

Better:

```js
fetchData()
  .then((data) => {
    return new Promise((resolve) => {
      setTimeout(() => resolve(data), 1000);
    });
  })
  .then(console.log);
```

**2. Forgetting return in chains**

Bad:

```js
fetchData()
  .then((data) => {
    processData(data);
  })
  .then(console.log);
```

Better:

```js
fetchData()
  .then((data) => {
    return processData(data);
  })
  .then(console.log);
```

## Real World Example (API)

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```

## Summary

**Key points:**

- Promise handles **asynchronous operations**

**Three states:**

- pending

- fulfilled

- rejected

**Main methods:**

- `.then()`

- `.catch()`

- `.finally()`

**Static methods:**

- `Promise.all()`

- `Promise.race()`

- `Promise.allSettled()`

- `Promise.any()`

Promises are the **foundation for async/await**, which makes asynchronous code easier to write and read.
