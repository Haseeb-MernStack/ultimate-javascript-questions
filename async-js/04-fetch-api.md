# Fetch API in JavaScript

The **Fetch API** is the modern way to make **HTTP requests** in JavaScript.

It allows JavaScript applications to communicate with servers to:

- retrieve data
- send data
- update data
- delete data

Fetch is **Promise-based** and widely used in:

- Frontend applications (React, Vue, Next.js)
- Node.js (modern versions)
- Browser applications

---

# Basic Syntax

```js
fetch(url, options);
```

- `url` → endpoint you want to request
- `options` → configuration object (method, headers, body, etc.)

Example:

```js
fetch("https://jsonplaceholder.typicode.com/posts");
```

This returns a **Promise**.

---

# Simple GET Request

Example:

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  });
```

Explanation:

1. `fetch()` sends request
2. server responds
3. `.json()` converts response to JavaScript object
4. data becomes usable

Example response:

```json
{
  "userId": 1,
  "id": 1,
  "title": "example title",
  "body": "example body"
}
```

---

# Using Async / Await

Most production applications use **async/await**.

Example:

```js
async function getPost() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");

  const data = await response.json();

  console.log(data);
}

getPost();
```

This code is easier to read compared to `.then()` chains.

---

# Response Object

Fetch returns a **Response object**.

Example:

```js
const response = await fetch("/api/data");

console.log(response);
```

Important properties:

| Property  | Description               |
| --------- | ------------------------- |
| `status`  | HTTP status code          |
| `ok`      | true if status is 200–299 |
| `headers` | response headers          |
| `json()`  | parse JSON                |
| `text()`  | parse text                |

Example:

```js
if (!response.ok) {
  throw new Error("Request failed");
}
```

---

# Sending Data (POST Request)

POST requests are used to **send data to a server**.

Example:

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "Hello",
    body: "Learning Fetch API",
    userId: 1,
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

---

# POST with Async/Await

```js
async function createPost() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      title: "New Post",
      body: "This is a post",
      userId: 1,
    }),
  });

  const data = await response.json();

  console.log(data);
}
```

---

# PUT Request (Update Data)

Example:

```js
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    id: 1,
    title: "Updated Title",
    body: "Updated content",
    userId: 1,
  }),
})
  .then((res) => res.json())
  .then(console.log);
```

---

# DELETE Request

Example:

```js
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "DELETE",
}).then(() => {
  console.log("Post deleted");
});
```

---

# Handling Errors

Fetch only rejects on **network errors**, not HTTP errors.

Example:

```js
async function loadData() {
  try {
    const response = await fetch("/api/data");

    if (!response.ok) {
      throw new Error("Server error");
    }

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}
```

---

# Sending Headers

Headers are used for:

- authentication
- content type
- API keys

Example:

```js
fetch("/api/user", {
  headers: {
    Authorization: "Bearer TOKEN",
    "Content-Type": "application/json",
  },
});
```

---

# Fetch with Query Parameters

Example:

```js
const userId = 5;

fetch(`https://api.example.com/users?id=${userId}`)
  .then((res) => res.json())
  .then(console.log);
```

---

# Fetch Timeout Pattern

Fetch does not support timeouts natively, but you can use `AbortController`.

Example:

```js
const controller = new AbortController();

setTimeout(() => {
  controller.abort();
}, 3000);

fetch("/api/data", {
  signal: controller.signal,
})
  .then((res) => res.json())
  .then(console.log)
  .catch((err) => {
    console.log("Request aborted", err);
  });
```

---

# Fetch Multiple Requests

Example:

```js
async function loadPosts() {
  const urls = ["/api/posts/1", "/api/posts/2", "/api/posts/3"];

  const responses = await Promise.all(urls.map((url) => fetch(url)));

  const data = await Promise.all(responses.map((res) => res.json()));

  console.log(data);
}
```

This approach is **much faster than sequential requests**.

---

# Production Pattern (Reusable Fetch)

Example helper function:

```js
async function api(url, options = {}) {
  const response = await fetch(url, options);

  if (!response.ok) {
    throw new Error("API Error");
  }

  return response.json();
}
```

Usage:

```js
const users = await api("/api/users");

console.log(users);
```

This pattern is used in **production applications**.

---

# Common Mistakes

### Forgetting `await response.json()`

Incorrect:

```js
const data = response.json();
```

Correct:

```js
const data = await response.json();
```

---

### Not checking `response.ok`

Always verify response status.

---

# Summary

Key concepts:

- Fetch API is used for **HTTP requests**
- It returns a **Promise**
- Supports all HTTP methods:
  - GET
  - POST
  - PUT
  - DELETE

- Use `async/await` for cleaner code
- Always check `response.ok`
- Use `Promise.all()` for parallel requests

Fetch API is widely used in **modern web development and production applications**.

---
