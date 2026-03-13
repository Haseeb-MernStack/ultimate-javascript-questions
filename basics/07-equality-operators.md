# Equality Operators in JavaScript

JavaScript provides **two main equality operators** to compare values:

1. Loose Equality (`==`)
2. Strict Equality (`===`)

These operators behave differently when comparing values.

---

# 1. Loose Equality (==)

The loose equality operator compares **values after performing type coercion**.

This means JavaScript may **automatically convert data types** before comparison.

**Example**:

```javascript
console.log(5 == "5");
```

**Output**:

```javascript
true;
```

Why?

JavaScript converts **"5"** into a number.

```javascript
5 == 5;
```

## More Examples of Loose Equality

```javascript
console.log(true == 1);
console.log(false == 0);
```

**Output**:

```javascript
true;
true;
```

**Because**:

```javascript
true  → 1
false → 0
```

Example with **null** and **undefined**:

```javascript
console.log(null == undefined);
```

**Output**:

```javascript
true;
```

Loose equality treats them as equal.

## 2. Strict Equality (===)

Strict equality compares both value and type.

It does NOT perform type coercion.

**Example**:

```javascript
console.log(5 === "5");
```

**Output**:

```javascript
false;
```

**Because**:

```javascript
Number !== String;
```

## More Examples of Strict Equality

```javascript
console.log(true === 1);
console.log(false === 0);
```

**Output**:

```javascript
false;
false;
```

Because the types are different.

## Real Example

Imagine checking a user's age:

```javascript
let age = "18";

if (age == 18) {
  console.log("Access granted");
}
```

**Output**:

```javascript
Access granted
```

Because **"18"** becomes **18**.

## Using strict equality:

```javascript
if (age === 18) {
  console.log("Access granted");
}
```

**Output**:

```javascript
No output
```

Because **"18"** is a string.

## Important JavaScript Interview Examples

These examples often confuse developers.

**Example 1**

```javascript
console.log([] == false);
```

**Output**:

```javascript
true;
```

**Explanation**:

```javascript
[] → "" → 0
false → 0
```

**So**:

```javascript
0 == 0;
```

**Example 2**

```javascript
console.log("" == 0);
```

**Output**:

```javascript
true;
```

**Because**:

```javascript
"" → 0
```

**Example 3**

```javascript
console.log(null === undefined);
```

**Output**:

```javascript
false;
```

**But**:

```javascript
console.log(null == undefined);
```

**Output**:

```javascript
true;
```

## Best Practice

Always prefer strict equality (**===**).

Why?

- `Avoids unexpected type conversions`

- `Makes code more predictable`

- `Reduces bugs`

**Example**:

```javascript
if (value === 10) {
  console.log("Correct value");
}
```

## Key Points

```javascript
== performs type coercion

=== compares value and type

Strict equality is safer and recommended

Loose equality can cause unexpected results
```
