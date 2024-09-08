# lambda表达式的类型

在C++中，lambda表达式实际上是一个匿名的闭包类型（closure type），每个lambda表达式都有自己独特的类型。这种类型是编译器生成的，通常无法直接引用。为了使用这种匿名类型，可以通过`decltype`来获取它。

### 理解lambda表达式的类型

当我们定义一个lambda表达式时，编译器会为其生成一个匿名类类型，并在其中定义一个`operator()`。例如：

```cpp
auto deleter = [](int* ptr) {
    std::cout << "Lambda deleter called\n";
    delete ptr;
};
```

上面的lambda表达式在编译时会被转换为类似下面的匿名类：

```cpp
struct __lambda_deleter {
    void operator()(int* ptr) const {
        std::cout << "Lambda deleter called\n";
        delete ptr;
    }
};
```

因此，`deleter`的类型是一个具有`operator()`的匿名类。

当我们需要一个函数类型参数时，通常使用`decltype(lambda)`。

例如`unique_ptr<T, D> u(d) `自定义删除器的构造函数

D为decltype(lambda)

d为一个lambda对象