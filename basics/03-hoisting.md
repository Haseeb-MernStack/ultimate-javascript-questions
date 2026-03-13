# JavaScript Hoisting

Hoisting is JavaScript's **default behavior of moving declarations to the top of their scope before code execution**.

This means variables and functions can sometimes be used **before they are declared in the code**.

---

# Example of Hoisting

```javascript
console.log(a);

var a = 10;
```

**Output**: undefined

Why?

JavaScript internally interprets it like this:

```javascript
var a;

console.log(a);

a = 10;
```

The declaration is hoisted, but the initialization is not.

## Variable Hoisting

**1. Hoisting with var**

Variables declared with **var** are hoisted and initialized with undefined.

```javascript
console.log(a);

var a = 10;
```

**Output**: undefined

## 2. Hoisting with let

Variables declared with **let** are hoisted but not initialized.

They stay in something called the Temporal Dead Zone (TDZ) until the line where they are declared.

```javascript
console.log(a);

let a = 10;
```

**Output**: ReferenceError: Cannot access 'a' before initialization

## 3. Hoisting with const

**const** behaves the same as **let** regarding hoisting.

```javascript
console.log(a);

const a = 10;
```

**Output**: ReferenceError Function Hoisting

Functions declared with the **function** keyword are fully hoisted.

```javascript
greet();

function greet() {
  console.log("Hello");
}
```

**Output**: Hello

This works because the entire function definition is hoisted.

## Function Expression Hoisting

Function expressions are not **hoisted** the same way.

```javascript
greet();

var greet = function () {
  console.log("Hello");
};
```

**Output**: TypeError: greet is not a function

Why?

Because JavaScript interprets it like this:

```javascript
var greet;

greet();

greet = function () {
  console.log("Hello");
};
```

## Key Points

```javascript
Hoisting moves declarations to the top of the scope

var is initialized with undefined

let and const stay in Temporal Dead Zone

Function declarations are fully hoisted

Function expressions behave like normal variables
```
