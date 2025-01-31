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

