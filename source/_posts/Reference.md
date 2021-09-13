---
title: Reference
date: 2021-09-07 09:10:17
tags:
---
# 概念
- **引用的本质：** 给变量起别名
- 语法： `数据类型 & 别名 = 原名`
- 引用必须初始化
- **引用初始化后不可改变**，不能再变成其他变量的别名

# 引用做函数形参
**函数参数传递方式：**
- 值传递
- 地址传递(指针)
- 引用传递

# 引用做函数返回值
**注意：**
- 不要返回局部变量的引用
- 函数的调用可以作为左值

# 引用的本质
- 引用实际上是再C++内部实现一个指针变量
- 指针的操作由编译器帮助实现

## 引用 vs. 指针
- 不存在空引用。引用必须连接到一块合法的内存。
- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。

# 常引用
用 `const` 关键字修饰引用，防止形参改变实参

```cpp
#include <iostream>
using namespace std;


// 交换函数

// 值传递
// void swap(int a, int b)
// {
//     int temp = a;
//     a = b;
//     b = temp;
// }

// 地址传递
void swap(int * a, int * b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// 引用
void swap(int &a, int &b)
{
    int temp = a;
    a = b;
    b = temp;
}


// 引用做函数返回值
int& test()
{
    // int a = 10;// 栈区，函数结束自动释放
    // return a;// INVALID
    static int b = 10;// 全局区
    return b;
}


// 常引用
void showValue(const int &a)
{
    // a = 10000;// INVALID
    cout << a << endl;
}


int main()
{
    int a = 10;
    int &b = a;// 自动转换为 int * const b = &a;
    b = 20;// 自动转换为 *b = 20;
    cout << a << '\t' << b << endl;
    int c = 50;
    swap(a, c);
    swap(&a, &c);

    int &ref = test();
    cout << ref << endl;
    // 左值
    test() = 1000;// a = 1000
    cout << ref << endl;
    cout << endl;

    int anu = 100;
    showValue(anu);
    return 0;
}
```