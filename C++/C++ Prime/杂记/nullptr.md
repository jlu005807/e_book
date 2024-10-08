# nullptr和NULL



`nullptr` 在 C++11 中被引入，相比于之前的 `NULL`，它提供了更安全和清晰的方式来表示空指针。以下是 `nullptr` 相比于 `NULL` 更安全的几个原因：

1. **类型安全**：`nullptr` 是一个特殊的类型，`std::nullptr_t`，可以转换为任何指针类型，但不能转换为非指针类型（除了布尔类型）。而 `NULL` 通常被定义为 `0` 或者 `((void*)0)`，它实际上是一个整数，这可能导致类型混淆和潜在的错误。例如，在函数重载的情况下，使用 `NULL` 可能会导致调用错误的函数版本。
2. **更好的兼容性**：在模板编程中，`nullptr` 可以清晰地表示空指针，而 `NULL` 可能会引起歧义。因为 `NULL` 被定义为 `0`，在模板函数中，编译器可能会将其视为整数而不是指针，从而导致错误的模板实例化。
3. **避免隐式转换错误**：由于 `nullptr` 不能隐式转换为整数类型，这避免了将空指针与整数进行比较时可能出现的错误。而使用 `NULL` 时，由于它可以是 `0`，可能会在不适当的上下文中被错误地用作整数。
4. **清晰的语义**：`nullptr` 明确表示空指针，这使得代码的意图更加清晰，可读性和可维护性也因此提高。

下面是一个展示 `nullptr` 和 `NULL` 在函数重载中差异的例子：

````cpp
void* func(char *ptr) {

  cout << "char version*" << endl;

}

void func(int *i) {

  cout << "int version" << endl;

}

int main() {
  func(NULL);  // 可能调用 func(int)，这取决于 NULL 的定义
  func(nullptr); // *明确调用 func(char*)
}
````
在这个例子中，使用 `nullptr` 可以确保调用的是接受指针参数的函数版本，而使用 `NULL` 可能会调用错误的版本，这取决于 `NULL` 的具体定义。这种类型安全和清晰的语义是 `nullptr` 相比于 `NULL` 更安全的主要原因。