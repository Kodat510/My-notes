**Practice Problems Based on C++ Folder:**  

1. **Linked List Implementation**  
   Implement a singly linked list class in C++ with the following methods:  
   - `void insertAtEnd(int value)`  
   - `void deleteByValue(int value)`  
   - `bool search(int value)`  
   - `void printList()`  
   Ensure proper memory management (avoid memory leaks).  

2. **Sorting Algorithm**  
   Write a function `void sortArray(int arr[], int n)` that sorts the array in ascending order using **only** the bubble sort algorithm. Do not use any built-in sorting functions.  

3. **Class Hierarchy**  
   Create a base class `Shape` with a pure virtual function `virtual double area() = 0`. Derive two classes `Rectangle` and `Circle` from `Shape`, implementing the `area()` method for each. Demonstrate polymorphism by creating an array of `Shape*` pointers and calling `area()` on each.  

4. **STL Containers**  
   Given a vector of integers, write a function `std::vector<int> removeDuplicates(const std::vector<int>& input)` that returns a new vector with all duplicates removed, preserving the original order. Use only STL containers (no loops if possible).  

5. **Dynamic Memory and Pointers**  
   Implement a function `int* findMaximum(int* arr, int size)` that dynamically allocates memory for an integer, stores the maximum value in the array, and returns the pointer. Ensure the caller is responsible for freeing the memory.  

---  
**Note:** These problems focus on core C++ concepts (OOP, STL, pointers, algorithms). Adjust based on your vault's specific content.