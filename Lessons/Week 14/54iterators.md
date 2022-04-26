# 04/19/22: Introduction to Iterators

## Motivation
- **Container** is an object that holds other objects: lists, vectors, trees, graphs, etc.
- They can have a sequence, ex: beginning = head, end = tail
- Common **Algorithms**: tasks performed on containers
    - Collect data into container
    - Organize data by some rule
    - Retrieve items (by index, by value, by property, etc)
    - Add new items
    - Remove existing items
    - Search
    - Sort
    - Numeric operations (sum all items, etc)
- A lot of the logic for tasks such as searching have the same logic, is a generic solution possible?

## Iterators
- **Iterator is an abstraction of a pointer to some element in a sequence**
- Operators of iterator
    - **operator\*** - access the element we are currently visiting
    - **operator++** - move to the next element in sequence
    - **operator==** - check if two iterators are visiting same element

## Simplified std::vector iterator
```cpp
template <typename InputIt, typename T>
InputIt Find(InputIt first, InputIt last, const T& value) {
    while (first != last) {
        if (*first == value) return first;
        first++;
    }
    return last;
}
```

## STL overview
- Algorithms manipulate data, but don't know about containers. Containers store data, but don't know about algorithms. **Iterators bridge this gap** while providing
    - Uniform access to data
    - Independent of how it is stored
    - Independent of type
    - Easy/fast to read/modify
- Read/White iterators: .begin(), .end()
- Read only iterators: .cbegin(), cend()

### STL Iterators in action
```cpp
std:vector<int> v{1, 2, 3, 4};
for (auto iter = v.begin(); iter != v.end(); iter++) {
    std::cout << *iter << std::endl;
}

auto iter_to_result = std::find(v.begin(), v.end(), 2);
if (iter_to_result != v.end()) {
    std::cout << *iter_to_result << std::endl;
} else {
    std::cout << "elem not found" << std::endl;
}
```