# C++ Data Structures & Algorithms

Generic containers, linked structures, and sorting algorithms written in modern C++. These were built for CS 311 (Data Structures and Algorithms) at the University of Alaska Fairbanks, Fall 2023, and focus on templates, iterators, resource management, and exception safety.

## What's Inside

### TMSArray: STL-Compatible Dynamic Array (`tmsarray/`)
A templated, resizable array class similar to `std::vector`.
- Works with any element type: `TMSArray<int>`, `TMSArray<std::string>`, and so on
- Random-access iterators, so it works with STL algorithms like `std::sort` and `std::copy`
- Copy and move constructors and assignment, using the copy-and-swap idiom
- `push_back`, `pop_back`, `insert`, `erase`, `resize`, and `swap`, with amortized capacity growth
- Documented exception-safety guarantees, with `noexcept` where appropriate

### Linked Lists: Reverse & SlowMap (`linked-list/`)
- **`reverseList`:** reverses a singly linked list in place in O(n) time and O(1) extra space, using `std::unique_ptr` for ownership
- **`SlowMap<Key, Value>`:** an associative container (like a simple `std::map`) built on a linked list of key-value pairs, with smart-pointer memory management and exceptions for error handling

### Treesort (`treesort/`)
A generic sort built on a binary search tree.
- Inserts each item into a BST of `std::unique_ptr` nodes, then writes them back in order with an in-order traversal
- Works on any forward-iterator range: `treesort(v.begin(), v.end())`
- Stable for equal keys; O(n log n) on average and O(n²) in the worst case (already-sorted input)

### TimSort-Inspired Sort (`timsort/`, honors project)
An independent honors project exploring the ideas behind TimSort, the hybrid algorithm used by Python and Java.
- Sorts the input in runs with insertion sort, doubling the run size on each pass
- Includes a random-array generator and an ordering check for testing
- A full TimSort also merges adjacent sorted runs; adding that merge step is the planned next improvement

## Example

```cpp
#include "tmsarray.hpp"
#include "tsort.hpp"
#include <algorithm>
#include <string>

TMSArray<std::string> names;
names.push_back("Charlie");
names.push_back("Alice");
names.push_back("Bob");
std::sort(names.begin(), names.end());   // TMSArray works with STL algorithms

std::vector<int> nums = {5, 2, 9, 1, 7};
treesort(nums.begin(), nums.end());      // nums is now 1 2 5 7 9
```

## Building

Requires a C++17 compiler (g++ or clang++).

```
# TMSArray demo
g++ -std=c++17 tmsarray/tmsarray_main.cpp -o tmsarray_demo && ./tmsarray_demo

# TimSort-inspired sort (prompts for an array size)
g++ -std=c++17 timsort/timsort.cpp -o timsort_demo && ./timsort_demo
```

The linked-list and treesort components are header-only; include the header in your own program to use them.

## Project Structure

```
cpp-data-structures/
├── tmsarray/
│   ├── tmsarray.hpp        # TMSArray class template
│   └── tmsarray_main.cpp   # Demo program
├── linked-list/
│   ├── da6.hpp             # reverseList and SlowMap
│   └── llnode2.hpp         # Linked-list node (provided by instructor)
├── treesort/
│   └── tsort.hpp           # BST-based Treesort
└── timsort/
    ├── timsort.hpp         # Run-based sort, helpers
    └── timsort.cpp         # Demo program
```

## Concepts Practiced

Class and function templates · iterators and STL compatibility · RAII and smart pointers (`std::unique_ptr`) · move semantics · copy-and-swap · exception safety · recursion · binary search trees · algorithm analysis

## Credits

Assignment specifications, the linked-list node (`llnode2.hpp`), and starter files for Treesort were provided by Professor Glenn G. Chappell. All other implementation work is my own.