**Practice Problems (based on the C++ folder content)**

1. **Header Guard Implementation**
   - Write a header file `utils.h` that declares two functions:
     ```cpp
     int add(int a, int b);
     int multiply(int a, int b);
     ```
   - Provide a correct header guard (using `#ifndef`/`#define`/`#endif`) to prevent duplicate inclusion.
   - Write a source file `utils.cpp` that includes `utils.h` and defines the two functions.
   - Write a `main.cpp` that includes `utils.h` and calls both functions, printing the results.
   - Show the exact command you would use with `g++` to compile and link all three files into an executable.

2. **Macro vs. constexpr**
   - Create a header `constants.h` that defines the mathematical constant `PI` using `#define PI 3.14159`.
   - Write a small program that uses this macro to compute the area of a circle given a radius.
   - Refactor the program to replace the macro with a `constexpr` variable (or `const` double) and explain why the refactored version is preferable.

3. **Conditional Compilation with `#ifdef`**
   - In a header `debug.h`, wrap a block of code that prints a debug message using `std::cout` with `#ifdef DEBUG`.
   - In `main.cpp`, demonstrate both scenarios:
     a) Compile without defining `DEBUG` and show that the debug output is omitted.
     b) Compile with the compiler flag `-DDEBUG` (or `#define DEBUG` somewhere) and show that the debug output appears.
   - Provide the exact compilation commands for both cases.

4. **Including Your Own Header vs. System Header**
   - Write a simple program that includes a standard library header (e.g., `<iostream>`) using angle brackets and a custom header (e.g., `"myMath.h"`) using quotes.
   - Explain the difference in search paths and why each syntax is used for its respective type of header.

5. **Multi‑File Project Linking**
   - Design a small library consisting of:
     - `matrix.h` – declares a class `Matrix` with a constructor, a method `void set(int row, int col, double val)`, and a method `double get(int row, int col) const`.
     - `matrix.cpp` – includes `matrix.h` and provides the definitions for the class methods.
     - `main.cpp` – includes `matrix.h`, creates a `Matrix` object, sets and retrieves values, and prints the result.
   - Compile and link all files into a single executable using a single `g++` command.
   - List any additional flags or options you would use to ensure the header is not included multiple times during compilation.