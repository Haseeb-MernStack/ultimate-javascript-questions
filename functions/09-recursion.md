# Recursion in JavaScript

**Recursion** is a technique where a function **calls itself** in order to solve a problem.

A recursive function breaks a problem into **smaller subproblems** until it reaches a **base case**.

A recursion must always have:

1. **Base Case** → stops the recursion
2. **Recursive Case** → function calls itself

---

# Basic Example

```javascript
function countDown(n) {
  if (n === 0) {
    console.log("Done!");
    return;
  }

  console.log(n);
  countDown(n - 1);
}

countDown(5);
```

**Output**

```javascript
5
4
3
2
1
Done!
```

**Here:**

- The function calls itself

- It stops when n === 0 (base case)

## Example: Factorial

The factorial of a number is:

```javascript
n! = n * (n - 1)!
```

**Example:**

```javascript
5! = 5 × 4 × 3 × 2 × 1
```

**Recursive solution:**

```javascript
function factorial(n) {
  if (n === 1) {
    return 1;
  }

  return n * factorial(n - 1);
}

console.log(factorial(5));
```

**Output**

```javascript
120;
```

## Visualizing Recursion

**Calling:**

```javascript
factorial(5);
```

**Expands to:**

```javascript
5 * factorial(4);
5 * 4 * factorial(3);
5 * 4 * 3 * factorial(2);
5 * 4 * 3 * 2 * factorial(1);
```

Then it resolves back up the stack.

## Example: Fibonacci Sequence

**Fibonacci sequence:**

```javascript
0, 1, 1, 2, 3, 5, 8...
```

**Recursive implementation:**

```javascript
function fibonacci(n) {
  if (n <= 1) {
    return n;
  }

  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(6));
```

**Output**

```javascript
8;
```

## Recursion vs Loop

**Example using a loop:**

```javascript
function sum(n) {
  let total = 0;

  for (let i = 1; i <= n; i++) {
    total += i;
  }

  return total;
}
```

**Recursive version:**

```javascript
function sum(n) {
  if (n === 1) {
    return 1;
  }

  return n + sum(n - 1);
}
```

Both achieve the same result.

## Call Stack in Recursion

Each recursive call is added to the call stack.

**Example:**

```javascript
function greet(n) {
  if (n === 0) return;

  console.log("Hello");
  greet(n - 1);
}

greet(3);
```

The call stack grows until the base case is reached.

## Recursion Problems

Recursion can cause:

**Stack Overflow**

If there is no base case, recursion will run infinitely.

**Example:**

```javascript
function loop() {
  loop();
}

loop();
```

This will crash the program.

## When Recursion Is Useful

**Recursion is useful for:**

- Tree traversal

- Graph algorithms

- Divide and conquer algorithms

- File system traversal

- Backtracking problems

**Example use cases:**

- Binary trees

- Depth-first search (DFS)

- Parsing nested structures

## Summary

Recursion is a technique where:

- A function calls itself

- A base case stops the recursion

- Problems are broken into smaller parts

**Structure of recursion:**

```javascript
function recursiveFunction() {
  if (baseCase) return;

  recursiveFunction();
}
```

Recursion is widely used in **algorithms**, **data structures**, and **functional programming**.
