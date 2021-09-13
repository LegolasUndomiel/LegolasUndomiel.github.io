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

**示例：**
```cpp
#include <iostream>
using namespace std;

class Person
{
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

**示例：**
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
## 拷贝构造函数
拷贝构造函数调用时机：
- 使用一个创建完毕的对象初始化一个新对象
- 值传递的方式给函数参数传值
- 以值方式返回局部对象

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
    Person(const Person& a);
    ~Person();
};

Person::Person()
{
    cout << "calling a default constructor function" << endl;
}

Person::Person(int a)
{
    cout << "calling a constructor function" << endl;
    age = a;
}

Person::Person(const Person& a)
{
    cout << "calling a copy constructor function" << endl;
    age = a.age;
}

Person::~Person()
{
    cout << "calling a destructor function" << endl;
}


void test01(Person p)
{
}
Person dowork01()
{
    Person p;
    return p;
}
void test03()
{
    Person p = dowork01();
}


int main()
{
    // 初始化新对象
    Person p1(20);
    Person p2(p1);
    cout << endl;

    // 值传递
    test01(p1);
    cout << endl;

    // 值方式返回
    // 返回值优化
    test03();// 编译器优化使得观察不到调用拷贝构造函数

    return 0;
}
```

## 构造函数调用规则
默认情况下，C++编译器给一个类添加三个函数：
1. 默认构造函数(无参，空实现)
2. 默认析构函数(无参，空实现)
3. 默认拷贝构造函数，对属性进行 **值拷贝**

构造函数调用规则如下：
- 如果定义有参构造函数，不再提供默认构造函数，但是会提供默认拷贝构造函数
- 如果定义拷贝构造函数，不再提供其他构造函数

## 深拷贝和浅拷贝
- 浅拷贝：简单的赋值拷贝操作
    - 属性有在堆区开辟的，堆区内存重复释放，非法操作内存
- 堆区重新申请空间，进行拷贝操作

```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    int age;
    int * height;
    Person();
    Person(int a, int h);
    Person(const Person& a);
    ~Person();
};

Person::Person()
{
    cout << "calling a default constructor function" << endl;
}

Person::Person(int a, int h)
{
    cout << "calling a constructor function" << endl;
    age = a;
    height = new int(h);
}

Person::Person(const Person& a)
{
    cout << "calling a deep copy constructor function" << endl;
    age = a.age;
    // height = a.height;// 编译器默认实现的效果
    height = new int(*a.height);
}

Person::~Person()
{
    // 将堆区开辟的数据做释放
    if (height != NULL)
    {
        delete height;
        height = NULL;// 防止野指针
    }
    cout << "calling a destructor function" << endl;
}


void test01()
{
    Person p1(18, 160);
    cout << "p1年龄： " << p1.age << "身高为： " << p1.height << endl;
    Person p2(p1);// 使用编译器默认拷贝构造函数
    cout << "p2年龄： " << p2.age << "身高为： " << p2.height << endl;
    // 浅拷贝：堆区内存重复释放，非法操作内存
}

int main()
{
    test01();
    return 0;
}
```
## 初始化列表
**作用：** 初始化属性
**语法：**
- `ClassName(): Property1(Value1)...{}`
- `ClassName(Type Property1, ...): Property1(Value1)...{}`

## 类对象作为类成员
C++类中的成员可以是另一个类的对象，称为 **对象成员**
- 构造时，先构造 **对象成员** 再构造 **自身**
- 析构时，先释放 **自身** 再释放 **对象成员**

```cpp
#include <iostream>
#include <string>
using namespace std;

class Phone
{
public:
    string pName;
    Phone(string n);
    ~Phone();
};

Phone::Phone(string n): pName(n)
{
    cout << "Calling constructor of Phone class" << endl;
}

Phone::~Phone()
{
    cout << "Calling destructor of Phone class" << endl;
}


class Person
{
public:
    string name;
    Phone phone;
    Person(string n, string pn);
    ~Person();
};

// 相当于Phone phone = pn 隐式转换法
Person::Person(string n, string pn): name(n),phone(pn)
{
    cout << "Calling constructor of Person class" << endl;
}

Person::~Person()
{
    cout << "Calling destructor of Person class" << endl;
}


void test01()
{
    Person p("Legolas", "Nokia");
    cout << p.name << "拿着" << p.phone.pName << endl;
}

int main()
{
    test01();
    return 0;
}
```
## 静态成员
用关键字 `static` 修饰成员变量和成员函数，静态成员分为：
- 静态成员变量
    - 所有对象共享同一份数据
    - 在 **编译阶段** 分配内存，全局区
    - 类内声明，类外初始化
    - 访问：
        - 受 **访问权限** 限制
        - 通过 **对象** 访问
        - 通过 **类名** 访问
- 静态成员函数
    - 所有对象共享同一个函数
    - 静态成员函数 **只能** 访问 **静态成员变量**，对于非静态成员变量，无法区分操作哪个对象的变量
    - 受 **访问权限** 限制

```cpp
#include <iostream>
using namespace std;
class Person
{
private:
    static int b;
    int c;
public:
    static int a;
    Person();
    ~Person();
    static void func();
};

Person::Person()
{
}

Person::~Person()
{
}

void Person::func()
{
    a++;
    b++;
    // 不知道操作哪个对象的属性
    // c = 200;// INVALID
    cout << "Calling a static member function" << endl;
}

int Person::a = 100;// 初始化
int Person::b = 100;// 初始化

void test01()
{
    Person p1;
    cout << p1.a << endl;

    Person p2;
    p2.a = 200;
    cout << p2.a << endl;
}
void test02()
{
    Person p;
    // 通过对象访问
    cout << p.a << endl;

    // 通过类名访问
    cout << Person::a << endl;

    // 静态成员变量有访问权限
    // cout << Person::b << endl;// INVALID
}
void test03()
{
    // 通过对象访问
    Person p;
    p.func();

    // 通过类名访问
    Person::func();
}

int main()
{
    // test01();
    // test02();
    test03();
    return 0;
}
```
# C++对象模型和this指针
## 成员变量和成员函数分开存储
- 只有 **非静态成员变量** 才属于类的对象
- 静态成员、非静态成员函数 不属于某一个对象，只有一份，分开存储

```cpp
#include <iostream>
using namespace std;

class Person
{
private:
    int a;// 非静态成员变量 属于类的对象上
    static int b;// 静态成员变量 不属于类对象上
public:
    Person();
    ~Person();
    void func(){}// 非静态成员函数 不属于类对象上
    static void foo(){}// 静态成员函数 不属于类对象上
};

Person::Person()
{
}

Person::~Person()
{
}

int Person::b = 5;

void test01()
{
    Person p;
    // 空对象占用内存空间为：1
    // C++编译器给每个空对象分配一个字节空间，区分空对象占内存的位置
    // 每个空对象也应该有独一无二的内存地址
    cout << "sizeof(p)" << sizeof(p) << endl;
}

int main()
{
    test01();
    return 0;
}
```
## this指针
每个非静态成员函数只有一份函数实例，多个类型的对象会共用一块代码
- **问题是：** *代码如何区分是哪个对象在调用自己？*
- this指针指向 **被调用的成员函数所属的对象**
- this指针隐含在每一个非静态成员函数内，不需要定义，直接使用
- this指针的 **本质** 是一个指针常量，指针的指向不可以修改 `ClassName * const this`
- 在成员函数中使用属性相对于 `this->Property`

**this指针的用途：**
- 形参和成员变量同名时，可以用this指针区分
- 返回对象本身可以使用 `return *this`

```cpp
#include <iostream>
using namespace std;
class Person
{
public:
    int age;
    Person(int age);
    Person(const Person &p)
    {
        age = p.age;
        cout << "Calling a copy constructor" << endl;
    }
    ~Person();
    void PersonAddAge(Person & p)
    {
        this->age += p.age;
    }
    Person & PersonAdd(Person & p)// 返回值 和 返回引用 的区别
    // Person PersonAdd(Person & p)// 返回值 发生复制 类似与 值传入
    {
        this->age += p.age;
        return *this;
    }
};

Person::Person(int age)
{
    // age = age;
    this->age = age;// this指向p1
}

Person::~Person()
{
}


void test01()
{
    Person p1(18);
    cout << p1.age << endl;
}
void test02()
{
    Person p1(10);
    Person p2(10);
    p2.PersonAddAge(p1);
    cout << "Age = " << p2.age << endl;

    // 链式编程思想 e.g. cout
    Person p3 = p2.PersonAdd(p1).PersonAdd(p1);
    cout << "Age = " << p2.age << endl;
    cout << "Age = " << p3.age << endl;
}


int main(int argc, char const *argv[])
{
    // test01();
    test02();
    return 0;
}
```
## 空指针访问成员函数
C++中允许空指针调用成员函数，要注意有没有用到this指针
```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    int age;
    Person();
    ~Person();
    void showClassName()
    {
        cout << "this is Person class" << endl;
    }
    void showPersonAge()
    {
        // 预防破坏
        if (this == NULL)
        {
            return;
        }

        // 传入的指针为NULL
        cout << "age = " << age << endl;// this->age
    }
};

Person::Person()
{
}

Person::~Person()
{
}

void test01()
{
    Person * p = NULL;
    p->showClassName();
    p->showPersonAge();
}

int main(int argc, char const *argv[])
{
    test01();
    return 0;
}
```
## const修饰成员函数
**常函数：**
- 常函数不可以修改成员属性
- 成员属性声明加关键字 `mutable` 后，在常函数中仍可修改
- `返回值类型 成员函数名() const`
- 此时this指针修改为 `const ClassName * const this` 因此不能修改成员属性

**常对象：**
- 常对象只能调用常函数
- 构造语法： `const ClassName ObjectName`

# 友元
使用 **友元** 技术，可以让类外特殊的 **函数或类** 访问 **私有属性**
关键字 `friend`
## 全局函数做友元
**语法：** 在类中用 `friend 返回值类型 函数名();` 声明
## 类做友元
**语法：** 在类中用 `friend class 类名;` 声明该类是本类的友元，可以访问私有属性
## 成员函数做友元
限定类中特殊成员函数可以访问，局部授权
**语法：** 在类中用 `friend 返回值类型 类名::函数名();` 声明
# 运算符重载
对已有运算符重新定义，赋予其另一种功能，以适应不同的数据类型
- 对于内置数据类型，编译器知道如何运算
- 对于自定义数据类型，使用运算符重载
- 通过成员函数、全局函数重载运算符
- 运算符重载也可以发生 **函数重载**

## 加号运算符重载
- **作用：** 实现两个自定义数据类型相加运算
- **全局函数重载：** `ClassName operator+(const ClassName & Object1, const ClassName & Object2)`
- **成员函数重载：** `ClassName operator+(const ClassName & Object)`

## 左移运算符重载
- **作用：** 实现输出自定义数据类型
- 只能用全局函数重载
- **语法：** `ostream & operator<<(ostream & output, const ClassName & Object)`

```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    int a;
    int b;
    Person();
    Person(const Person & p);
    ~Person();
    // Person & operator+(const Person & p);// 成员函数重载运算符+，需要自己管理内存
    Person operator+(const Person & p);// 成员函数重载运算符+
    // void operator<<(cout)// 实质：p.operator<<(cout) 简化：p << cout
    // 不能用成员函数重载<<运算符，只能用全局函数重载<<运算符
    friend ostream & operator<<(ostream & out, const Person & p);// 友元全局函数
};

Person::Person()
{
}

Person::Person(const Person & p)
{
    this->a = p.a;
    this->b = p.b;
    cout << "Calling a copy constructor" << endl;
}

Person::~Person()
{
}

// Person & Person::operator+(const Person & p)
// {
    // Person * temp = new Person;
    // temp->a = this->a + p.a;
    // temp->b = this->b + p.b;
    // cout << "Calling a member function" << endl;
    // return *temp;
// }
Person Person::operator+(const Person & p)
{
    Person temp;
    temp.a = this->a + p.a;
    temp.b = this->b + p.b;
    cout << "Calling a member function" << endl;
    return temp;
}

Person operator+(const Person & a, const Person & b)// 全局函数重载
{
    Person temp;
    temp.a = a.a + b.a;
    temp.b = a.b + b.b;
    cout << "Calling a function" << endl;
    return temp;
}

Person operator+(const Person & a, const int & b)// 运算符重载-函数重载
{
    Person temp;
    temp.a = a.a + b;
    temp.b = a.b + b;
    return temp;
}

ostream & operator<<(ostream & out, const Person & p)// 输出自定义类型
{
    out << "a = " << p.a << "\tb = " << p.b;
    return out;
    // 实质：operator<<(cout, p);
    // 简化：cout << p;
}

void test01()
{
    Person p1;
    p1.a = 10;
    p1.b = 10;
    Person p2;
    p2.a = 10;
    p2.b = 10;
    Person p3 = p1 + p2;
    Person p4 = p3 + 10;// 函数重载
    // Person p3 = p1.operator+(p2);// 成员函数重载本质
    // Person p3 = operator+(p1, p2);// 全局函数重载本质
    cout << p3.a << p3.b << endl;
    cout << p4.a << p4.b << endl;

    cout << p1 << endl;// 使用链式编程思想
}
void test02()
{
    Person p1;
    p1.a = 10;
    p1.b = 10;
    Person p2;
    p2.a = 10;
    p2.b = 10;
    cout << p1 + p2 << endl;
    Person p3 = p1 + p2;
    cout << p3 << endl;
}

int main()
{
    test01();
    // test02();
    return 0;
}
```

## 自增运算符重载

```cpp
#include <iostream>
using namespace std;
// 重载自增运算符++

class MyInteger
{
private:
    int num;
public:
    MyInteger();
    ~MyInteger();
    friend ostream & operator<<(ostream & output, MyInteger m);
    // 重载前置自增运算符++
    MyInteger & operator++()// 返回引用对一个对象进行自增操作
    {
        num++;
        return *this;
    }
    // 重载后置自增运算符++
    MyInteger operator++(int)// int占位，使得可以重载，可以用于区分前置和后者
    {
        // 先记录结果
        MyInteger temp;
        // 自增
        num++;
        // 记录结果返回
        return temp;
    }
};

MyInteger::MyInteger()
{
    num = 0;
}

MyInteger::~MyInteger()
{
}

ostream & operator<<(ostream & output,const MyInteger m)
{
    output << m.num;
    return output;
}

void test01()
{
    MyInteger myint;
    cout << ++(++myint) << endl;
    cout << myint << endl;
}
void test02()
{
    MyInteger myint;
    cout << myint++ << endl;
    cout << myint << endl;
}

int main(int argc, char const *argv[])
{
    // test01();
    test02();
    return 0;
}
```

## 赋值运算符重载
- 编译器提供赋值运算符 `operator=` 对属性进行值拷贝
- 如果类中有属性指向 **堆区**，赋值操作会出现浅拷贝的问题

```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    int * age;
    Person(int Age);
    ~Person();
    Person & operator=(const Person & p);
};

Person::Person(int Age)
{
    age = new int(Age);
}

Person::~Person()
{
    if (age != NULL)
    {
        delete age;
        age = NULL;
    }
}
// 重载 赋值运算符
Person & Person::operator=(const Person & p)
{
    // 编译器提供 浅拷贝
    // age = p.age;

    // 应该先判断是否有属性在堆区，如果有先释放干净，再深拷贝
    if (age != NULL)
    {
        delete age;
        age = NULL;
    }
    // 深拷贝
    age = new int(*p.age);
    // 返回自身，链式编程
    return *this;
}

void test01()
{
    Person p1(18);
    Person p2(19);
    Person p3(30);
    p2 = p1;// 未重载赋值运算符，使用编译器默认值拷贝，析构时重复释放(浅拷贝)
    p3 = p2 = p1;
    cout << *p1.age << endl;
    cout << *p2.age << endl;
    cout << *p3.age << endl;
}


int main(int argc, char const *argv[])
{
    test01();
    return 0;
}
```

## 关系运算符重载
- 判断自定义类型的关系(==,<,>,!=)
- `bool operator==(cnost ClassName & Object)`
- `bool operator<(cnost ClassName & Object)`
- `bool operator>(cnost ClassName & Object)`
- `bool operator!=(cnost ClassName & Object)`

## 函数调用运算符重载
- 函数调用运算符 `()`
- 由于重载后使用方式非常像函数的调用，称之为 **仿函数**，*在 `STL` 中应用较多*，非常灵活
- `void operator()(形参){}`

**匿名函数对象：** `类名()`
# 继承
- 下级别的成员拥有上级别的共性，还有自己的特性
- 利用 **继承** 的技术，减小代码重复
- `class A : 继承方式 class B`
    - A类称为 **子类** 或 **派生类**
    - B类称为 **父类** 或 **基类**
    - **继承方式：** public   protected   private

```cpp
#include <iostream>
using namespace std;

// 不使用 继承 技术
// Java 页面
class Java
{
public:
    Java();
    ~Java();
    void header()
    {
        cout << "首页、公开课、登录、注册...(公共分类列表)" << endl;
    }
    void footer()
    {
        cout << "帮助中心、交流合作...(公共底部)" << endl;
    }
    void left()
    {
        cout << "Java,Python,C++,...(公共分类列表)" << endl;
    }
    void content()
    {
        cout << "Java学科视频" << endl;
    }
};

Java::Java()
{
}

Java::~Java()
{
}

// Python页面
class Python
{
public:
    Python();
    ~Python();
    void header()
    {
        cout << "首页、公开课、登录、注册...(公共分类列表)" << endl;
    }
    void footer()
    {
        cout << "帮助中心、交流合作...(公共底部)" << endl;
    }
    void left()
    {
        cout << "Java,Python,C++,...(公共分类列表)" << endl;
    }
    void content()
    {
        cout << "Python学科视频" << endl;
    }
};

Python::Python()
{
}

Python::~Python()
{
}

// 使用 继承 技术
class BasePage
{
public:
    BasePage();
    ~BasePage();
    void header()
    {
        cout << "首页、公开课、登录、注册...(公共分类列表)" << endl;
    }
    void footer()
    {
        cout << "帮助中心、交流合作...(公共底部)" << endl;
    }
    void left()
    {
        cout << "Java,Python,C++,...(公共分类列表)" << endl;
    }
};

BasePage::BasePage()
{
}

BasePage::~BasePage()
{
}

// C++页面
class Cpp : public BasePage
{
public:
    Cpp();
    ~Cpp();
    void content()
    {
        cout << "C++学科视频" << endl;
    }
};

Cpp::Cpp()
{
}

Cpp::~Cpp()
{
}


void test01()
{
    Java Ja;
    Ja.header();
    Ja.footer();
    Ja.left();
    Ja.content();
}
void test02()
{
    Python Py;
    Py.header();
    Py.footer();
    Py.left();
    Py.content();
}
void test03()
{
    Cpp cpp;
    cpp.header();
    cpp.footer();
    cpp.left();
    cpp.content();
}


int main()
{
    test01();
    test02();
    test03();
    return 0;
}
```
## 继承方式
**继承规则：**
- 父类中 **私有属性** 三种继承方式 **都不可访问**
- 公共继承  public，父类中 **公共属性** 和 **保护属性** **访问权限不变**
- 保护继承  protected，父类中 **公共属性** 和 **保护属性** 变为 **保护类型**
- 私有继承  private，父类中 **公共属性** 和 **保护属性** 变为 **私有属性**

## 继承中的对象模型
- 父类中 **非静态成员属性** 都会被继承
- 私有成员属性是被编译器 **隐藏**，访问不到，但确实继承了

**查看类的布局：**
- GCC 7.x及更早版本：`g++ -fdump-class-hierarchy fileName`
- GCC 8.x： `g++ -fdump-lang-class fileName`
- Visual Studio: 开发人员命令提示符 `cl /d1 reportSingleClassLayout类名 文件名`

## 继承中的构造和析构顺序
创建子类对象，也会调用父类的构造函数
**构造顺序：**
- 构造父类对象
- 构造子类对象

**析构顺序：**
- 析构子类对象
- 析构父类对象

## 继承同名成员处理方式
子类和父类出现同名的成员，如何访问数据？
- 访问 **子类** 同名成员    **直接访问**即可
    - **语法：** `Object.Property`
    - **语法：** `Object.MemberFunction`
- 访问 **父类** 同名成员    **需要加作用域**
    - **语法：** `Object.BaseClass::Property`
    - **语法：** `Object.BaseClass::MemberFunction`

**注：** 如果子类中出现和父类同名的成员函数，父类中所有同名成员函数隐藏，想访问父类中隐藏的同名成员函数，需要加作用域

## 继承同名静态成员处理方式
静态成员和非静态成员出现同名，处理方式一致。
- 通过类名访问：
    - `Subclass::BaseClass::MemberFunction`

## 多继承语法
C++允许 **一个类继承多个类**
语法： `class 子类 : 继承方式 父类 , ...`
实际开发中不建议用
```cpp
#include <iostream>
using namespace std;

class Base
{
public:
    int a;
    Base();
    ~Base();
protected:
    int b;
private:
    int c;
};

Base::Base()
{
    a = 100;
    b = 200;
    c = 300;
    cout << "Calling a Base constructor" << endl;
}

Base::~Base()
{
    cout << "Calling a Base destructor" << endl;
}

class Base2
{
public:
    int a;
    Base2();
    ~Base2();
};

Base2::Base2()
{
    a = 400;
    cout << "Calling a Base2 constructor" << endl;
}

Base2::~Base2()
{
    cout << "Calling a Base2 destructor" << endl;
}


class Son : public Base , public Base2
{
public:
    int a;
    int d;
    Son();
    ~Son();
};

Son::Son()
{
    a = 2000;
    d = 1000;
    cout << "Calling a Son constructor" << endl;
}

Son::~Son()
{
    cout << "Calling a Son destructor" << endl;
}

void test01()
{
    Son s;
    cout << "sizeof(Son) = " << sizeof(s) << endl;
    // 父类中非静态成员属性都会被继承
    // 私有成员属性是被编译器隐藏，访问不到，但确实继承了
    cout << "a = " << s.a << endl;
    cout << "Base::a = " << s.Base::a << endl;
    cout << "Base2::a = " << s.Base2::a << endl;
}

int main(int argc, char const *argv[])
{
    test01();
    return 0;
}
```

## 菱形继承
**概念：** 两个派生类继承一个基类，又有一个类同时继承这两个派生类
- 二义性，继承了两份基类数据，只需要一份即可
- 利用 **虚继承** 可以解决菱形继承的问题
- `class 类名 : virtual 继承方式 基类`
- `vbptr` virtual base pointer

```cpp
#include <iostream>
using namespace std;

class Animal
{
public:
    int age;
};

class Sheep : virtual public Animal
{
};

class Camel : virtual public Animal
{
};

class Alpaca : public Sheep, public Camel
{
};


void test01()
{
    Alpaca a;
    a.age = 18;
    cout << "age = " << a.age << endl;
    cout << "sizeof(Alpaca) = " << sizeof(Alpaca) << endl;
}

int main(int argc, char const *argv[])
{
    test01();
    return 0;
}
```

# 多态
## 多态的基本概念
多态分两类：
- **静态多态：** **函数重载** 和 **运算符重载** 都属于静态多态
- **动态多态：** 由 **派生类** 和 **虚函数** 实现运行时多态

静态多态和动态多态的 **区别：**
- 静态多态的 函数地址 是 **早绑定**，编译阶段确定函数地址
- 动态多态的 函数地址 是 **晚绑定**，运行阶段确定函数地址

动态多态的满足条件：
- 有继承关系
- 子类要 **重写** 父类的虚函数，返回值类型、函数名、参数列表完全相同

动态多态的使用：
- 父类的 指针或引用 指向子类对象 `e.g. Animal & animal = cat`

```cpp
#include <iostream>
using namespace std;

class Animal
{
public:
    // 地址早绑定 在编译阶段确定函数地址
    // 如果想执行猫说话,要晚绑定
    virtual void speak();
};

void Animal::speak()
{
    cout << "Animal is speaking" << endl;
}

class Cat : public Animal
{
public:
    void speak();
};

void Cat::speak()
{
    cout << "Cat is speaking" << endl;
}


void doSpeak(Animal & animal)
{
    animal.speak();
}

void test01()
{
    Cat cat;
    doSpeak(cat);// Animal & animal = cat;
}
void test02()
{
    cout << "sizeof(Animal) = " << sizeof(Animal) << endl;
}


int main(int argc, char const *argv[])
{
    // test01();
    test02();
    return 0;
}
```
## 多态的底层原理

## 多态案例1：计算器类
多态的优点：
- 代码组织结构清晰
- 可读性强
- 利于前期和后期的 **扩展** 以及 **维护**
- **C++开发提倡利用多态设计程序架构**

```cpp
#include <iostream>
#include <string>
using namespace std;

// 普通写法
class Calculator
{
public:
    int iNum1;
    int iNum2;
    int getResult(string oper);
};
// 
int Calculator::getResult(string oper)
{
    if (oper == "+")
    {
        return iNum1 + iNum2;
    }
    else if (oper == "-")
    {
        return iNum1 - iNum2;
    }
    else if (oper == "*")
    {
        return iNum1 * iNum2;
    }
    // 如果想扩展新的功能，需要修改源码
    // 在真实开发中， 提倡 开闭原则
    // 开闭原则：对扩展进行开放，对修改进行关闭
    else
    {
        return 0;
    }
}

// 利用多态实现计算器
// 计算器抽象类
class AbstractCalculator
{
public:
    int iNum1;
    int iNum2;
    virtual int getResult()
    {
        return 0;
    }
};

// 加法计算器
class AddCalculator : public AbstractCalculator
{
public:
    int getResult()
    {
        return iNum1 + iNum2;
    }
};

// 减法计算器
class SubCalculator : public AbstractCalculator
{
public:
    int getResult()
    {
        return iNum1 - iNum2;
    }
};

// 乘法计算器
class MulCalculator : public AbstractCalculator
{
public:
    int getResult()
    {
        return iNum1 * iNum2;
    }
};

void test01()
{
    Calculator c;
    c.iNum1 = 10;
    c.iNum2 = 10;
    cout << c.iNum1 << " + " << c.iNum2 << " = " << c.getResult("+") << endl;
    cout << c.iNum1 << " - " << c.iNum2 << " = " << c.getResult("-") << endl;
    cout << c.iNum1 << " * " << c.iNum2 << " = " << c.getResult("*") << endl;
}

void test02()
{
    // 多态使用条件，父类指针或者引用指向子类对象
    AbstractCalculator * abc = new AddCalculator;
    abc->iNum1 = 10;
    abc->iNum2 = 10;
    cout << abc->iNum1 << " + " << abc->iNum2 << " = " << abc->getResult() << endl;
    // 销毁
    delete abc;

    AddCalculator add;
    add.iNum1 = 20;
    add.iNum2 = 40;
    AbstractCalculator & temp = add;
    cout << temp.iNum1 << " + " << temp.iNum2 << " = " << temp.getResult() << endl;

    // 减法运算
    abc = new SubCalculator;
    abc->iNum1 = 10;
    abc->iNum2 = 10;
    cout << abc->iNum1 << " - " << abc->iNum2 << " = " << abc->getResult() << endl;
    // 销毁
    delete abc;
}

int main(int argc, char const *argv[])
{
    // test01();
    test02();
    return 0;
}
```

## 纯虚函数和抽象类
- 在多态中，父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容，因此可以将 **虚函数** 改为 **纯虚函数**
- 语法： `virtual 返回值类型 函数名() = 0;`
- 类中有纯虚函数，称为 **抽象类**
- 抽象类特点：
    - 无法实例化对象
    - 子类必须 **重写** 抽象类中的纯虚函数，否则也属于抽象类

```cpp
#include <iostream>
using namespace std;

class AbastractDrinks
{
public:
    virtual void Boil() = 0;
    virtual void Brew() = 0;
    virtual void PourInCup() = 0;
    virtual void AddSth() = 0;
    void makeDrink()
    {
        Boil();
        Brew();
        PourInCup();
        AddSth();
    }
};

class Coffee : public AbastractDrinks
{
public:
    virtual void Boil()
    {
        cout << "煮农夫山泉" << endl;
    }
    virtual void Brew()
    {
        cout << "冲泡咖啡" << endl;
    }
    virtual void PourInCup()
    {
        cout << "倒入杯中" << endl;
    }
    virtual void AddSth()
    {
        cout << "加入糖和牛奶" << endl;
    }
};

class Tea : public AbastractDrinks
{
public:
    virtual void Boil()
    {
        cout << "煮矿泉水" << endl;
    }
    virtual void Brew()
    {
        cout << "冲泡茶叶" << endl;
    }
    virtual void PourInCup()
    {
        cout << "倒入杯中" << endl;
    }
    virtual void AddSth()
    {
        cout << "加入枸杞" << endl;
    }
};

void doWork(AbastractDrinks * abs)
{
    abs->makeDrink();
    delete abs;// 释放
}

void test01()
{
    // 制作咖啡
    doWork(new Coffee);
    doWork(new Tea);
}

int main()
{
    test01();
    return 0;
}
```

## 虚析构和纯虚析构
**问题：** 多态使用时，如果子类中有属性开辟到堆区，父类指针在释放时无法调用子类的析构代码
**解决方法：** 将父类中的析构函数 改为 **虚析构** 或者 **纯虚析构**

虚析构和纯虚析构共性：
- 可以解决父类指针释放子类对象
- 需要有具体的函数实现

**注：**
- 纯虚析构需要 **声明** 也需要 **实现**
- 如果是纯虚析构，该类属于抽象类，无法实例化对象
- 虚析构： `virtual ~类名()`
- 纯虚析构： `virtual ~类名() = 0;`
- 如果子类中没有堆区数据，可以不写为虚析构构或纯虚析构

```cpp
#include <iostream>
#include <string>
using namespace std;

class Animal
{
public:
    // 纯虚函数
    virtual void speak() = 0;
    Animal()
    {
        cout << "Calling an Animal constractor" << endl;
    }
    // 虚析构
    // virtual ~Animal()
    // {
    //     cout << "Calling an Animal virtual destractor" << endl;
    // }

    // 纯虚析构 声明
    virtual ~Animal() = 0;
};

void Animal::speak()
{
    cout << "Animal is speaking" << endl;
}

// 纯虚析构 实现
Animal::~Animal()
{
    cout << "Calling an Animal pure virtual destractor" << endl;
}

class Cat : public Animal
{
public:
    string * name;
    Cat(string n)
    {
        cout << "Calling a Cat constractor" << endl;
        name = new string(n);
    }
    ~Cat()
    {
        if (name != NULL)
        {
            cout << "Calling a Cat destractor" << endl;
            delete name;
            name = NULL;
        }
    }
    void speak();
};

void Cat::speak()
{
    cout << *name << " Cat is speaking" << endl;
}


void test01()
{
    Animal * animal = new Cat("Tom");
    animal->speak();
    // 父类指针在析构时候，不会调用子类中析构函数，导致如果子类有堆区属性，出现内存泄漏
    // 利用 虚析构 解决父类指针释放子类对象时不干净的问题
    delete animal;
}


int main(int argc, char const *argv[])
{
    test01();
    return 0;
}
```