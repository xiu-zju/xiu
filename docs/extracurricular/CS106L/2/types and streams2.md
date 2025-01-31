# Types and streams II

## Stream II

`getline` reads till the newline character and also consume the newline character.

`cin >>` will **skip** the whitespace character without **consuming** them.

!!! example
    ```cpp
    istringstream iss ("16.9\n 24");
    double val;
    string line;
    iss >> val; // val = 16.9
    getline(iss, line); // line = "";
    getline(iss, line); // line = " 24"
    ```

    We will get empty at the first `getline`.

    We can also do that:

    ```cpp
    istringstream iss ("16.9\n 24");
    double val;
    string line;
    iss >> val; // val = 16.9
    iss.ignore();
    getline(iss, line); // line = " 24"
    ```

## Morden C++ types

### auto

![alt text](<CleanShot 2025-01-25 at 09.35.39@2x.png>)

### pair/tuple

![alt text](<CleanShot 2025-01-25 at 10.00.07@2x.png>)

```cppvoid pairAndTuple() {
    // make_pair/tuple (C++11) automatically deduces the type!
    auto prices = make_pair(3.4, 5);  // pair<double, int>
    auto values = make_tuple(3, 4, "hi");  //tuple<int, int, const char*>

    prices.first = prices.second;    // prices = {5.0, 5}
    get<0>(values) = get<1>(values);  // values = {4, 4, "hi"}

    // structured binding (C++17) - extract each component
    auto [a, b] = prices;
    const auto& [x, y, z] = values;

    cout << "a: " << a << ", b: " << b << endl;
    cout << "x: " << x << ", y: " << y << ", z: " << z << endl;
}
```

### struct

![alt text](<CleanShot 2025-01-25 at 10.00.59@2x.png>)

### references

![alt text](<CleanShot 2025-01-25 at 10.01.16@2x.png>)

