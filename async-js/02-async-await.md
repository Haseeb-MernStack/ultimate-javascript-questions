# Async / Await in JavaScript

`async/await` is a modern way to work with **Promises** in JavaScript.
It makes asynchronous code **look synchronous**, which improves readability and maintainability.

Async/await was introduced in **ES2017 (ES8)** and is now the **standard way to write asynchronous code** in modern JavaScript and Node.js.

---

# Why Async / Await?

Before async/await, developers used:

- Callbacks
- Promise chains (`.then()`)

These approaches can become difficult to read when multiple asynchronous operations are involved.

**Example using Promises:**

```js
fetchUser()
  .then((user) => fetchPosts(user.id))
  .then((posts) => fetchComments(posts[0].id))
  .then((comments) => console.log(comments))
  .catch((err) => console.error(err));
```

Using `async/await`, the same logic becomes much cleaner:

```js
async function getComments() {
  try {
    const user = await fetchUser();
    const posts = await fetchPosts(user.id);
    const comments = await fetchComments(posts[0].id);

    console.log(comments);
  } catch (error) {
    console.error(error);
  }
}
```

---

# Async Functions

An **async function** always returns a **Promise**.

Syntax:

```js
async function myFunction() {
  return "Hello";
}
```

Example:

```js
async function greet() {
  return "Hello World";
}

greet().then(console.log);
```

Output:

```
Hello World
```

Even though we return a **string**, **JavaScript** automatically wraps it inside a **Promise**.

Equivalent to:

```js
function greet() {
  return Promise.resolve("Hello World");
}
```

---

# Await Keyword

The `await` keyword pauses execution until a Promise is resolved.

It can **only be used inside an async function**.

Example:

```js
function delay() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Done"), 2000);
  });
}

async function run() {
  const result = await delay();
  console.log(result);
}

run();
```

Output after 2 seconds:

```
Done
```

---

# Converting Promise Code → Async/Await

Promise version:

```js
fetchData()
  .then((data) => processData(data))
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

Async/Await version:

```js
async function handleData() {
  try {
    const data = await fetchData();
    const result = await processData(data);

    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
```

---

# Sequential vs Parallel Execution

Async operations can run **sequentially** or **in parallel**.

Understanding this is important for **performance optimization**.

---

## Sequential Execution

Each task waits for the previous one.

```js
async function sequential() {
  const a = await task1();
  const b = await task2();
  const c = await task3();

  console.log(a, b, c);
}
```

Total time = `task1 + task2 + task3`

---

## Parallel Execution

Tasks start at the same time.

```js
async function parallel() {
  const p1 = task1();
  const p2 = task2();
  const p3 = task3();

  const results = await Promise.all([p1, p2, p3]);

  console.log(results);
}
```

Total time = `max(task1, task2, task3)`

This is **much faster** in many cases.

---

# Looping with Async/Await

Many developers make mistakes when using async/await with loops.

---

## Correct Way (for...of)

```js
async function processUsers(users) {
  for (const user of users) {
    const data = await fetchUser(user);
    console.log(data);
  }
}
```

---

## Avoid Using await in forEach

Incorrect:

```js
users.forEach(async (user) => {
  const data = await fetchUser(user);
  console.log(data);
});
```

`forEach` does not wait for async operations.

---

# Running Multiple Requests

Example:

```js
async function getUsers() {
  const urls = ["/api/user1", "/api/user2", "/api/user3"];

  const requests = urls.map((url) => fetch(url));

  const responses = await Promise.all(requests);

  const data = await Promise.all(responses.map((res) => res.json()));

  console.log(data);
}
```

---

# Top-Level Await

Modern JavaScript modules support **top-level await**.

Example:

```js
const data = await fetch("/api/data");
const result = await data.json();

console.log(result);
```

This only works in **ES modules**.

---

# Error Handling with Async/Await

Use `try...catch`.

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

---

# Async Function Returning Values

Example:

```js
async function add(a, b) {
  return a + b;
}

add(2, 3).then(console.log);
```

Output:

```
5
```

---

# Real Production Example (Node.js)

Example using database query:

```js
async function getUserProfile(userId) {
  try {
    const user = await db.users.findById(userId);
    const posts = await db.posts.find({ userId });

    return {
      user,
      posts,
    };
  } catch (error) {
    throw new Error("Failed to load profile");
  }
}
```

This pattern is commonly used in:

- Express APIs
- Backend services
- Production applications

---

# Best Practices

### 1. Use async/await instead of long promise chains

Cleaner code and easier debugging.

---

### 2. Run independent operations in parallel

Use:

```js
Promise.all();
```

---

### 3. Always handle errors

Use:

```js
try...catch
```

---

### 4. Avoid blocking loops

Use parallel execution where possible.

---

# Summary

Key concepts:

- `async` makes a function return a Promise
- `await` pauses execution until a Promise resolves
- Use `try...catch` for error handling
- Use `Promise.all()` for parallel operations
- Avoid `await` inside `forEach`

`Async/await` makes asynchronous JavaScript **cleaner, safer, and easier to maintain**.

---
