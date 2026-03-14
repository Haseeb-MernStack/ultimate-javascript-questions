# Memoization in JavaScript

**Memoization** is an optimization technique used to **speed up expensive function calls** by **caching the results** of previous computations.

If the same input occurs again, the function **returns the cached result instead of recalculating it**.

---

# Basic Example (Without Memoization)

```javascript
function square(n) {
  console.log("Calculating...");
  return n * n;
}

console.log(square(5));
console.log(square(5));
```

**Output:**

```javascript
Calculating...
25
Calculating...
25
```

The calculation runs every time.

## Memoization Example

```javascript
function memoizedSquare() {
  const cache = {};

  return function (n) {
    if (cache[n]) {
      console.log("Returning from cache");
      return cache[n];
    }

    console.log("Calculating...");
    const result = n * n;
    cache[n] = result;

    return result;
  };
}

const square = memoizedSquare();

console.log(square(5));
console.log(square(5));
```

**Output:**

```javascript
Calculating...
25
Returning from cache
25
```

The second call uses the cached result.

## How Memoization Works

**Steps:**

1. Store results in a cache object

2. When the function runs, check if the result already exists

3. If it exists → return cached value

4. If not → calculate and store it

## Real World Example (Fibonacci)

The Fibonacci sequence is often used to demonstrate memoization.

**Without memoization:**

```javascript
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}

console.log(fib(10));
```

This approach recalculates many values and becomes **slow for large numbers**.

## Fibonacci with Memoization

```javascript
function memoizedFib() {
  const cache = {};

  function fib(n) {
    if (n in cache) {
      return cache[n];
    }

    if (n <= 1) {
      return n;
    }

    const result = fib(n - 1) + fib(n - 2);
    cache[n] = result;

    return result;
  }

  return fib;
}

const fib = memoizedFib();

console.log(fib(10));
```

This version is much faster because previously computed values are reused.

## Memoization Using Closures

Memoization works well with closures.

**Example:**

```javascript
const memoize = (fn) => {
  const cache = {};

  return function (value) {
    if (value in cache) {
      return cache[value];
    }

    const result = fn(value);
    cache[value] = result;

    return result;
  };
};

const square = memoize((n) => n * n);

console.log(square(4));
console.log(square(4));
```

## Memoization in React

Memoization is commonly used in React to **avoid unnecessary re-renders**.

**Examples:**

- `React.memo`

- `useMemo`

- `useCallback`

**Example:**

```javascript
const expensiveCalculation = useMemo(() => {
  return heavyFunction(data);
}, [data]);
```

## Advantages of Memoization

Memoization provides several benefits:

- Improves performance

- Reduces repeated calculations

- Speeds up recursive algorithms

- Helps optimize expensive operations

## When to Use Memoization

Use memoization when:

- Functions are computationally expensive

- The same inputs are used multiple times

- Performance optimization is needed

## Summary

Memoization is a technique that:

- Stores previous function results

- Returns cached results when the same input occurs

- Improves performance by avoiding repeated calculations

Memoization is commonly used in **algorithms**, **functional programming**, and **React optimization**.
