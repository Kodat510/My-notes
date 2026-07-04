---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# If statement:-

- The if statement works basically the same in Python and C++.
- When there are 2 if conditions, it will check both of them.
- The major difference between if and else if is that it won't check an else if when the if condition is satisfied
- In Python, we use "elif" for multiple conditions, whereas in C++ we use "else if".
- The "else" keyword functions in the same way in both Python and C++.
- When there are multiple if and else if conditions we start a new boundary with an if condition
- If condition 1 is true it will only skip condition 2 for you conditions 4 & 5 are bound to condition 3 
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

# Else if statement:-

- The Else if statement is used to improve performance in C++ code.
- The Else if statement won't execute if the initial 'if' condition is true.
- When multiple 'if' conditions are present, each one will be checked.
- The checking of 'if' conditions is regardless of whether the preceding conditions are true or not.
- This means that every 'if' condition will be evaluated, even if a previous condition has already been met.

# Else statement:-

- The else statement is mainly used for scenarios that the if condition or the else if condition did not capture.
- Its scope is wide, covering everything that is not included in the if or else if conditions.
- It is mostly used for basic cases of error handling.
- It is also used for handling unexpected [[01) Input & Output|inputs]] that are not accounted for by the if or else if conditions.