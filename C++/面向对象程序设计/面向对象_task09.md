# dynamic_cast

`dynamic_cast` 是 C++ 中的一个运算符，用于在运行时进行类型安全的向下转换（downcasting）或横向转换（cross-casting）。它主要用于处理含有继承关系的类对象。`dynamic_cast` 的使用主要集中在以下几个方面：

### 主要用途
1. **向下转换（Downcasting）**：
   - 从基类指针或引用转换为派生类指针或引用。
2. **横向转换（Cross-casting）**：
   - 在同一个继承体系内，从一个指向基类的指针或引用转换为另一个派生类的指针或引用。

### 语法
```cpp
dynamic_cast<new_type>(expression)
```
- `new_type`：目标类型，必须是指针或引用类型。
- `expression`：要转换的表达式。

### 使用示例
#### 向下转换
```cpp
class Base {
public:
    virtual ~Base() {} // 必须有虚函数，通常是虚析构函数
};

class Derived : public Base {
public:
    void derivedFunction() {
        std::cout << "Derived function called." << std::endl;
    }
};

Base* basePtr = new Derived();
Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);

if (derivedPtr) {
    derivedPtr->derivedFunction();
} else {
    std::cout << "Dynamic cast failed." << std::endl;
}
```

#### 横向转换
```cpp
class AnotherDerived : public Base {
public:
    void anotherFunction() {
        std::cout << "Another function called." << std::endl;
    }
};

Base* basePtr = new Derived();
AnotherDerived* anotherPtr = dynamic_cast<AnotherDerived*>(basePtr);

if (anotherPtr) {
    anotherPtr->anotherFunction();
} else {
    std::cout << "Dynamic cast failed." << std::endl;
}
```

### 关键点
1. **必须有虚函数**：`dynamic_cast` 只能用于包含虚函数的类，这通常通过在基类中定义虚析构函数来实现。
2. **类型安全检查**：如果转换不成功，转换为指针类型时返回 `nullptr`，转换为引用类型时抛出 `std::bad_cast` 异常。
3. **运行时开销**：由于`dynamic_cast` 在运行时进行类型检查，因此会带来一定的运行时开销。

### 使用场景
1. **复杂继承体系中的类型检查**：在多态环境中，当需要确保指针或引用指向的是特定的派生类对象时，使用 `dynamic_cast` 进行类型检查。
2. **安全的类型转换**：相对于 `static_cast`，`dynamic_cast` 提供了更安全的类型转换方式，因为它会在运行时进行类型检查，避免了类型转换错误带来的潜在风险。

`dynamic_cast` 是C++中提供的一种强大且类型安全的类型转换工具，适用于需要在运行时确认类型的多态场景。





# 抽象类的接口

抽象类表示一种泛化关系，其接口函数应在子类中存在,以保证接口的一致性，包括 创建对象和释放对象的接口，因此构造函数和拷贝构造函数应为 public。

# 析构函数不重载

wdnmd.

# 继承下的类型转换

(从来没看过...)

### protected/private继承下

从派生类向基类转换：向上类型转换

从基类向派生类转换：向下类型转换

### public继承下

从子类向父类转换：向上类型转换

从父类向子类转换：向下类型转换

1.**此时的向上**类型转换**有意义**

2.逻辑上，是类型的泛化或一般化

3.**语言上，**public**行为集被窄化**

![image-20240604170317470](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240604170317470.png)

**public****继承方式下向下类型转换**

1.**此时的向下类型转换有意义**

2.**但可能成功，也可能失败**

3.**只能在运行时确定**(**dynamic_cast**)

# **C++**中的类型转换操作符

### 转换方式

1.内置类型的自动转换，如 int->float

2.构造函数转换

3.定义自动转换函数

4.public继承下的向上类型自动转换

5.使用类型转换操作符

​    1.static_cast转换操作符

​    2.const_case转换操作符

​    3.reinterpret_cast转换操作符

​    4.dynamic_cast转换操作符



**static_cast<T>(exp)**等价于C语言中的强制类型转换 (T)exp？

**const_cast<T>(exp)**常量转换：用于添加或移除表达式中的const或volatile约束, 其中 T 与exp的类型，除了const或volatile等修饰之外，必须一致

**reinterpret_cast<T>(exp)**重新解释：对表达式的类型做出重新解释

**dynamic_cast<T>(exp)**动态转换：

在运行时刻，尝试将exp转换成T类型。多用于public继承下，将父类类型转换成子类类型；

T**只能**为类的指针、类的引用、void *三种形式;

dynamic_cast要用到RTTI(运行时类型识别),通常各编译器都是通过虚拟表(VTable)来实现RTTI的，因此类中要有虚函数，才能使用.