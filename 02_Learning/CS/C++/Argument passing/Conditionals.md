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

Some compilers warn about this; if unsure, write the comparison as `10 == x` so an accidental `=` becomes a compile error instead of a silent bug.

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

### Short-Circuit Evaluation

`&&` and `||` **stop evaluating as soon as the result is known**. This matters both for performance and for safety.

```cpp
// Safe: if ptr is nullptr, the left side is false, so *ptr is NEVER evaluated
if (ptr != nullptr && *ptr > 0) {
    // ...
}

// Safe: if isValid() is false, expensiveCheck() never runs
if (isValid() && expensiveCheck()) {
    // ...
}
```

This pattern (null/guard check first, real check second) is extremely common — order matters.

---

## 3. Combining Relational + Logical Operators

You'll typically nest these together for real conditions.

```cpp
int temperature = 30;
bool isRaining = false;

if ((temperature > 25 && temperature < 35) && !isRaining) {
    std::cout << "Good day for a run";
}
```

**Operator precedence** (highest to lowest, for the operators covered here):

1. `!` (NOT)
2. `<`, `<=`, `>`, `>=`
3. `==`, `!=`
4. `&&`
5. `||`

Because relational operators bind tighter than `&&`/`||`, you often don't strictly need parentheses — but use them anyway for readability:

```cpp
// Technically equivalent, but the parenthesized version is clearer
if (a > 5 && b < 10)
if ((a > 5) && (b < 10))
```

---

## 4. Bitwise Operators (Not the Same as Logical!)

These operate on individual bits, not on the boolean truth-value of an expression. They're a common source of bugs when confused with `&&`/`||`.

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

`&` and `&&` are **not interchangeable**: `&` does not short-circuit, and it works bit-by-bit on integers rather than treating the whole expression as one truth value.

```cpp
if (a & b) { ... }   // bitwise AND on integer values, no short-circuit
if (a && b) { ... }  // logical AND on truthiness, short-circuits
```

---

## 5. The Ternary (Conditional) Operator `?:`

Not an `if` block itself, but a compact expression-level alternative for simple cases.

```cpp
int a = 5, b = 10;
int max = (a > b) ? a : b;

std::cout << (score >= 60 ? "Pass" : "Fail");
```

Equivalent to:

```cpp
int max;
if (a > b) {
    max = a;
} else {
    max = b;
}
```

Best used for simple value selection, not for complex branching logic.

---

## 6. Implicit Conversions in Conditions

Any expression convertible to `bool` can sit in an `if`, not just relational/logical results.

```cpp
int count = 0;
if (count) {           // false, since 0 converts to false
    // ...
}

int* ptr = nullptr;
if (ptr) {              // false, since nullptr converts to false
    // ...
}

std::string s = "hi";
if (!s.empty()) {       // .empty() returns bool directly
    // ...
}
```

|Type|Falsy value|Truthy values|
|---|---|---|
|Integer types|`0`|any nonzero value|
|Pointers|`nullptr` / `0`|any non-null address|
|`bool`|`false`|`true`|
|`std::string`/containers|(no implicit bool conversion — use `.empty()`)|—|

---

## 7. `if` with Initializer (C++17)

Lets you scope a variable to just the `if`/`else` chain — useful to avoid leaking helper variables into the outer scope.

```cpp
if (auto it = myMap.find(key); it != myMap.end()) {
    std::cout << it->second;
} else {
    std::cout << "Not found";
}
// 'it' does not exist here
```

---

## 8. `switch` as an Alternative

When you're comparing one variable against many discrete values with `==`, a `switch` is often cleaner than a long `if`/`else if` chain.

```cpp
switch (grade) {
    case 'A':
        std::cout << "Excellent";
        break;
    case 'B':
        std::cout << "Good";
        break;
    default:
        std::cout << "Needs improvement";
}
```

`switch` only supports equality against integral/enum/char constants — it cannot express ranges (`score >= 90`) or arbitrary boolean logic the way `if` can.

---

## Quick Reference Table

|Category|Operators|Short-circuits?|Produces|
|---|---|:-:|---|
|Relational|`== != > < >= <=`|N/A|`bool`|
|Logical|`&& \| !`|Yes (`&&`, `\|`)|`bool`|
|Bitwise|`& \| ^ ~ << >>`|No|integer|
|Ternary|`?:`|N/A (only one branch evaluated)|value of either branch|

---

## Common Pitfalls

1. **`=` vs `==`** — assignment inside a condition compiles and silently does the wrong thing.
2. **`&`/`|` vs `&&`/`||`** — bitwise operators don't short-circuit and operate bit-by-bit, not on overall truthiness.
3. **Comparing floating-point values with `==`** — due to rounding error, prefer a tolerance check:
    
    ```cpp
    if (std::abs(a - b) < 1e-9) { /* "equal enough" */ }
    ```
    
4. **Forgetting short-circuit order matters** — always put the guard/null-check condition first in `&&` chains.
5. **Dangling `if` without braces** — only the very next statement belongs to the `if`; missing braces around multi-line blocks is a classic bug source. Always use `{}` even for single statements.