---
title: Class and Object
date: 2021-08-30 11:36:24
tags:
---
- 对象具有 **属性** 和 **行为**
- 具有相同性质的对象抽象为 **类**
- **面向对象** 具有三大特性: **封装**、 **继承**、 **多态**
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# 封装
## 封装的意义
1. 将属性和行为作为一个整体，表现生活中的事务
2. 将属性和行为加以 **权限控制**

**示例1：** 设计一个圆类，计算圆的周长
```cpp
#include <iostream>
#include <string>
using namespace std;

const double PI = 3.1415926;
class Circle
{
public:// 访问权限-公共权限
    // 属性
    int r;
    // 行为
    double calculate()
    {
        return 2 * PI * r;
    }
};

int main()
{
    // 实例化
    Circle c1;
    c1.r = 10;
    cout << "Circumference = " << c1.calculate() << endl;
    cout << endl;
    return 0;
}
```
**示例2：** 设计一个学生类，有姓名和学号两个属性，可以给姓名和学号赋值，可以显示姓名和学号
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student
{
public:
    string sName;
    int iID;
    Student(string Name, int ID)
    {
        sName = Name;
        iID = ID;
    }
    void setName(string Name)
    {
        sName = Name;
    }
    void setID(int ID)
    {
        iID = ID;
    }
    void showStudent()
    {
        cout << "Name: " << sName << "\tID: " << iID << endl;
    }
};

int main()
{
    Student s1("Legolas", 100545);
    s1.showStudent();
    return 0;
}
```

## 成员访问权限
- 类中 **属性** 和 **行为** 统一称为 **成员**
    - 属性、成员属性、成员变量
    - 行为、成员函数、成员方法

权限范围 | 关键字 | 说明
-----|-----|---
公共权限 | public | 成员 类内可以访问，类外可以访问
保护权限 | protected | 成员 类内可以访问，类外不可以访问 **子类** 可以访问 **父类** 的保护内容
私有权限 | private | 成员 类内可以访问，类外不可以访问

**注：** 权限对于 **属性** 和 **行为** 均适用

**示例3：**
```cpp
#include <iostream>
#include <string>
using namespace std;

class Person
{
public:
    string sName;
protected:
    string sCar;// 汽车
private:
    int iPassword;// 银行卡密码
private:
    void func()
    {
        sName = "Legolas";
        sCar = "BMW";
        iPassword = 445621;
    }
};

int main()
{
    Person p1;
    p1.sName = "Undomiel";// 公共权限，类外可以访问
    return 0;
}
```

## struct和class区别
- struct 默认权限为 **公共**
- class 默认权限为 **私有**

**示例4：**
```cpp
#include <iostream>
#include <string>
using namespace std;

class C1
{
    int m_A;
};
struct C2
{
    int m_B;
};

int main()
{
    // C1 a1;
    // a1.m_A = 1;//INVALID
    C2 a2;
    a2.m_B = 100;
    cout << a2.m_B << endl;
    return 0;
}
```

## 成员属性设置为私有
1. 自己控制读写权限
2.  对于写的权限（**设置数据**），检测数据的有效性，防止不合理的数据

**示例5：**
```cpp
#include <iostream>
#include <string>
using namespace std;

class Personn
{
private:
    string sName;// 读写权限
    int iAge;// 只读 -> 读写权限，合理范围
    string sLover;// 只写
public:
    void setName(string name)
    {
        sName = name;
    }
    string getName()
    {
        return sName;
    }
    int getAge()
    {
        // iAge = 0;
        return iAge;
    }
    void setLover(string lover)
    {
        sLover = lover;
    }
    void setAge(int age)
    {
        if (age < 0 || age > 900)
        {
            iAge = 0;
            return;
        }
        iAge = age;
    }
};

int main()
{
    Personn p;
    p.setName("Legolas");
    p.setAge(375);
    cout << "Name: " << p.getName();
    cout << "\tAge: " << p.getAge();
    p.setLover("Undomiel");
    return 0;
}
```
# 对象的初始化和清理
- 电子产品的出厂设置，不用时删除自己信息数据保证安全
- 每个对象也应该有 **初始设置** 以及对象销毁前的 **清理数据** 的设置

## 构造函数和析构函数
对象的 **初始化和清理** 是两个非常重要的安全问题
- 一个对象没有初始状态，对其使用后果是未知的
- 使用完一个对象，要及时清理，避免安全问题

C++利用 **构造函数** 和 **析构函数** 解决 **初始化和清理** 的问题，这两个函数将会被编译器 **自动调用**，完成对象初始化和清理的工作。
对象的初始化和清理工作是编译器 **强制要求** 我们做的事，因此 ***如果我们不提供构造和析构，编译器会自己提供***，编译器提供的构造函数和析构函数是 **空实现**。
- **构造函数：** 创建对象时为对象的成员属性赋值
- **析构函数：** 对象 **销毁** 前系统自动调用，执行一些清理工作

**构造函数语法：** `类名(){}`
1. 没有返回值，也不写void
2. 函数名和类名相同
3. 可以有参数，因此可以发生 **重载**
4. 创建对象会自动调用，只会调用一次

**析构函数语法：** `~类名(){}`
1. 没有返回值，也不写void
2. 不可以有参数，不可以 **重载**
3. 程序在对象销毁前会自动调用析构，只调用一次

```cpp
#include <iostream>
using namespace std;

class Person
{
private:
    /* data */
public:
    Person();
    ~Person();
};

Person::Person()// constructor
{
    cout << "calling a constructor function" << endl;
}

Person::~Person()// destructor
{
    cout << "calling a destructor function" << endl;
}


int main()
{
    Person p;
    system("pause");
    return 0;
}
```
## 构造函数的分类及调用
- 按 **参数** 分：
    1. 有参构造
    2. 无参构造(编译器默认，默认构造)
- 按 **类型** 分：
    1. 普通构造
    2. 拷贝构造，不能修改原本的对象 `ClassName(const ClassName & ObjectName)`

调用：
1. 括号法
2. 显示法
3. 隐式转换法

**注意事项：**
1. 调用默认构造函数，不要加括号()，加括号()编译器会认为是函数的声明，`Person p1();`会认为是 `返回值类型 函数名();`
2. 不要利用拷贝构造函数 初始化 **匿名对象**，编译器会认为是对象声明 `Person(p3)` 认为是 `Person p3;`

```cpp
#include <iostream>
using namespace std;

class Person
{
private:
    int age;
public:
    Person();
    Person(int a);
    Person(const Person &p);// const限定修改，引用传递
    ~Person();
};

Person::Person()// constructor
{// 无参构造(默认构造)
    cout << "calling a constructor function with no parameters" << endl;
}

Person::Person(int a)// constructor
{// 有参构造
    age = a;
    cout << "calling a constructor function" << endl;
}

Person::Person(const Person &p)// 拷贝构造
{
    // 拷贝传入对象的属性
    age = p.age;
    cout << "calling a copy constructor function" << endl;
}

Person::~Person()// destructor
{
    cout << "calling a destructor function" << endl;
}


int main()
{
    // 括号法
    Person p1;// 默认构造函数调用
    Person p2(10);// 有参构造函数调用
    Person p3(p2);// 拷贝构造函数

    // 显示法
    Person p4;
    Person p5 = Person(10);// Person(10)单独拿出来是匿名对象
    Person p6 = Person(p5);// 当前行结束后，系统会立即回收
    cout << "test" << endl;
    Person(10);
    cout << "test" << endl;

    // 隐式转换法
    Person p7 = 10;// Person p7 = Person(10);
    Person p8 = p7;
    system("pause");
    return 0;
}
```



