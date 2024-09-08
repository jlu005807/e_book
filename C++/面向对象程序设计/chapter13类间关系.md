# chapter13类间关系

# **必须使用初始化列表:**

1. 常量数据成员(必须)
2. 引用数据成员(必须)
3. 对象数据成员(没有默认构造函数情况下)(必须)
4. 普通数据成员

# 标识符的作用域

1. local scope(块, 局部)
2. global scope(全局)
3. class scope(类作用域)
4. namespace scope(名字空间)

# 静态数据成员

在面向对象编程（OOP）中，静态数据成员和静态成员函数是类的一部分，具有特殊的性质和用途。下面是对这两个概念的解释：

### 静态数据成员（Static Data Members）

1. **定义与特性**：
   - 静态数据成员是类的成员变量，但它属于类本身，而不是任何一个具体的对象。
   - 不同于普通的成员变量，每个类的实例（对象）都有自己的成员变量副本，而静态数据成员在所有对象之间共享一份副本。
   - 静态数据成员在程序开始时（通常是第一次访问类或创建类的对象时）初始化，并且在整个程序运行期间保持存在，直到程序结束。

2. **声明和定义**：
   - 在类内部声明静态数据成员时，需要使用关键字`static`。
   - 在类外部定义静态数据成员，并进行初始化。

3. **访问方式**：
   - 静态数据成员可以通过类名直接访问，也可以通过对象来访问。
   - 通过类名访问的语法：`ClassName::staticMemberName`
   - 通过对象访问的语法：`object.staticMemberName`

4. **示例**：

```cpp
class MyClass {
public:
    static int staticVar; // 静态数据成员声明

    void show() {
        std::cout << "Static Variable: " << staticVar << std::endl;
    }
};

// 静态数据成员定义与初始化
int MyClass::staticVar = 0;

int main() {
    MyClass obj1, obj2;

    // 通过类名访问
    MyClass::staticVar = 5;
    obj1.show(); // 输出：Static Variable: 5

    // 通过对象访问
    obj2.staticVar = 10;
    obj1.show(); // 输出：Static Variable: 10

    return 0;
}
```

### 静态成员函数（Static Member Functions）

1. **定义与特性**：
   - 静态成员函数是类的成员函数，但它不作用于任何具体的对象。
   - 静态成员函数只能访问静态数据成员和其他静态成员函数，**不能**访问非静态成员变量和非静态成员函数，因为它们**不属于任何具体的对象。**
   - 静态成员函数在程序开始时就存在，可以通过类名直接调用，而不需要创建对象。

2. **声明和定义**：
   - 在类内部声明静态成员函数时，需要使用关键字`static`。
   - 在类外部定义静态成员函数时，**不需要**使用`static`关键字。

3. **访问方式**：
   - 静态成员函数通过类名直接访问，也可以通过对象来访问。
   - 通过类名访问的语法：`ClassName::staticFunctionName`
   - 通过对象访问的语法：`object.staticFunctionName`

4. **示例**：

```cpp
class MyClass {
public:
    static int staticVar;

    static void staticFunc() {
        std::cout << "Static Function called. Static Variable: " << staticVar << std::endl;
    }

    void nonStaticFunc() {
        staticFunc(); // 可以在非静态成员函数中调用静态成员函数
    }
};

int MyClass::staticVar = 0;

int main() {
    MyClass obj;

    // 通过类名调用静态成员函数
    MyClass::staticFunc(); // 输出：Static Function called. Static Variable: 0

    // 通过对象调用静态成员函数
    obj.staticFunc(); // 输出：Static Function called. Static Variable: 0

    return 0;
}
```

### 总结

- **静态数据成员**：属于类本身，所有对象共享，通常用于表示**类级别**的属性或常量。
- **静态成员函数**：属于类本身，可以在没有对象的情况下调用，通常用于表示类级别的**操作或工具函数**。



# 

# 类间关系

### 关联, 聚合, 组合, 依赖

**association**: a **has** b, 含有数据成员 the relationship is more permanent. 

人, associate 街道

**aggregation**: a *contains* b, 但不负责销毁b

鸽群, aggregates 鸽子.

**composition**: a *contains* b, a负责销毁b

房子, composition 卧室

**dependency**: a **uses** b. (参数)

翟旭, dependency ozy



在面向对象编程（OOP）中，除了**继承、组合、聚合、关联和依赖**等基本的类间关系外，还有一些更细化的概念，如**强关联、弱关联**以及**泛化**和**实现**。这些关系进一步描述了类与类之间的复杂交互。下面是对这些细化概念的详细解释：

### 强关联（Strong Association）

强关联表示两个类之间的关系非常密切，其中一个类通常包含对另一个类的引用，并且**生命周期和存在性密切相关**。强关联在代码中通常通过**指针或引用**实现，并且一个类**需要明确**知道另一个类的存在。

**示例**：

```cpp
class Department; // 前向声明

class Employee {
private:
    Department* dept; // Employee强关联到Department

public:
    void setDepartment(Department* d) {
        dept = d;
    }

    void work() {
        // Employee的行为依赖于Department
        std::cout << "Working in department" << std::endl;
    }
};

class Department {
private:
    Employee* emp; // Department强关联到Employee

public:
    void setEmployee(Employee* e) {
        emp = e;
    }

    void manage() {
        // Department的行为依赖于Employee
        std::cout << "Managing employee" << std::endl;
    }
};
```

在这个例子中，`Employee`类和`Department`类之间有强关联关系，**两个类需要明确知道对方的存在**。

### 弱关联（Weak Association）

弱关联表示两个类之间的关系比较松散，一个类可能知道另一个类的存在，但不依赖于其生命周期。弱关联通常通过**临时对象或方法参数**来实现，不需要对方的长期存在。

**示例**：

```cpp
class Library {
public:
    void issueBook(Student& student) {
        std::cout << "Issuing book to student" << std::endl;
        student.readBook();
    }
};

class Student {
public:
    void readBook() {
        std::cout << "Reading book" << std::endl;
    }
};
```

在这个例子中，`Library`类和`Student`类之间有弱关联关系，`Library`类通过**方法参数**临时使用`Student`对象。

### 实现（Realization）

**前缀virtual! overwrite后缀!**

实现关系通常用于**描述类与接口**之间的关系，一个类实现了某个接口，意味着这个**类提供了接口定义的所有方法**。实现关系是一种“can-do”关系，表明一个**类具备某种能力**。

**示例**：

```cpp
class Printable {
public:
    virtual void print() = 0; // 纯虚函数，表示接口
};

class Document : public Printable {
public:
    void print() override {
        std::cout << "Printing document" << std::endl;
    }
};
```

在这个例子中，`Document`类实现了`Printable`**接口**。

### 泛化（Generalization）

泛化关系是**继承**关系的一种，表示一个类是另一个类的泛化或**具体化**。泛化关系通常用于表示“is-a”关系，其中子类继承父类的属性和行为。

**示例**：

```cpp
class Shape {
public:
    virtual void draw() = 0; // 纯虚函数
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing circle" << std::endl;
    }
};
```

在这个例子中，`Circle`类是`Shape`类的泛化。

### 子类型化

**继承, 实现.**



#### 依赖(再次强调)（Dependency）

依赖关系表示一个类使用另一个类的对象或方法。**依赖关系通常是临时的**，即一个类在方法中**使用(而不是包含has)**另一个类的实例。

**示例**：

```cpp
class Engine {
public:
    void start() {
        std::cout << "Engine started" << std::endl;
    }
};

class Mechanic {
public:
    void repairEngine(Engine& engine) {
        engine.start();
        std::cout << "Engine repaired" << std::endl;
    }
};
```

在这个例子中，`Mechanic`类依赖于`Engine`类，但这种依赖是临时的，仅在`repairEngine`方法中。

### 总结

- **继承**：表示“is-a”关系，子类继承父类的属性和行为。
- **组合和聚合**：表示“has-a”关系，组合是强依赖，聚合是弱依赖。
- **关联**：表示两个类之间的关系，可以是单向或双向。
- **强关联和弱关联**：表示关联的强度，强关联表示生命周期密切相关，弱关联表示生命周期独立。
- **实现**：表示类实现了接口，提供接口定义的方法。
- **泛化**：表示类之间的继承关系，子类是父类的具体化, **父类是子类的泛化**
- **依赖**：表示一个类临时使用另一个类的实例。

这些类间关系帮助我们设计清晰、可维护的面向对象系统，提升代码的可读性和可扩展性。



##### for example:

动物(Animal)和虎(Tiger)、鸟(Bird)之间是泛化关系；

 鸟(Bird)和企鹅(Penguin)、鸽子(Pigeon)之间是泛化关系；

 鸽子(Pigeon)和鸽群(Pigeon Group)之间是聚合关系；

 鸽子(Pigeon)和飞翔(Fly)之间是实现关系。





## chapter14类的设计

继承, 多态, 封装和信息隐蔽

#### 封装: 抽象, 提炼总结

#### 信息隐蔽:

> [!tip]
>
> 隐藏行为、操作:
>
> 事物的一个行为特征可由多个操作过程构成，在C++中一个操作通常由一个或多个成员函数实现. 设计时，可隐藏全部或部分成员函数
>
> 隐藏数据： 
>
>  面向对象程序设计在抽象时更关注事物的行为特征，在表示时把数据隐藏起来更能体现事物的本质特征。

> [!note]
>
> 减少外部可见行为和数据
> 对象间只通过可见行为交互
>
> 更安全、可靠
> 维护方便
> 便于复用

#### 分离使用和实现: 

类的使用者---调用方

类的实现---成员函数实现、数据的表示、组织等

> [!note]
>
> 建议：
> 尽量减小使用和实现间的耦合度
> 前置声明好于include
> 定义类时尽量减小与运行环境、平台、硬件系统等关联
