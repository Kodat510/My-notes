---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# Basics of Defining Functions in C++

A function is a named block of code that can be called from elsewhere in the program. This covers the core syntax for writing one.

---

## 1. Basic Structure

```cpp
returnType functionName(parameterType parameterName) {
    // code
    return value;   // only if returnType is not void
}
```

Example:

```cpp
int add(int a, int b) {
    return a + b;
}
```

- `int` — the return type (what the function gives back)
- `add` — the function name
- `(int a, int b)` — parameters, with their types
- `{ ... }` — the function body
- `return a + b;` — sends the result back to the caller

Calling it:

```cpp
int result = add(3, 4);   // result is 7
```

---

## 2. Functions with No Return Value

Use `void` when the function performs an action but doesn't return anything.

```cpp
void greet(std::string name) {
    std::cout << "Hello, " << name << "!" << std::endl;
}

greet("L");   // no value to store, just runs
```

---

## 3. Functions with No Parameters

```cpp
void printMenu() {
    std::cout << "1. Start\n2. Options\n3. Exit" << std::endl;
}

printMenu();
```

---

## 4. Declaration vs. Definition

A **declaration** (function prototype) tells the compiler a function exists, without giving its body. A **definition** provides the actual code.

```cpp
// Declaration (prototype) — usually at the top of the file or in a header
int add(int a, int b);

int main() {
    std::cout << add(2, 3);   // can call it here, even though it's defined below
    return 0;
}

// Definition — the actual implementation
int add(int a, int b) {
    return a + b;
}
```

Declarations are necessary when a function is called before its definition appears in the file, or when it's shared across multiple files via a header (`.h`) file.

---

## 5. Default Parameters

A parameter can have a default value, used when the caller omits that argument.

```cpp
void greet(std::string name, std::string greeting = "Hello") {
    std::cout << greeting << ", " << name << "!" << std::endl;
}

greet("L");            // "Hello, L!"
greet("L", "Hey");     // "Hey, L!"
```

Default parameters must come after any non-default ones in the parameter list.

---

## 6. Returning Early

A function stops executing as soon as it hits a `return` statement.

```cpp
int absoluteValue(int x) {
    if (x < 0) {
        return -x;
    }
    return x;
}
```

---

## 7. `main()` — the Entry Point

Every C++ program has exactly one `main` function; execution starts there.

```cpp
int main() {
    std::cout << "Program starts here" << std::endl;
    return 0;   // 0 means the program exited successfully
}
```

---

## Quick Reference

|Piece|Purpose|
|---|---|
|Return type|Type of value sent back (`int`, `void`, `std::string`, etc.)|
|Function name|How you call it later|
|Parameters|Inputs the function needs, each with a type|
|Function body|The code that runs|
|`return`|Sends a value back and exits the function|
|Declaration|Tells the compiler the function exists (signature only)|
|Definition|The actual implementation|