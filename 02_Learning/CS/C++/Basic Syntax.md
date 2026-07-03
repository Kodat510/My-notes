# C++ Master Syntax Cheat Sheet
**Category:** Language Specification / Memory Mechanics
**System Targets:** Bare-Metal Architecture, Embedded Firmware (Arduino), High-Performance Pipelines

---

## 1. Input, Output, & Headers (`<iostream>`)
```cpp
#include <iostream> // Preprocessor directive to include the Standard I/O library

int main() {
    // 1. Standard Console Output
    std::cout << "System Initialize..." << std::endl; // Flushes buffer (slower)
    std::cout << "Data Packet Sent.\n";              // Inserts newline character (faster optimization)

    // 2. Standard Console Input
    int rawSensorInput;
    std::cin >> rawSensorInput; // Extracts stream data directly into variable memory
    
    return 0;
}

```
### std::cout

- std::cout is considered a hole from your program to the console, where data flows into it
- The data flow into std::cout is indicated by the << operator
- To add variables, you must use another << operator to separate them from strings
- It is essential to keep strings and variables separated using the << operator
- The << operator must always flow into std::cout to ensure proper data output
- jkjdkjdjk