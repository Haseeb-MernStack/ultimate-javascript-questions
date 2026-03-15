# Debounce and Throttle in JavaScript

**Debounce** and **Throttle** are techniques used to **control how often a function executes**, especially when events fire repeatedly.

Common examples:

- Search input
- Window resizing
- Scroll events
- Button clicks
- API calls

These techniques help **improve performance and prevent unnecessary function executions**.

---

# Debounce

**Debouncing** ensures that a function runs **only after a certain delay has passed since the last event**.

If the event keeps triggering, the timer resets.

Example:

User typing in a search box → API request should run **after the user stops typing**.

---

# Debounce Example

```javascript
function debounce(fn, delay) {
  let timer;

  return function (...args) {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn.apply(this, args);
    }, delay);
  };
}
```

**Usage example:**

```javascript
const search = debounce(function (query) {
  console.log("Searching for:", query);
}, 500);

search("j");
search("ja");
search("jav");
search("java");
```

**Output (after delay):**

```javascript
Searching for: java
```

Only the last call executes.

## Real World Example (Search Input)

```javascript
const input = document.querySelector("#search");

const handleSearch = debounce((event) => {
  console.log("Searching:", event.target.value);
}, 500);

input.addEventListener("input", handleSearch);
```

This prevents **API** calls on every keystroke.

## Throttle

Throttling ensures that a function runs at most once within a specified time interval.

**Example:**

Scrolling a page → run a function every 200ms instead of every scroll event.

## Throttle Example

```javascript
function throttle(fn, limit) {
  let waiting = false;

  return function (...args) {
    if (!waiting) {
      fn.apply(this, args);
      waiting = true;

      setTimeout(() => {
        waiting = false;
      }, limit);
    }
  };
}
```

**Usage:**

```javascript
const logScroll = throttle(() => {
  console.log("Scrolling...");
}, 1000);

window.addEventListener("scroll", logScroll);
```

This limits the function to once **every 1 second.**

## Debounce vs Throttle

**Example timeline:**

```javascript
User typing quickly:

Debounce → Only last event runs
Throttle → Runs periodically
```

## Visual Example

**Typing event:**

```javascript
Typing: a b c d e

Debounce → execute after user stops typing

Throttle → execute every X milliseconds
```

## Real World Use Cases

**Debounce**

- Search inputs

- Form validation

- Auto-save features

**Throttle**

- Scroll events

- Window resizing

- Game loops

- Mouse movement tracking

## Libraries That Use This Concept

Many libraries provide debounce/throttle utilities:

- Lodash (`_.debounce`, `_.throttle`)

- Underscore.js

- RxJS

**Example with Lodash:**

```javascript
import debounce from "lodash/debounce";

const debouncedSearch = debounce(searchFunction, 500);
```

## Summary

**Debounce:**

- Runs after events stop

- Prevents repeated executions

- Ideal for search inputs and API calls

**Throttle:**

- Runs at fixed intervals

- Limits execution frequency

- Ideal for scroll and resize events

Both techniques are important for **performance optimization** in **JavaScript applications**.
