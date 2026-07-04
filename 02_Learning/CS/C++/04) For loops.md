# Basics of Range-Based For Loops in C++

A range-based `for` loop (introduced in C++11) lets you iterate over every element of a container or array without manually managing an index. It's shorter and less error-prone than a traditional `for` loop.

---

## 1. Basic Syntax

```cpp
for (elementType elementName : container) {
    // use elementName
}
```

Example:

```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};

for (int n : numbers) {
    std::cout << n << " ";
}
// prints: 1 2 3 4 5
```

Compare to the traditional index-based version it replaces:

```cpp
for (int i = 0; i < numbers.size(); i++) {
    std::cout << numbers[i] << " ";
}
```

---

## 2. Works on Any "Iterable" Type

Arrays:

```cpp
int arr[] = {10, 20, 30};
for (int x : arr) {
    std::cout << x << " ";
}
```

Strings (iterates character by character):

```cpp
std::string word = "hello";
for (char c : word) {
    std::cout << c << " ";
}
// prints: h e l l o
```

`std::map` (iterates key-value pairs):

```cpp
std::map<std::string, int> ages = {{"L", 17}, {"A", 25}};

for (auto pair : ages) {
    std::cout << pair.first << " is " << pair.second << std::endl;
}
```

---

## 3. Using `auto` Instead of Writing the Type

Instead of spelling out the element type, `auto` lets the compiler figure it out. This is the most common style in modern C++.

```cpp
for (auto n : numbers) {
    std::cout << n << " ";
}
```

---

## 4. Modifying Elements: Use a Reference

By default, `elementName` is a **copy** of each element — changes to it don't affect the container.

```cpp
std::vector<int> numbers = {1, 2, 3};

for (int n : numbers) {
    n = n * 2;   // only modifies the local copy
}
// numbers is unchanged: {1, 2, 3}
```

To actually modify the container, iterate by reference with `&`:

```cpp
for (int& n : numbers) {
    n = n * 2;
}
// numbers is now {2, 4, 6}
```

---

## 5. Avoiding Copies: Use `const auto&` for Read-Only Access

For large elements (like `std::string` or custom objects), copying each one is wasteful if you're only reading. Use a `const` reference:

```cpp
std::vector<std::string> names = {"Alice", "Bob", "Charlie"};

for (const auto& name : names) {
    std::cout << name << std::endl;
}
```

This avoids copying each `name` while also preventing accidental modification.

---

## Quick Reference

|Syntax|Copies element?|Can modify container?|When to use|
|---|:-:|:-:|---|
|`for (T x : container)`|Yes|No|Small types (`int`, `char`), read-only|
|`for (T& x : container)`|No|Yes|Need to modify elements in place|
|`for (const T& x : container)`|No|No|Large types, read-only (most common for objects)|
|`for (auto x : container)`|Yes|No|Let compiler infer type, read-only|
|`for (auto& x : container)`|No|Yes|Let compiler infer type, modifying|
|`for (const auto& x : container)`|No|No|Let compiler infer type, efficient read-only (default choice for objects)|

---

## Common Pitfall

Trying to modify elements without `&` — the loop compiles fine but silently does nothing to the original container:

```cpp
for (int n : numbers) {
    n++;   // no effect on numbers itself
}
```

If you need to change the container's contents, always reach for `int&` / `auto&`.