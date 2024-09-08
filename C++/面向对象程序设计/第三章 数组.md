# 第三章 数组

```c++
#include<iostream>
using namespace std;

using int_array = int[4];
void test01()
{
	int array[3][4];
	for(int_array *p=array;p!=array+3;p++)
		for(int*q=*p;q!=*p+4;q++)
			cout<<*q<<" ";
}


/*int array[4] = {1, 2, 3, 4};
int* p = array;      // p 指向 array 的第一个元素，即 &array[0]
int* q = array + 4;  // q 指向 array 的“超尾”元素，即 &array[4]
*/

#define Row 3
#define Col 4
void test02()
{
	int cnt = 1;

	int array[Row][Col];
	for(auto& row:array)
	{
		for (auto& col : row)
		{
			col = cnt;
			cnt++;
			cout << col << " ";
		}cout << endl;
	}
	
}

int main()
{
	//test01();
	test02();
	return 0;
}
```

# 第四章 表达式

##### 4.1 基础 

如果改变了某对象值, 在表达的是其他地方不要再使用这个运算对象.

```C++
cout<<i<<i++<<endl;//输出结果未知
//唯一例外:
//在*++iter里, 递增运算必须先求值, 然后再解引用运算
```

##### 4.2 算数运算符

![](C:\Users\10164\AppData\Roaming\Typora\typora-user-images\image-20240601192835872.png)

##### 4.3 关系运算符

```c++
void test03()
{
	const char*cp = "hello world";
	if (cp && *cp)
		cout << cp << endl;/*指针 cp 指向的地址有效且该地址处的值不为空字符时，条件成立*/
}

```

##### 4.4 赋值运算符

赋值运算符优先级低于关系运算符

##### 4.5 递增和递减运算符

尽量使用前置运算符, 后置版本将对象原始值副本作为**右值**返回, 前置版本将对象本身作为左值返回.

```C++
cout<<*iter++<<endl;
//same as
cout<<*iter<<endl;
++iter;
```

##### 4.6 成员访问运算符

如果一条子表达式改变了某个运算对象的值，另一条子表达式又要使用该值的话，运算对象的求值顺序就很关键了。

##### 4.7 条件运算符

?:照搬if else 逻辑, ?: 可以嵌套

```C++
string finalgrade;
finalgrade=(grade>90)?"highGrade":(grade<60)?"fail":"pass";
```

条件运算符优先级很低 (link P 135)

##### 4.8 位运算符

> [!NOTE]
>
> &位与, | 位或, ^位反, <<左移, >>右移.

移位运算符的优先级介于中间: **比算术运算符低**, 比关系运算符, 赋值运算符, 条件运算符高. 

##### 4.9 sizeof运算符

右结合, 不实际计算运算对象值, 返回值位常量表达式, 返回值可以用来声明数组的维度.

##### 4.10 逗号运算符

从左到右依次求值, 依次丢掉结果, 返回值位最右侧表达式的值, 若其为左值, 则最终求值结果也是左值. 

##### 4.11 类型转换

1.  int 类型小的整型值首先提升为较大的整数类型。
2. 非布尔值转换成布尔类型。
3. 非布尔值转换成布尔类型。
4. 算术运算或关系运算的运算对象有多种类型，需要转换成同一种类型。
5. 函数调用时也会发生类型转换。

###### 4.11.1 算数转换

算术转换: 将运算对象转换为最宽的类型

整型提升: 小整数提升为大整数, 较大char提升至小整数最小的类型

无符号类型的符号运算: 







