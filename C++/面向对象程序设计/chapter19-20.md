# chapter19-20

## chapter19**多态性及其应用**

多态性：相同的消息请求，执行不同的代码体，从而有不同的行为后果。


静态多态: 根据目标对象的静态类型和参数表中参数的静态类型确定目标代码体。
模板-不同的模板参数
函数重载

动态多态



### 静态多态-模板

```cpp
#include <iostream>
#include <string>

using namespace std;

template<typename T>
class My
{
public:
	void f(const T& x)
	{
		cout << typeid(x).name() << endl;
	}
};

int main()
{
	My<int>obj1;
	My<float>obj2;

	obj1.f(10);//输出int
	obj2.f(20);//输出float
}
```

### 静态多态-函数重载

```go
//略
```

### 动态多态性

动态多态：
根据目标对象的动态类型和参数表中参数的静态类型确定目标代码体。（虚机制）
根据目标对象的动态类型和参数表中参数的动态类型确定目标代码体。**（C++不支持）**

#### C++中的动态多态性-例

```cpp
class B;
class A
{
public:
    virtual ~A( ) { }
    virtual void f(A *)  { cout<<1<<endl;}
    virtual void f(B *)  { cout<<2<<endl; }
};

class B:public A
{
public:
     virtual ~B( ){ }
     virtual void f(A *)  { cout<<3<<endl;}
     virtual void f(B *)  { cout<<4<<endl;}
};
```

```cpp
int main()
{
    B b;
    A*pa = &b; //&b隐式转换为*B
    pa->f(&b);//4
    pa->f(pa);//3
    b.f(pa);//3
    return 0;
}
```

#### 虚机制的作用

虚机制是实现动态多态的一种方法；
意义-在保持客户端访问接口不变的前提下，可以变更类的实现

#### 子类型化和适应变化

![image-20240629201603214](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240629201603214.png)

```cpp
Parent * p = new Child1;
p->Func( );
delete p;

Child2  myObj;
Parent& obj = myObj;
obj.Func( );

void Proc(Parent * p) 
{     p->Func();   }
```

##### eg:例1-父类提供接口，子类提供具体实现

![image-20240629202006877](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240629202006877.png)

```cpp
class Fruit
{
public:
	int Energy() const
	{
		return this->m_energy;;
	}
private:
	int m_energy;
};
class Mouse
{
public:
	void eat(Fruit& fruit)
	{
		weight += fruit.Energy() * 0.15;
	}
private:
	int weight;
};
```

##### 例2--父类提供框架，子类提供细节

![image-20240629202032527](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240629202032527.png)

##### 例3--虚拟的拷贝构造

问题：

1. 拷贝构造函数不能是虚的；
2.即使能虚，各类中函数名字也不能相同

![image-20240629202254408](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240629202254408.png)

虚机制的意义:

使用虚机制，使得当变更子类的具体实现时，不用改客户端XXX类的定义及实现



使用继承和虚机制的不足:

![image-20240629202342115](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240629202342115.png)

