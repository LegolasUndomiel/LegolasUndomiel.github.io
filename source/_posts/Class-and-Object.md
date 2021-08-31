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