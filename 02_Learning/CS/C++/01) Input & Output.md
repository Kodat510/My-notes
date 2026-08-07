---
tags:
  - Programming
  - CPP
  - CS
author: Kodat510
---
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
### std::cin

-  Consider cin as a stream of data flowing from the program to your code
-  You must capture this stream of data in your code
-  Cin is based on line order, meaning you can't access data out of sequence
-  You can capture data and assign it to a variable as it is input
-  Since data flows out of cin, you must use the >> operator to capture it in variables

Инструкция: based on the C++ folder in my vault give me some practice problems based on it to test my knowledge and do not go out of the scope of these problems give me only 5 problems

## 2. Practice Problems

1. Print "Hello World" using `std::cout` and `std::endl`.

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World" << std::endl;
    return 0;
}
```

2. Read an integer from `std::cin` and output it.

```cpp
#include <iostream>

int main() {
    int value;
    std::cin >> value;
    std::cout << value << std::endl;
    return 0;
}
```

3. Read an integer, determine if it is even, and print "Even" or "Odd".

```cpp
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    if (n % 2 == 0)
        std::cout << "Even" << std::endl;
    else
        std::cout << "Odd" << std::endl;
    return 0;
}
```

4. Implement `void increment(int &x)` and call it in `main` to increment a variable.

```cpp
#include <iostream>

void increment(int &x) {
    ++x;
}

int main() {
    int num = 5;
    increment(num);
    std::cout << num << std::endl;
    return 0;
}
```

5. Output "Data Packet Sent." then read a float and print it with two decimal places.

```cpp
#include <iostream>
#include <iomanip>

int main() {
    std::cout << "Data Packet Sent." << std::endl;
    float value;
    std::cin >> value;
    std::cout << std::fixed << std::setprecision(2) << value << std::endl;
    return 0;
}
```

---