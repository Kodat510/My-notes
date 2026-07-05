---
tags:
  - CPP
  - CS
  - Programming
author: Kodat510
---
# Basics of Pointers in C++

A pointer is a variable that stores a **memory address** instead of a value directly. Think of it like a house's street address written on a sticky note — the note itself isn't the house, but it tells you exactly where to find it.

---

## 1. The Core Analogy

- A normal variable is like a **house**: it holds something (a value) at a specific location.
- A pointer is like a **sticky note with the house's address written on it**. The note doesn't contain the furniture (the value) — it just tells you where the house is.
- To actually see or use the furniture, you have to **go to the address** — this is called **dereferencing**.

```cpp
int age = 25;        // "age" is the house, containing the value 25
int* ptr = &age;      // "ptr" is the sticky note, holding the address of "age"
```

---

## 2. The Two Key Operators

|Operator|Name|Meaning|Analogy|
|:-:|---|---|---|
|`&`|Address-of|"Give me the address of this variable"|Writing the house's address onto the sticky note|
|`*`|Dereference|"Go to the address this pointer holds, and give me what's there"|Walking to the address and looking inside the house|

```cpp
int age = 25;
int* ptr = &age;    // ptr now holds the address of age

std::cout << ptr;    // prints the memory address (e.g. 0x7ffee4a3)
std::cout << *ptr;   // prints 25 — the value AT that address
```

---

## 3. Modifying a Value Through a Pointer

Dereferencing doesn't just read — it can also write, since you're directly accessing the original house.

```cpp
int age = 25;
int* ptr = &age;

*ptr = 30;    // go to the address, change what's there
std::cout << age;   // prints 30 — the original variable changed
```

It's like going to the house at that address and repainting a wall — the house itself changes, not just your sticky note.

---

## 4. `nullptr` — A Pointer to Nowhere

```cpp
int* ptr = nullptr;
```

This is a sticky note with **no address written on it** — it doesn't point anywhere. Trying to dereference it (`*ptr`) is like trying to walk to a blank address — undefined behavior, often a crash.

Always check before dereferencing if a pointer might be null:

```cpp
if (ptr != nullptr) {
    std::cout << *ptr;
}
```

---

## 5. Pointers and Functions (Quick Recap)

Passing a pointer lets a function modify the caller's original variable, since it has the "address," not just a copy of the value.

```cpp
void addTen(int* x) {
    *x = *x + 10;   // walk to the address, update the value there
}

int main() {
    int number = 5;
    addTen(&number);   // hand over the address
    // number is now 15
}
```

---

## 6. Pointers and Arrays

An array name behaves like a pointer to its first element — like the address of the first house on a street, from which every other house can be reached by walking further down.

```cpp
int numbers[3] = {10, 20, 30};
int* ptr = numbers;      // points to numbers[0]

std::cout << *ptr;        // 10
std::cout << *(ptr + 1);  // 20 — move one "house" down the street
std::cout << *(ptr + 2);  // 30
```

---

## 7. Double Pointers (`int**`)

A double pointer is a **sticky note that holds the address of another sticky note**, rather than the address of an actual house.

```cpp
int age = 25;
int* ptr = &age;       // ptr holds the address of age
int** ptrToPtr = &ptr;  // ptrToPtr holds the address of ptr
```

To reach the actual value (`age`), you have to dereference **twice** — walk to the first sticky note, read the address written on it, then walk to that second address.

```cpp
std::cout << **ptrToPtr;   // 25
```

Breaking it down step by step:

```cpp
*ptrToPtr    // dereference once -> gives you "ptr" itself (an address)
**ptrToPtr   // dereference twice -> gives you "age" itself (the value, 25)
```

|Expression|What it holds / gives|
|---|---|
|`ptrToPtr`|Address of `ptr`|
|`*ptrToPtr`|The value of `ptr`, which is the address of `age`|
|`**ptrToPtr`|The value of `age`|

### Why Would You Ever Need This?

Common case: a function needs to modify a pointer itself (not just the thing it points to) — e.g. making the original pointer point somewhere new.

```cpp
void allocateAndSet(int** ptrAddress) {
    *ptrAddress = new int;    // change what the original pointer points to
    **ptrAddress = 42;         // set the value at that new location
}

int main() {
    int* myPtr = nullptr;
    allocateAndSet(&myPtr);    // pass the address of the pointer itself
    std::cout << *myPtr;        // 42
    delete myPtr;
}
```

Without the double pointer, the function would only receive a _copy_ of `myPtr` and couldn't redirect the caller's original pointer to a new address — same reasoning as pass-by-value vs. pass-by-reference, just one level deeper.

---

## Quick Reference

|Concept|Analogy|
|---|---|
|Variable|A house with something inside|
|Pointer (`T*`)|A sticky note with a house's address|
|`&x`|Writing `x`'s address onto a sticky note|
|`*ptr`|Walking to the address and reading/writing what's there|
|`nullptr`|A blank sticky note — pointing nowhere|
|Double pointer (`T**`)|A sticky note holding the address of _another_ sticky note|
|`**ptrToPtr`|Walk to the first note, follow the address on it, walk again, then read the house|

---

## Common Pitfalls

1. **Dereferencing `nullptr` or an uninitialized pointer** — like trying to visit an address that doesn't exist; causes crashes or undefined behavior.
2. **Dangling pointers** — a pointer that still holds an address after the house at that address has been destroyed (e.g. after `delete`). The sticky note is still there, but the house is gone.
    
    ```cpp
    int* ptr = new int(5);delete ptr;      // house destroyedstd::cout << *ptr;   // BUG: reading a demolished house
    ```
    
3. **Confusing `*` in declarations vs. dereferencing** — `int* ptr` declares a pointer type; `*ptr` in an expression dereferences it. Same symbol, different meaning depending on context.
4. **Memory leaks** — allocating memory with `new` but forgetting `delete` is like getting a new house address and never telling anyone it can be reused — the memory stays "occupied" even though nothing uses it anymore.