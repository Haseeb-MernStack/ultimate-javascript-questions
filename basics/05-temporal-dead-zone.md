# Temporal Dead Zone (TDZ) in JavaScript

The **Temporal Dead Zone (TDZ)** is the time between **entering a scope and the variable being declared** where the variable **cannot be accessed**.

It mainly applies to variables declared with:

- `let`
- `const`

If you try to access these variables before their declaration, JavaScript will throw a **ReferenceError**.

---

# Why TDZ Exists

The Temporal Dead Zone was introduced in ES6 to **prevent unexpected bugs** that occurred with `var`.

It forces developers to **declare variables before using them**, making code more predictable and safer.

---

# Example of Temporal Dead Zone

```javascript
console.log(a);

let a = 10;
```

**Output**: ReferenceError: Cannot access 'a' before initialization

Even though **let** variables are hoisted, they are not initialized immediately.

They stay inside the **_Temporal Dead Zone_** until the line where they are declared.

## Visual Representation

```javascript
Start of Scope
     ↓
TDZ begins
     ↓
Variable declared
     ↓
TDZ ends
     ↓
Variable usable
```

## TDZ with const

**const** behaves the same as **let** regarding TDZ.

```javascript
console.log(id);

const id = 123;
```

**Output**: ReferenceError

## TDZ inside Block Scope

TDZ also applies inside blocks.

```javascript
{
  console.log(a);

  let a = 5;
}
```

**Output**: ReferenceError

The variable **a** exists in the block scope but cannot be accessed before its declaration.

## TDZ vs var

**var** does not have a Temporal Dead Zone.

```javascript
console.log(a);

var a = 10;
```

**Output**: undefined

Because **var** variables are hoisted and initialized with undefined.

## Real Example

```javascript
let username = "Malik";

function login() {
  console.log(username);

  let username = "Admin";
}

login();
```

**Output**: ReferenceError

Why?

Because the inner **username** creates a new scope, and until it is declared, it stays inside the **TDZ**.

## TDZ with Functions

**Example**:

```javascript
function test() {
  console.log(a);
  let a = 20;
}

test();
```

**Output**: ReferenceError

The variable **a** exists in the function scope but cannot be accessed until after declaration.

## Key Points

```javascript
TDZ applies to let and const

TDZ prevents variables from being used before declaration

Accessing variables in TDZ causes a ReferenceError

var does not have TDZ

TDZ helps write safer and more predictable code
```
