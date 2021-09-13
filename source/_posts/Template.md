---
title: Template
date: 2021-09-13 20:24:47
tags:
---
- **核心内容：** 泛型编程、STL

# 模板
## 模板的概念
- C++另一种编程思想称为 **泛型编程**，主要利用的技术就是 **模板**
- C++提供两种模板机制： **函数模板** 和 **类模板**
- 建立**通用的模具**，提高代码**复用性**
- 不能直接使用，只是一个框架
- 通用性很强，针对特定一类问题，并不是万能的

## 函数模板
### 函数模板语法
**作用：** 建立一个通用函数，其函数 **返回值类型** 和 **形参类型** 可以不具体指定，用一个 **虚拟的类型** 来代表
**语法：** `template<typename T>`
**解释：**
- `template` 是关键字，声明创建模板
- `typename` 是关键字，表明后面的符号是一种数据类型，可以用 `class` 替换
- `T` 通用的数据类型
- 使类型参数化

```cpp
#include <iostream>
using namespace std;

// 两个函数逻辑极其类似
void swapInt(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}

void swapDouble(double& a, double& b)
{
    int temp = a;
    a = b;
    b = temp;
}

// 一个函数实现各种数据的交换
// 函数模板
template<typename T>// 声明一个模板，告诉编译器后面代码中的T不要报错，T是一个通用数据类型
void mySwap(T& a, T& b)// 使用时再指定
{
    T temp = a;
    a = b;
    b = temp;
}

void test01()
{
    int a = 1;
    int b = 2;
    cout << "a = " << a << "\tb = " << b << endl;

    swapInt(a, b);
    cout << "Swapping..." << endl;
    cout << "a = " << a << "\tb = " << b << endl;
}

void test02()
{
    int a = 1;
    int b = 2;
    cout << "a = " << a << "\t b = " << b << endl;
    // 利用函数模板交换
    // 两种方式使用函数模板
    // 1.自动类型推导
    mySwap(a, b);
    cout << "Swapping..." << endl;
    cout << "a = " << a << "\t b = " << b << endl;
    // 2.显式指定类型
    mySwap<int>(a, b);
    cout << "Swapping..." << endl;
    cout << "a = " << a << "\t b = " << b << endl;
}

int main(int argc, char const *argv[])
{
    // test01();
    test02();
    return 0;
}
```
## 函数模板主要事项
- 自动类型推导，必须推导出 **一致** 的数据类型T
- 模板必须要确定出T的数据类型

```cpp
#include <iostream>
using namespace std;

// 一种思想：typename函数模板，class类模板
template<class T>// typename可以替换为class
void mySwap(T& a, T& b)// 使用时再指定
{
    T temp = a;
    a = b;
    b = temp;
}

template<class T>
void func()
{
    cout << "Calling a func..." << endl;
}

void test01()
{
    int a = 10;
    int b = 20;
    char c = 'c';
    mySwap(a, b);
    // mySwap(a, c);// INVALID
    cout << "a = " << a << "b = " << b << endl;
    // func();// INVALID
    func<int>();//VALID
}

int main(int argc, char const *argv[])
{
    test01();
    return 0;
}
```
## 函数模板案例
```cpp
#include <iostream>
using namespace std;

// 交换数组元素模板
template<typename T>
void mySwap(T& a, T& b)
{
    T temp = a;
    a = b;
    b = temp;
}

// 选择排序模板
template<typename T>
void selectSort(T arr[], int len)
{
    for (int i = 0; i < len; i++)
    {
        int max = i;
        for (int j = i + 1; j < len; j++)
        {
            if (arr[max] < arr[j])
            {
                max = j;
            }
        }
        if (max != i)
        {
            mySwap(arr[max],arr[i]);
        }
    }
}

// 打印数组模板
template<typename T>
void printArry(T arr[], int len)
{
    for (int i = 0; i < len; i++)
    {
        cout << arr[i] << '\t';
    }
    cout << endl;
}

void test01()
{
    char charArr[] = "badcfe";
    int len = sizeof(charArr) / sizeof(char);
    selectSort(charArr, len);
    printArry(charArr, len);
}

void test02()
{
    int arr[] = {7,5,1,3,9,2,4,6,8};
    int len = sizeof(arr) / sizeof(int);
    selectSort(arr, len);
    printArry(arr, len);
}

int main()
{
    // test01();
    test02();
    return 0;
}
```
## 普通函数与函数模板的区别
- 普通函数调用时可以发生 **自动类型转换(隐式类型转换)**
- 函数模板调用时，利用自动类型推导，不会发生隐式类型转换
- 利用显式指定类型，可以发生隐式类型转换

```cpp
#include <iostream>
using namespace std;

int myAdd01(int a, int b)
{
    return a + b;
}

template<typename T>
T myAdd02(T a, T b)
{
    return a + b;
}

void test01()
{
    int a = 10;
    int b = 20;
    char c = 'c';
    cout << myAdd01(a, b) << endl;
    cout << myAdd01(a, c) << endl;// 转换ASCII码运算

    // 自动类型推导
    // cout << myAdd02(a, c) << endl;// INVALID

    // 显式指定类型
    // 一切按int类型为准计算，非int类型自动转换
    cout << myAdd02<int>(a, c) << endl;// VALID
}

int main()
{
    test01();
    return 0;
}
```
## 普通函数与函数模板的调用规则
普通函数和函数模板可以 **重载**
**调用规则：**
- 如果函数模板和普通函数都可以实现，优先调用 **普通函数**
- 可以通过 **空模板参数列表** 来强制调用函数模板
- 函数模板也可以发生函数重载
- 如果函数模板可以产生更好的匹配(不发生隐式类型转换)，优先调用函数模板
- 实际开发中，提供了函数模板，最好不要提供普通函数

```cpp
#include <iostream>
using namespace std;

void myPrint(int a, int b);

template<typename T>
void myPrint(T a, T b)
{
    cout << "调用函数模板" << endl;
}

template<typename T>
void myPrint(T a, T b, T c)
{
    cout << "调用重载函数模板" << endl;
}

void test01()
{
    int a = 10;
    int b = 20;
    int c = 30;
    myPrint(a, b);
    myPrint<>(a, b);// 强制调用函数模板
    myPrint(a, b, c);

    char c1 = 'a';
    char c2 = 'd';
    myPrint(c1, c2);// 调用普通函数要发生隐式类型模板，故调用函数模板
}

int main(int argc, char const *argv[])
{
    test01();
    return 0;
}

void myPrint(int a, int b)
{
    cout << "调用普通函数" << endl;
}
```
## 模板的局限性
- 针对自定义类型，提供模板的重载，可以为特定的类型提供 **具体化的模板**
- 语法： `template<> 返回值类型 函数名(特定类)` 实现具体化重载
- 学习模板是为了在STL中运用系统提供的模板