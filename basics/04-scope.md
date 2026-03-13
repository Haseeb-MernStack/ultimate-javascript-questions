# JavaScript Scope

Scope determines **where variables are accessible in your code**.

In simple terms:

> Scope defines the **visibility and lifetime of variables**.

---

# Types of Scope in JavaScript

JavaScript has **three main types of scope**:

1. Global Scope
2. Function Scope
3. Block Scope

---

# 1. Global Scope

Variables declared **outside any function or block** are in the global scope.

They can be accessed **anywhere in the program**.

```javascript
let name = "Malik";

function greet() {
  console.log(name);
}

greet(); // Malik
```

⚠️ Avoid using too many global variables because they can cause naming conflicts and bugs.

## 2. Function Scope

Variables declared inside a function are only accessible inside that function.

```javascript
function greet() {
  let message = "Hello World";
  console.log(message);
}

greet();

console.log(message); // Error
```

Here, message exists only inside the function.

## 3. Block Scope

Block scope is created by curly braces **{}**.

Variables declared with **let** and **const** are block scoped.

```javascript
{
  let a = 10;
  const b = 20;

  console.log(a); // 10
  console.log(b); // 20
}

console.log(a); // Error
console.log(b); // Error
```

Outside the block, these variables do not exist.

## var vs let vs const in Scope

**var** behaves differently from **let** and **const**.

**var** is function scoped, not block scoped.

```javascript
{
  var a = 10;
}

console.log(a); // 10
```

But with **let**:

```javascript
{
  let a = 10;
}

console.log(a); // Error
```

This is why modern JavaScript prefers let and const.

## Lexical Scope

JavaScript uses lexical scope, meaning scope is determined by where variables are written in the code.

**Example**:

```javascript
function outer() {
  let name = "Malik";

  function inner() {
    console.log(name);
  }

  inner();
}

outer();
```

**Output**: Malik

The inner function can access variables from its outer scope.

This behavior is the foundation of closures.

## Scope Chain

When JavaScript tries to access a variable, it looks in:

1. Current scope

2. Outer scope

3. Global scope

**Example**:

```javascript
let a = 1;

function outer() {
  let b = 2;

  function inner() {
    let c = 3;

    console.log(a, b, c);
  }

  inner();
}

outer();
```

**Output**: 1 2 3

JavaScript finds variables through the scope chain.

## Real Example

```javascript
let user = "Developer";

function login() {
  let status = "Logged In";

  if (true) {
    let role = "Admin";
    console.log(user);
    console.log(status);
    console.log(role);
  }
}

login();
```

**Accessible variables**:

**user** → global scope

**status** → function scope

**role** → block scope

## Key Points

```javascript
Scope controls where variables can be accessed

JavaScript has global, function, and block scope

var is function scoped

let and const are block scoped

JavaScript follows lexical scope

Scope chain allows nested functions to access outer variables

```
