# Sequence

## Sequence containers

Provide access to sequence of elements.

Includes:

- `std::vector<T>`
- `std::deque<T>`
- `std::list<T>`
- `std::array<T>`
- `std::forward_list<T>`

### std::vector<T>

A vector represents a sequence of elements of **any** types.

You specify the type when using the vector:

- `std::vector<int> vecInt;`
- `std::vector<string> vecStr;`
- `std::vector<myStruct> vecStruct;`
- `std::vector<std::vector<string>> vecOfVec;`

### std::deque<T>

It suppose the `push_front` operation. But the speed to access the element is slower the `vector`.

## Container adaptors

- stack
- queue

They are implemented by deque commonly.

- Step 1
    - `stack`: Just limit the functionality of a vector/deque to only allow push_back and pop_back.
    - `queue`: Just limit the functionality of a deque to only allow push_back and pop_front.
- Step 2
    - Only allow access to the “top” element.

## Associative Containers

Have no idea of a sequence.

Data is accessed uding the **key** instead of indexes.

Includes:

- `std::map<T1, T2>`
- `std::set<T>`
- `std::unordered_map<T1, T2>`
- `std::unordered_set<T>`

In map and set, keys need to be comparable using **<** (less than) operator.

Unordered map and set are based on hash function. You need to define how the key can be hashed.

- map/set: keys in sorted order, faster to interate through a range of elements.
- unordered map/set: faster to access individual elements by key.

## Iteraters

Iteraters allows iteration over **any container**, whether it is ordered or not.

### Usage

- create an iterater: `set<int>::iterator iter = mySet.begin();`
- dereference: `cout << *iter << endl;`
- advance the iterator one: `iter++`
- check if we have hit the end by comparing to `mySet.end()`: `if(iter == mySet.end()) return;`

!!! tip

    **第一种方式（基于范围的 for 循环）**

    ```cpp
    for (auto elem : freqMap) {
        cout << elem.first << ", " << elem.second << endl;
    }
    ```
    ✅ **特点：**

    - **使用范围 for 循环**（C++11 引入）。
    - `auto elem` 代表 `std::pair<const Key, Value>`，即 `std::map` 的键值对。
    - `elem.first` 访问键，`elem.second` 访问值。
    - **底层是拷贝遍历**（`elem` 是 `std::pair` 的副本，而非引用）。
    - 适用于 `std::map` 和 `std::unordered_map` 等 STL 容器。

    🛑 **缺点：**

    - 每次遍历时会拷贝 `std::pair`，如果 `freqMap` 很大，拷贝开销较高。
    - **解决方案**：使用 **引用**，避免不必要的拷贝：

    ```cpp
    for (const auto& elem : freqMap) {
        cout << elem.first << ", " << elem.second << endl;
    }
    ```

    ---

    **第二种方式（基于迭代器的 while 循环）**
    ```cpp
    while (it != freqMap.end()) {
        cout << it->first << ", " << it->second << endl;
        ++it;
    }
    ```
    ✅ **特点：**

    - **使用迭代器手动遍历 `std::map`**。
    - `it` 是 `std::map<Key, Value>::iterator` 类型的变量（需要在循环前初始化）。
    - `it->first` 访问键，`it->second` 访问值。
    - **不会产生拷贝开销**（直接访问原始数据）。

    🛑 **注意点：**

    - 需要在循环前声明并初始化 `it`：
    ```cpp
    auto it = freqMap.begin(); // 必须初始化
    ```
    - 手动管理 `it`，必须 **确保 `++it`，避免死循环**。
    - 适用于 **可能需要删除元素的情况**（`erase(it)` 需要用迭代器）。

    ---

    **第三种方式（结构化绑定的范围 for 循环，C++17）**
    ```cpp
    for (auto [key, val] : freqMap) {
        cout << key << ", " << val << endl;
    }
    ```
    ✅ **特点：**

    - **使用 C++17 的结构化绑定**（`std::pair` 解构）。
    - `key` 直接绑定 `first`，`val` 直接绑定 `second`，写法更简洁。
    - 仍然是 **拷贝遍历**，如果 `val` 是对象，可能有开销。
    - **解决方案**（使用引用，避免拷贝）：
  
    ```cpp
    for (const auto& [key, val] : freqMap) {
        cout << key << ", " << val << endl;
    }
    ```


    **三者的区别与关联**

    | 遍历方式  | 适用场景  | 是否拷贝 | 代码简洁性 | 适用 C++ 版本 |
    |---------|---------|-------|---------|---------|
    | **范围 for 循环 (`for (auto elem : freqMap)`)** | 适用于所有 STL 容器 | **是**（除非 `auto&`） | 简洁 | C++11+ |
    | **迭代器 while (`while (it != freqMap.end())`)** | 需要删除元素或更灵活控制遍历 | **否** | 较繁琐 | C++98+ |
    | **结构化绑定 (`for (auto [key, val] : freqMap)`)** | 代码更直观，可读性更好 | **是**（除非 `auto&`） | 最简洁 | C++17+ |

    ✅ **推荐方案**：

    1. **若无特殊需求**，优先使用 **C++17 结构化绑定遍历**（更简洁）。
    2. **避免拷贝**，使用 `const auto&`：
    ```cpp
    for (const auto& [key, val] : freqMap) { /* ... */ }
    ```
    3. **需要修改或删除元素**，使用迭代器：
    ```cpp
    for (auto it = freqMap.begin(); it != freqMap.end(); ) {
        if (it->second < 0) it = freqMap.erase(it);
        else ++it;
    }
    ```

!!! note
    ```cpp
    set<int>::iterator iter = elems.lower_bound(4); // find smallest element >= key
    set<int>::iterator end = elems.upper_bound(6); // find smallest element > key
    cout << "start: " << *iter << ", end: " << *end << endl;

    for(; iter != end; iter++) {
        cout << *iter << " ";
    }
    ```

    ||[a, b]|[a, b)|(a, b]|(a, b)|
    |---|---|---|---|---|
    |begin|lower_bound(a)|lower_bound(a)|upper_bound(a)|upper_bound(a)|
    |end|upper_bound(b)|lower_bound(b)|upper_bound(b)|lower_bound(b)|