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