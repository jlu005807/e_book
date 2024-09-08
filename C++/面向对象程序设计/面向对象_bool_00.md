面向对象_book00

# 重载

```cpp
class A
{
public:
    int x; // 成员变量 x

    // 构造函数，使用初始化列表将参数 i 赋值给成员变量 x
    A(int i) : x(i) {}

    // 类型转换运算符，将 A 类型对象转换为 float 类型
    operator float()
    {
        float f = this->x * 1.0; // 将 x 转换为 float 类型
        return f; // 返回转换后的 float 值
    }
};

```

```cpp
int main()
{
    A a(9); // 创建一个 A 类的对象 a，并用 9 初始化它
    float m = 10 + a; // 将 a 转换为 float 类型，然后与 10 相加
    cout << m << endl; // 输出结果
}

```

