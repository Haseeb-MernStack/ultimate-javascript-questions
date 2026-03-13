# Type Coercion in JavaScript

Type coercion is the **automatic or implicit conversion of values from one data type to another** by JavaScript.

JavaScript is a **dynamically typed language**, meaning variables do not have fixed types. Because of this, JavaScript sometimes converts values automatically.

---

# Types of Type Coercion

There are **two types of coercion**:

1. Implicit Coercion (automatic conversion)
2. Explicit Coercion (manual conversion)

---

# 1. Implicit Type Coercion

Implicit coercion happens when **JavaScript automatically converts data types during operations**.

---

## Example 1: Number + String

```javascript
let result = 5 + "5";

console.log(result);
```

**Output**:

```javascript
55;
```

Why?

JavaScript converts the number **5** into a string.

```javascript
"5" + "5" = "55"
```

## Example 2: String - Number

```javascript
let result = "10" - 5;

console.log(result);
```

**Output**:

```javascript
5;
```

Here JavaScript converts **"10"** into a number.

```javascript
10 - 5 = 5
```

## Example 3: Boolean to Number

```javascript
console.log(true + 1);
console.log(false + 1);
```

**Output**:

```javascript
2;
1;
```

**Because**:

```javascript
true  → 1
false → 0
```

## Example 4: null with Number

```javascript
console.log(null + 5);
```

**Output**:

```javascript
5;
```

**Because**:

```javascript
null → 0
```

## Example 5: undefined with Number

```javascript
console.log(undefined + 5);
```

**Output**:

```javascript
NaN;
```

Because **undefined** cannot be converted into a valid number.

## 2. Explicit Type Coercion

Explicit coercion happens when developers manually convert types.

This is done using functions like:

```javascript
Number();

String();

Boolean();
```

## Convert to Number

```javascript
let str = "100";

let num = Number(str);

console.log(num);
```

**Output**:

```javascript
100;
```

## Convert to String

```javascript
let num = 50;

let str = String(num);

console.log(str);
```

**Output**:

```javascript
"50";
```

## Convert to Boolean

```javascript
console.log(Boolean(1));
console.log(Boolean(0));
```

**Output**:

```javascript
true;
false;
```

## Truthy and Falsy Values

JavaScript converts values to true or false in conditions.

**Falsy Values**

These values become **false**:

```javascript
false;

0;

("");

null;

undefined;

NaN;
```

**Example**:

```javascript
if (0) {
  console.log("Hello");
} else {
  console.log("Falsy value");
}
```

**Output**:

```javascript
Falsy value
```

## Real World Example

Form inputs often return strings.

```javascript
let input = "20";

let total = Number(input) + 10;

console.log(total);
```

**Output**:

```javascript
30;
```

## Without conversion:

```javascript
let input = "20";

console.log(input + 10);
```

**Output**:

```javascript
2010;
```

This is why explicit conversion is important in real applications.

## Key Points

```javascript
Type coercion converts values from one type to another

JavaScript performs implicit coercion automatically

Developers can use explicit coercion for better control

Understanding coercion helps avoid unexpected bugs
```
