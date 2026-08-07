

---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# Operators in `if` Statements (C++)

`if` blocks evaluate a **condition** that must resolve to something convertible to `bool` (`true`/`false`, or `0`/nonzero for numeric types, or non-null for pointers). This file covers every category of operator you'll use to build those conditions.

```cpp
if (condition) {
    // runs if condition is true
} else if (otherCondition) {
    // runs if condition is false and otherCondition is true
} else {
    // runs if none matched
}
```

---

## 1. Relational (Comparison) Operators

Compare two values, produce a `bool`.

|Operator|Meaning|Example|
|:-:|---|---|
|`==`|Equal to|`a == b`|
|`!=`|Not equal to|`a != b`|
|`>`|Greater than|`a > b`|
|`<`|Less than|`a < b`|
|`>=`|Greater than or equal to|`a >= b`|
|`<=`|Less than or equal to|`a <= b`|

```cpp
int score = 85;
if (score >= 90) {
    std::cout << "A grade";
} else if (score >= 75) {
    std::cout << "B grade";
} else {
    std::cout << "C grade or below";
}
```

**Common pitfall:** using `=` (assignment) instead of `==` (comparison).

```cpp
int x = 5;
if (x = 10) {   // BUG: assigns 10 to x, then evaluates as true (nonzero)
    // this block always runs
}
```

---

## 2. Logical Operators

Combine or invert `bool` expressions.

|Operator|Meaning|Example|
|:-:|---|---|
|`&&`|Logical AND — true only if both sides are true|`a && b`|
|`\|`|Logical OR — true if at least one side is true|`a \| b`|
|`!`|Logical NOT — inverts a bool|`!a`|

```cpp
int age = 20;
bool hasLicense = true;

if (age >= 18 && hasLicense) {
    std::cout << "Can drive";
}

if (age < 13 || age > 65) {
    std::cout << "Eligible for discount";
}

if (!hasLicense) {
    std::cout << "Cannot drive";
}
```

---

## 3. Bitwise Operators (Not the Same as Logical!)

Operate on individual bits, not on the boolean truth-value of an expression.

|Operator|Meaning|
|:-:|---|
|`&`|Bitwise AND|
|`\|`|Bitwise OR|
|`^`|Bitwise XOR|
|`~`|Bitwise NOT|
|`<<`|Left shift|
|`>>`|Right shift|

```cpp
int flags = 0b0110;
int mask  = 0b0100;

if (flags & mask) {       // bitwise AND — checks if that bit is set
    std::cout << "Flag is set";
}
```

---

## 4. Ternary (Conditional) Operator `?:`

Compact expression-level alternative for simple cases.

```cpp
int a = 5, b = 10;
int max = (a > b) ? a : b;

std::cout << (score >= 60 ? "Pass" : "Fail");
```

---

## 5. Implicit Conversions in Conditions

Any expression convertible to `bool` can sit in an `if`.

```cpp
int count = 0;
if (count) {           // false, since 0 converts to false
    // ...
}

int* ptr = nullptr;
if (ptr) {              // false, since nullptr converts to false
    // ...
}
```

---

## Practice Problems

### Problem 1
Write a condition that incorrectly uses `=` instead of `==`. Explain why it fails.

```cpp
int a = 5;
if (a = 5) { ... }  // Fill in the blank
```

### Problem 2
Rewrite the following condition to use short-circuit evaluation safely:
```cpp
if (ptr != nullptr && *ptr > 100) { ... }
```

### Problem 3
Use a bitwise operator to check if the third bit is set in `flags = 0b1011`.

### Problem 4
Convert this `if` block to a ternary expression:
```cpp
if (temperature > 30) {
    mode = "Heat";
} else {
    mode = "Cool";
}
```

### Problem 5
What is falsy in C++? Identify which of these are falsy: `0`, `nullptr`, `false`, `5`, `std::string("")`.
