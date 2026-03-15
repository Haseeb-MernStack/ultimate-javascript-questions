# Error Handling in Asynchronous JavaScript

Error handling is a **critical part of production-quality JavaScript**.
When working with asynchronous code (Promises, async/await, fetch), errors can occur due to:

- Network failures
- Server errors
- Invalid responses
- Unexpected bugs in code

A good developer must know **how to properly detect, handle, and propagate errors**.

---

# Types of Errors in JavaScript

JavaScript errors generally fall into three categories:

| Type           | Description                              |
| -------------- | ---------------------------------------- |
| Syntax Errors  | Mistakes in code syntax                  |
| Runtime Errors | Errors that occur during execution       |
| Logical Errors | Code runs but produces incorrect results |

Example:

```js
console.log(user.name);
```

If `user` is undefined → **runtime error**.

---

# Handling Errors with Promises

Promises handle errors using `.catch()`.

Example:

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    const success = false;

    if (success) {
      resolve("Data loaded");
    } else {
      reject("Failed to load data");
    }
  });
}

fetchData()
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

Output:

```
Failed to load data
```

---

# Error Propagation in Promise Chains

Errors automatically propagate through the promise chain.

Example:

```js
Promise.resolve()
  .then(() => {
    throw new Error("Something went wrong");
  })
  .then(() => {
    console.log("This will not run");
  })
  .catch((error) => {
    console.log(error.message);
  });
```

Output:

```
Something went wrong
```

---

# Using try/catch with Async/Await

When using `async/await`, errors should be handled with **try/catch**.

Example:

```js
async function loadData() {
  try {
    const response = await fetch("/api/data");
    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}
```

This pattern is **standard in production applications**.

---

# Throwing Custom Errors

You can throw custom errors using `throw`.

Example:

```js
function withdraw(balance, amount) {
  if (amount > balance) {
    throw new Error("Insufficient balance");
  }

  return balance - amount;
}

try {
  withdraw(100, 200);
} catch (error) {
  console.log(error.message);
}
```

Output:

```
Insufficient balance
```

---

# Handling HTTP Errors (Fetch Example)

Fetch does **not automatically throw errors for HTTP failures**.

Example:

```js
async function getUser() {
  try {
    const response = await fetch("/api/user");

    if (!response.ok) {
      throw new Error("Failed to fetch user");
    }

    const data = await response.json();

    return data;
  } catch (error) {
    console.error(error);
  }
}
```

Always check:

```js
response.ok;
```

---

# Global Error Handling

Sometimes errors happen outside normal flow.

JavaScript provides global handlers.

---

## Browser: Global Error

```js
window.onerror = function (message, source, lineno, colno, error) {
  console.error("Global error:", message);
};
```

---

## Browser: Unhandled Promise Rejection

```js
window.addEventListener("unhandledrejection", (event) => {
  console.error("Unhandled promise rejection:", event.reason);
});
```

---

# Node.js Error Handling

Node.js provides process-level handlers.

---

## Unhandled Promise Rejection

```js
process.on("unhandledRejection", (reason, promise) => {
  console.error("Unhandled Rejection:", reason);
});
```

---

## Uncaught Exception

```js
process.on("uncaughtException", (error) => {
  console.error("Uncaught Exception:", error);
});
```

These help prevent application crashes.

---

# Production Pattern: Centralized Error Handler

Example API helper:

```js
async function apiRequest(url, options = {}) {
  try {
    const response = await fetch(url, options);

    if (!response.ok) {
      throw new Error(`HTTP Error: ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error("API Error:", error);
    throw error;
  }
}
```

Usage:

```js
try {
  const users = await apiRequest("/api/users");
  console.log(users);
} catch (error) {
  console.log("Failed to load users");
}
```

---

# Creating Custom Error Classes

Large applications often create **custom error types**.

Example:

```js
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}

function validateUser(user) {
  if (!user.email) {
    throw new ValidationError("Email is required");
  }
}

try {
  validateUser({});
} catch (error) {
  console.log(error.name);
  console.log(error.message);
}
```

Output:

```
ValidationError
Email is required
```

---

# Logging Errors

In production applications, errors should be **logged**.

Common tools:

- server logs
- monitoring tools
- error tracking services

Example:

```js
console.error({
  message: error.message,
  stack: error.stack,
  time: new Date(),
});
```

---

# Best Practices

### 1. Always handle promise errors

Use `.catch()` or `try/catch`.

---

### 2. Do not ignore errors

Bad practice:

```js
.catch(() => {})
```

---

### 3. Use custom error messages

Helpful for debugging.

---

### 4. Separate user errors vs system errors

Example:

- Validation error → user input issue
- Server error → system problem

---

### 5. Log errors in production

Never silently fail.

---

# Common Mistakes

### Missing try/catch in async function

Bad:

```js
async function load() {
  const data = await fetch("/api/data");
}
```

Correct:

```js
async function load() {
  try {
    const data = await fetch("/api/data");
  } catch (error) {
    console.error(error);
  }
}
```

---

# Summary

Key concepts:

- Promises use `.catch()` for errors
- async/await uses `try...catch`
- Fetch does not throw HTTP errors automatically
- Always check `response.ok`
- Global handlers catch unexpected errors
- Custom error classes improve debugging
- Production apps must log errors

Error handling ensures your application is **stable, debuggable, and production-ready**.

---
