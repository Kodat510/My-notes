---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# Basics of Including Other Files in C++ (Preprocessor & Headers)

To use functions, classes, or variables defined in another file, C++ relies on the **preprocessor** — a step that runs before actual compilation and handles directives starting with `#`.

---

## 1. The `#include` Directive

Copies the contents of another file directly into the current file, before compilation happens.

```cpp
#include <iostream>      // library header — angle brackets
#include "myHeader.h"    // your own header — quotes
```

|Syntax|Used for|
|---|---|
|`#include <name>`|Standard library / system headers (`iostream`, `vector`, `string`)|
|`#include "name.h"`|Your own project headers, found relative to the current file|

---

## 2. Why You Can't Just `#include` a `.cpp` File

Splitting code across files normally means:

- A **header file** (`.h` / `.hpp`) — contains **declarations** (function prototypes, class definitions).
- A **source file** (`.cpp`) — contains **definitions** (the actual implementation).

Example project:

```
math_utils.h    <- declares functions
math_utils.cpp  <- defines (implements) functions
main.cpp        <- uses the functions
```

**math_utils.h**

```cpp
#ifndef MATH_UTILS_H
#define MATH_UTILS_H

int add(int a, int b);
int multiply(int a, int b);

#endif
```

**math_utils.cpp**

```cpp
#include "math_utils.h"

int add(int a, int b) {
    return a + b;
}

int multiply(int a, int b) {
    return a * b;
}
```

**main.cpp**

```cpp
#include <iostream>
#include "math_utils.h"

int main() {
    std::cout << add(2, 3) << std::endl;
    return 0;
}
```

`main.cpp` only needs the _declarations_ from `math_utils.h` to compile — the actual code gets linked in later from the compiled `math_utils.cpp`.

---

## 3. Header Guards

If a header gets `#include`d twice (directly or indirectly through other headers), the compiler sees duplicate declarations — an error. Header guards prevent this.

```cpp
#ifndef MATH_UTILS_H   // "if not already defined"
#define MATH_UTILS_H   // define it now, so next time it's skipped

// header content here

#endif
```

Modern alternative (supported by all major compilers):

```cpp
#pragma once
```

Simpler, but `#ifndef`/`#define`/`#endif` is the traditional, fully portable form.

---

## 4. Compiling Multiple Files

With separate `.cpp` files, you compile them together (or separately then link):

```bash
g++ main.cpp math_utils.cpp -o program
./program
```

Each `.cpp` file is compiled into an object file (`.o`), and the **linker** connects calls in `main.cpp` to the actual definitions in `math_utils.cpp`.

---

## 5. Other Common Preprocessor Directives

|Directive|Purpose|
|---|---|
|`#include`|Insert contents of another file|
|`#define`|Create a macro (text substitution)|
|`#ifndef` / `#ifdef` / `#endif`|Conditional compilation (used for header guards, platform-specific code)|
|`#pragma once`|Modern, simpler header guard|

### `#define` for Constants (older style)

```cpp
#define PI 3.14159

double area = PI * radius * radius;
```

In modern C++, prefer `const` or `constexpr` instead — they're type-safe, unlike macros:

```cpp
constexpr double PI = 3.14159;
```

### `#ifdef` for Conditional Compilation

```cpp
#ifdef DEBUG
    std::cout << "Debug mode active" << std::endl;
#endif
```

Code inside only compiles if `DEBUG` has been defined somewhere (e.g. via `#define DEBUG` or a compiler flag like `-DDEBUG`).

---

## Quick Reference

|Term|Meaning|
|---|---|
|Preprocessor|Runs before compilation, processes `#` directives|
|Header file (`.h`)|Contains declarations, shared across files|
|Source file (`.cpp`)|Contains definitions/implementation|
|`#include <...>`|Include a standard library header|
|`#include "..."`|Include your own header file|
|Header guard|Prevents a header from being included more than once|
|Linker|Connects function calls to their actual definitions across compiled files|

---

## Common Pitfall

Forgetting a header guard (or `#pragma once`) causes a **"redefinition" compile error** the moment a header is included from more than one place — which happens more often than expected once files start including each other.