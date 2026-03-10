# JavaScript Data Types

JavaScript data types define the **type of data that a variable can hold**.

JavaScript has **two main categories of data types**:

1. Primitive Data Types
2. Non-Primitive (Reference) Data Types

---

# 1. Primitive Data Types

Primitive data types store **single values** and are **immutable**.

There are **7 primitive data types in JavaScript**.

| Type      | Example               |
| --------- | --------------------- |
| String    | "Hello"               |
| Number    | 42                    |
| Boolean   | true / false          |
| Undefined | undefined             |
| Null      | null                  |
| Symbol    | Symbol("id")          |
| BigInt    | 12345678901234567890n |

---

## 1. String

Strings represent **textual data**.

```javascript
let name = "Malik";
let message = "Hello World";

2. Number

Numbers represent numeric values.

let age = 25;
let price = 99.99;

JavaScript numbers include:

Integers

Floating point numbers

3. Boolean

Boolean represents true or false values.

let isLoggedIn = true;
let hasPermission = false;

4. Undefined

A variable that is declared but not assigned a value has the value undefined.

let user;
console.log(user); // undefined

5. Null

null represents an intentional absence of value.

let data = null;

Difference

undefined → value not assigned

null → value intentionally empty

6. Symbol

Symbols create unique identifiers.

const id = Symbol("id");

Each symbol is unique.

7. BigInt

BigInt is used for very large integers beyond the limit of normal numbers.

const bigNumber = 123456789012345678901234567890n;

2. Non-Primitive (Reference) Data Types

These store collections of data and are stored by reference.

Main non-primitive types:

Object

Array

Function

Object

Objects store key-value pairs.

const user = {
name: "Malik",
age: 21
};

Array

Arrays store multiple values in a single variable.

const numbers = [1, 2, 3, 4];

Function

Functions are also objects in JavaScript.

function greet() {
console.log("Hello");
}

Example
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20

Primitive values are copied, not referenced.

Summary

JavaScript has two types of data types.

Primitive

String

Number

Boolean

Undefined

Null

Symbol

BigInt

Non-Primitive

Object

Array

Function
```
