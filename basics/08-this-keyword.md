# The `this` Keyword in JavaScript

In JavaScript, the `this` keyword refers to **the object that is currently executing the function**.

The value of `this` depends on **how a function is called**, not where it is defined.

---

# Global Context

In the global scope, `this` refers to the **global object**.

In browsers, the global object is `window`.

**Example**:

```javascript
console.log(this);
```

**Output** (in browser):

```javascript
Window {...}
```

## `this` Inside a Function

In a regular function, `this` depends on how the function is called.

**Example**:

```javascript
function greet() {
  console.log(this);
}

greet();
```

In browsers (non-strict mode):

```javascript
Window {...}
```

In strict mode:

```javascript
undefined;
```

## `this` Inside an Object Method

When a function is called as an object method, `this` refers to that object.

**Example**:

```javascript
const user = {
  name: "Malik",
  greet: function () {
    console.log(this.name);
  },
};

user.greet();
```

**Output**:

```javascript
Malik;
```

Here `this` refers to the `user` object.

## `this` in Arrow Functions

Arrow functions do not have their own `this`.

They inherit `this` from the surrounding (lexical) scope.

**Example**:

```javascript
const user = {
  name: "Malik",
  greet: () => {
    console.log(this.name);
  },
};

user.greet();
```

**Output**:

```javascript
undefined;
```

Because arrow functions take `this` from the outer scope, not the object.

## Arrow Function Example with Lexical `this`

```javascript
const user = {
  name: "Malik",
  greet: function () {
    const arrow = () => {
      console.log(this.name);
    };

    arrow();
  },
};

user.greet();
```

**Output**:

```javascript
Malik;
```

Here the arrow function inherits `this` from the `greet` method.

## `this` with Constructor Functions

When using `new`, `this` refers to the newly created object.

**Example**:

```javascript
function User(name) {
  this.name = name;
}

const user1 = new User("Malik");

console.log(user1.name);
```

**Output**:

```javascript
Malik;
```

## `this` with Event Handlers

In event handlers, `this` refers to the element that triggered the event.

**Example**:

```javascript
button.addEventListener("click", function () {
  console.log(this);
});
```

Here `this` refers to the button element.

## `call()`, `apply()`, and `bind()`

These methods allow you to manually control the value of `this`.

**Example**:

```javascript
function greet() {
  console.log(this.name);
}

const user = { name: "Malik" };

greet.call(user);
```

**Output**:

```javascript
Malik;
```

## Key Points

```javascript
this depends on how a function is called

Arrow functions do not have their own this

call, apply, and bind can control this

Understanding this is crucial for advanced JavaScript concepts
```
