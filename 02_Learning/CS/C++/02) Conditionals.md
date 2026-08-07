---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# If statement

- The if statement works basically the same in Python and C++.
- When there are two separate `if` statements, **both** conditions are checked independently.
- The major difference between `if` and `else if` is that `else if` won't be checked if the preceding `if` condition is satisfied.
- In Python, we use `elif` for multiple conditions, whereas in C++ we use `else if`.
- The `else` keyword functions the same way in both Python and C++.
- Starting a new `if` statement begins a new, independent conditional chain.
- **Example**: If Condition 1 is true, Condition 2 is skipped. However, Conditions 4 & 5 belong to a separate chain (started by Condition 3) and are evaluated independently.

```cpp
// ==================== CHAIN A ====================
if (Condition 1) { 
    // Block 1
} 
else if (Condition 2) { 
    // Block 2
} 
// =================================================


// ==================== CHAIN B ====================
if (Condition 3) { 
    // Block 3
} 
else if (Condition 4) { 
    // Block 4
} 
else if (Condition 5) { 
    // Block 5
}
// =================================================
```

# Else if statement

- The `else if` statement improves performance by skipping unnecessary condition checks once a match is found.
- An `else if` block executes **only** if all preceding `if` / `else if` conditions in the same chain are false.
- When multiple independent `if` statements are present (separate chains), **each one is checked** regardless of previous results.
- Evaluation of independent `if` statements occurs regardless of whether preceding conditions in other chains were true.

# Else statement

- The `else` statement handles scenarios not captured by the `if` or `else if` conditions in the same chain.
- Its scope covers all cases not explicitly handled by preceding conditions in that specific chain.
- Commonly used for default logic, error handling, or handling unexpected [[01) Input & Output|inputs]].

---

# Practice Problems (C++ `if` / `else if` / `else`)

**Scope**: Basic conditional logic, chaining (`else if`), independent chains, and `else` usage. No loops, functions, or complex data structures required.

---

### Problem 1: Grade Classifier (Basic Chaining)
Write a program that reads an integer `score` (0–100) and prints the letter grade using an `if-else if-else` chain:
- 90–100: `A`
- 80–89: `B`
- 70–79: `C`
- 60–69: `D`
- 0–59: `F`
- Otherwise: `Invalid Score`

**Constraint**: Use a single `if-else if-else` chain.

---

### Problem 2: Independent Checks (Multiple Independent `if`s)
Write a program that reads an integer `n` and prints messages based on **independent** properties. Check **all** that apply (use separate `if` statements, not `else if`):
- If divisible by 3: print `"Fizz"`
- If divisible by 5: print `"Buzz"`
- If even: print `"Even"`
- If positive: print `"Positive"`

**Example**: Input `6` → Output: `Fizz`, `Even`, `Positive` (each on new line).

---

### Problem 3: Leap Year Checker (Logical Operators in Condition)
Write a program that reads a `year` (integer) and prints `"Leap Year"` or `"Common Year"`.
Rules (Gregorian calendar):
- Divisible by 400 → Leap Year
- Divisible by 100 → Common Year
- Divisible by 4 → Leap Year
- Otherwise → Common Year

**Constraint**: Implement using a single `if-else if-else` chain with logical operators (`&&`, `||`) allowed inside conditions.

---

### Problem 4: Menu Calculator (Switch-like `if-else if` Chain)
Simulate a simple calculator menu. Read two doubles `a`, `b` and an integer `op`:
- `1`: Add (`a + b`)
- `2`: Subtract (`a - b`)
- `3`: Multiply (`a * b`)
- `4`: Divide (`a / b`, check division by zero → print `"Error: Division by zero"`)
- Other: `"Invalid Operation"`

**Constraint**: Use `if-else if-else` chain. Print result with 2 decimal places for valid ops.

---

### Problem 5: Quadrant & Axis Detector (Compound Conditions)
Read two integers `x` and `y`. Print the location of the point using **independent `if` statements** (check all that apply):
- If `x > 0 && y > 0`: print `"Quadrant I"`
- If `x < 0 && y > 0`: print `"Quadrant II"`
- If `x < 0 && y < 0`: print `"Quadrant III"`
- If `x > 0 && y < 0`: print `"Quadrant IV"`
- If `x == 0 && y == 0`: print `"Origin"`
- If `x == 0 && y != 0`: print `"Y-Axis"`
- If `x != 0 && y == 0`: print `"X-Axis"`

**Constraint**: Use **independent `if` statements** (not `else if`) so that points on axes print both axis labels if logic allows (though logic here makes them mutually exclusive, the practice is using independent `if`s).

---

**Compilation Tip**: Compile with `g++ -std=c++17 -Wall -Wextra -pedantic -o prog main.cpp`