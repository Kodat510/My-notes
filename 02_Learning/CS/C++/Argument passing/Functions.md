---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# Passing Arguments to Functions in C++

C++ gives you three fundamental ways to pass arguments into a function, plus a few modifiers (`const`, pointers, universal references) that combine with them. Understanding _what gets copied_ and _who owns the memory_ is the core of this topic.

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

- Safe — the original variable can't be accidentally modified.
- Costly for large objects (e.g. `std::vector`, `std::string`, custom classes), since the entire object is copied, including a call to its copy constructor.
- Fine for small, cheap-to-copy types: `int`, `double`, `char`, `bool`, small structs.

```cpp
double square(double x) {
    return x * x;
}
```

---

## 2. Pass by Reference

The function receives an **alias** to the original variable — no copy is made. Changes inside the function _do_ affect the caller's variable.

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

- No copy overhead — the reference is essentially a hidden pointer under the hood, but you use it with normal variable syntax.
- Necessary when a function needs to modify the caller's data (e.g. `swap(a, b)`).
- Can be dangerous if used carelessly — the function can silently mutate data the caller didn't expect to change.
- The argument at the call site must be an actual variable (an "lvalue"); you cannot bind a plain reference to a temporary like `increment(5);`.

### 2a. Pass by Reference-to-`const`

The most common way to pass **large objects you don't want copied but also don't want modified**.

```cpp
void printName(const std::string& name) {
    std::cout << name << std::endl;
    // name = "hacked"; // would be a compile error — name is const
}
```

**This is the default choice for passing large objects (strings, vectors, custom classes) when the function only needs to read them.** You get the performance of pass-by-reference (no copy) with the safety of pass-by-value (no mutation).

| Pass by...                   | Copies data? | Can modify caller's data? | Typical use case                                      |
| ---------------------------- | :----------: | :-----------------------: | ----------------------------------------------------- |
| Value                        |     Yes      |            No             | Small types (`int`, `double`, `char`)                 |
| Reference (`T&`)             |      No      |            Yes            | Need to modify caller's variable                      |
| Const Reference (`const T&`) |      No      |            No             | Large read-only objects (`string`, `vector`, classes) |

---

## 3. Pass by Pointer

The function receives the **address** of the variable. You must dereference the pointer to access or modify the value.

```cpp
void increment(int* x) {
    *x = *x + 1;   // dereference to modify the caller's variable
}

int main() {
    int a = 5;
    increment(&a);   // must pass the address explicitly
    // a is now 6
}
```

**Characteristics:**

- Similar effect to pass-by-reference (can modify caller's data, avoids copying), but:
    - The syntax is more explicit/verbose (`&a` at call site, `*x` inside the function).
    - Pointers can be `nullptr`, so the function must often check for that — references cannot be null (in valid, well-formed code).
    - Pointers can be reseated to point elsewhere; references are permanently bound to one variable.
- Useful when:
    - The argument is genuinely optional (pass `nullptr` to mean "no value").
    - You're interfacing with C-style APIs.
    - You need to pass arrays (which decay to pointers) or do pointer arithmetic.

### Pointer to const

```cpp
void printValue(const int* x) {
    std::cout << *x << std::endl;
    // *x = 10; // compile error
}
```

---

## 4. Passing Arrays

Arrays decay to pointers when passed to functions — the function never receives size information.

```cpp
void printArray(int arr[], int size) {   // arr is really int*
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
}
```

Prefer `std::vector` or `std::array` with references over raw C-style arrays in modern C++:

```cpp
void printVector(const std::vector<int>& v) {
    for (int x : v) std::cout << x << " ";
}
```

---

## Decision Guide

| Situation                                                    | Recommended approach                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| Small, cheap type (`int`, `double`, `bool`, `char`)          | Pass by value                                                            |
| Large object, function only reads it                         | `const T&`                                                               |
| Large object, function must modify caller's copy             | `T&`                                                                     |
| Argument is optional / may not exist                         | Pointer (`T*`, possibly `nullptr`)                                       |
| Function should take ownership / avoid a copy of a temporary | `T&&` with `std::move`                                                   |
| Generic/template code needing to preserve value category     | Forwarding reference `T&&` + `std::forward`                              |
| C-style array                                                | Decays to pointer — prefer `std::vector`/`std::array` + `const&` instead |

---

## Common Pitfalls

1. **Passing large objects by value unintentionally** — silently copies the whole object every call. Profile-sensitive code should default to `const&` for anything bigger than a pointer.
2. **Returning a reference to a local variable** — the local is destroyed when the function returns, leaving a dangling reference.
    
    ```cpp
    int& badFunction() {    int local = 5;    return local;   // BUG: dangling reference}
    ```
    
3. **Confusing reference and pointer semantics** — a reference must be initialized at declaration and can never be null or reseated; a pointer can be reassigned and can be null.
4. **Using `T&` when you meant `const T&`** — accidentally allows the function to mutate the caller's data when it shouldn't need to.
5. **Using `std::move` on an object you still need** — after `std::move(obj)`, `obj` is in a valid but unspecified state; don't rely on its old value afterward.