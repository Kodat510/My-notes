---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# Passing Arguments to Functions in C++

C++ provides three fundamental ways to pass arguments into a function, plus modifiers (`const`, pointers, universal references) that combine with them. Understanding *what gets copied* and *who owns the memory* is the core of this topic.

---

## 1. Pass by Value (Pass by Copy)

The function receives a **copy** of the argument. Changes inside the function do not affect the caller's variable.

```cpp
void increment(int x) {
    x = x + 1;   // modifies the local copy only
}

int main() {
    int a = 5;
    increment(a);
    // a is still 5
}
```

**Characteristics:**

- **Safe:** The original variable cannot be accidentally modified.
- **Costly for large objects:** Passing `std::vector`, `std::string`, or custom classes by value triggers a copy constructor, which can be expensive.
- **Ideal for small types:** Use this for primitives like `int`, `double`, `char`, and `bool`.

```cpp
double square(double x) {
    return x * x;
}
```

---

## 2. Pass by Reference

The function receives an **alias** to the original variable—no copy is made. Changes inside the function _do_ affect the caller's variable.

```cpp
void increment(int& x) {
    x = x + 1;   // modifies the caller's variable directly
}

int main() {
    int a = 5;
    increment(a);
    // a is now 6
}
```

**Characteristics:**

- **Efficient:** No copy overhead; it acts like a hidden pointer using standard variable syntax.
- **Mutation:** Necessary when the function must modify caller data (e.g., `swap(a, b)`).
- **Constraint:** Arguments must be lvalues (actual variables); you cannot bind a non-const reference to a temporary like `increment(5);`.

### 2a. Pass by Reference-to-`const`

The standard way to pass **large objects that should not be modified**.

```cpp
void printName(const std::string& name) {
    std::cout << name << std::endl;
    // name = "hacked"; // Compile error: name is const
}
```

**This is the default choice for passing large objects (strings, vectors, classes) when only read access is required.** It combines reference performance with value safety.

| Pass by...                   | Copies data? | Can modify caller's data? | Typical use case                                      |
| ---------------------------- | :----------: | :-----------------------: | ----------------------------------------------------- |
| Value                        |     Yes      |            No             | Small types (`int`, `double`)                         |
| Reference (`T&`)             |      No      |            Yes            | Modifying caller's variable                          |
| Const Reference (`const T&`) |      No      |            No             | Large read-only objects (`std::string`, etc.)        |

---

## 3. Pass by Pointer

The function receives the **address** of the variable. You must dereference it to access or modify the value.

```cpp
void increment(int* x) {
    if (x!= nullptr) *x = *x + 1; // Dereferencing to modify caller's data
}

int main() {
    int a = 5;
    increment(&a);   // Must pass the address explicitly
    // a is now 6
}
```

**Characteristics:**

- **Explicit Syntax:** Requires `&` at the call site and `*` inside the function.
- **Nullability:** Pointers can be `nullptr`, making them useful for optional arguments (unlike references).
- **Use cases:** Interfacing with C APIs, handling optional values, or performing pointer arithmetic.

### Pointer to const vs Const Pointer

```cpp
void printValue(const int* x) { // The value being pointed to is constant
    std::cout << *x << std::endl;
}
```

---

## 4. Passing Arrays

Raw C-style arrays decay into pointers when passed to functions, meaning size information is lost unless passed separately.

```cpp
void printArray(int arr[], int size) {   // 'arr' decays to 'int*'
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
}
```

**Modern C++ Recommendation:** Prefer `std::vector` or `std::array` passed by reference over raw arrays.

---

## Decision Guide

| Situation                                                    | Recommended approach                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| Small, cheap type (`int`, `double`, `bool`)                  | Pass by value                                                            |
| Large object (read-only)                                     | `const T&`                                                               |
| Large object (must modify caller's data)                     | `T&`                                                                     |
| Argument is optional / may not exist                         | Pointer (`T*`, possibly `nullptr`)                                       |
| Function takes ownership of a temporary                      | Rvalue reference (`T&&`) with `std::move`                                |

---

## Common Pitfalls & Practice Problems

### Common Pitfalls
1. **Unintentional Copying:** Passing large objects by value instead of `const&`. 
2. **Dangling References:** Returning a reference to a local variable (the local object is destroyed upon return).
3. **Null Dereferencing:** Forgetting that pointers can be `nullptr` while references cannot.

### Practice Problems (Test Your Knowledge)

1.  **Identify the Bug:** In the following code, what happens when `getVal()` finishes? Why is this dangerous?
    ```cpp
    int& getVal() { int x = 42; return x; } 
    ```
2.  **Efficiency Check:** Given a function `void process(std::vector<std::string> data)`, rewrite the signature to avoid unnecessary copying while ensuring the original vector remains unchanged.
3.  **Pointer vs Reference:** Write a function that takes an integer and increments it *only if* the provided argument is not "null". Use the appropriate parameter type for nullability. 
4.  **Array Decay:** Given `void func(int arr[])`, explain why calling `sizeof(arr)` inside this function will return different results than calling `sizeof` on an array declared in `main()`. How do you fix it?
5.  **Const Correctness:** Fix the following code so that it compiles and correctly prevents modification of the original object: ```cpp
    void display(std::string& s) { std::cout << s; } // Make this read-only only */ ```