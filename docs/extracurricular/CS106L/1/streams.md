# Streams

## Stringstream

```cpp
int main() {
    ostringstream oss("Ito-En Green Tea");
    cout << oss.str() << endl;
    oss << "haha";
    cout << oss.str() << endl;
    return 0;
}
```

这段程序执行的结果是：

```
Ito-En Green Tea
hahaEn Green Tea
```

这是因为stringstream有一个位置指针，当在执行`oss << "haha";`的时候，指针没有在末尾。我们可以做出如下改动：

```cpp
int main() {
    ostringstream oss("Ito-En Green Tea", ostringstream::ate);
    cout << oss.str() << endl;
    oss << "haha";
    cout << oss.str() << endl;
    return 0;
}
```

```
Ito-En Green Tea
Ito-En Green Teahaha
```

这样指针就是在末尾向后移动。


在C++中，`istringstream` 对象的读取是顺序进行的，每次读取操作都会从当前位置开始，直到遇到空白字符或流的末尾。因此，如果你在同一个 `istringstream` 对象上进行多次读取操作，每次读取操作都会从上一次读取结束的位置继续。

```cpp
int main() {
    istringstream iss("16.9 Ounces");
    double amount;
    string unit;

    iss >> amount;
    iss >> unit;

    cout << amount/2 << endl;
    cout << unit << endl;
    return 0;
}
```

```
8.45
Ounces
```

注意下面的区别：

```cpp
int main() {
    istringstream iss("16.9 Ounces");
    double amount;
    string unit;

    iss >> amount;
    iss >> unit;

    cout << amount << " " << unit << endl;

    return 0;
}
```

其输出结果是：

```
16.9 Ounces
```

而将`double`改为`int`，结果则变为：

```
16 .9
```

对于istringstream的抓取更准确的说法是：它会抓去尽可能多的有意义的字符。在这里，当其遇到小数点的时候，他认为这不能变成int的一部分，故停止抓取。

下图十分直观：

![alt text](<CleanShot 2025-01-21 at 23.47.39@2x.png>)

![alt text](<CleanShot 2025-01-21 at 23.47.56@2x.png>)


## stringstream v.s. string

![alt text](<CleanShot 2025-01-25 at 17.59.13@2x.png>)