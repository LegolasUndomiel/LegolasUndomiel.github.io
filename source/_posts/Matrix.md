---
title: Matrix
date: 2021-09-12 14:22:14
tags:
---
# Matrix类的实现
使用C++编写一个类，实现以下功能：
- 获得矩阵的行数、列数
- 设置矩阵中指定位置的元素值
- 获得矩阵中指定位置的元素值
- 重载运算符 `+ - * /` 实现矩阵对象的运算，其中 `*` 包括矩阵乘法和矩阵数乘两个功能
- 矩阵求逆运算
- 矩阵转置
- 求行列式

**目的：**
- 练习C++语法
- 熟悉指针、类与对象、深拷贝、动态内存与释放等等概念

# 代码示例
## 头文件
```cpp
#ifndef MATRIX_H
#define MATRIX_H
#include <cassert>
#include <iostream>
#include <string>
using namespace std;

class Matrix
{
private:
    int row, column;
    double** elements;
public:
    Matrix();// 默认构造函数
    Matrix(int row, int column);// 构造函数重载
    Matrix(int row, int column, double* matrix);// 构造函数重载
    Matrix(const Matrix& matrix);// 深拷贝构造函数
    int getRow() const;
    int getColumn() const;
    double getElement(int m, int n) const;
    void setElement(int m, int n, double value);
    Matrix operator+(const Matrix& matrix);
    Matrix operator-(const Matrix& matrix);
    Matrix operator*(double multiple);
    Matrix operator*(const Matrix& matrix);
    friend Matrix operator*(double multiple, const Matrix& matrix);
    Matrix operator/(const Matrix& matrix);// 未完成
    Matrix& operator=(const Matrix& matrix);// 赋值运算符重载
    Matrix operator-() const;// 一元负号运算符
    friend ostream& operator<<(ostream& output, const Matrix& matrix);
    Matrix Transpose();
    double Determinant();// 未完成
    Matrix Inverse();// 未完成
    ~Matrix();
};
#endif
```
## 源文件
```cpp
#include "Matrix.h"

Matrix::Matrix():Matrix::Matrix(1, 1){};// 委托构造

Matrix::Matrix(int row, int column)
{// 初始化行数、列数
    assert(row > 0 && column > 0);
    this->row = row;
    this->column = column;
    this->elements = new double*[this->row];
    for (int i = 0; i < this->row; i++)
    {
        this->elements[i] = new double[this->column];
    }
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < this->column; j++)
        {
            this->elements[i][j] = 0;
        }
    }
}

Matrix::Matrix(int row, int column, double* matrix)
{// 初始化行数、列数和元素
    assert(row > 0 && column > 0);
    this->row = row;
    this->column = column;
    this->elements = new double*[this->row];
    for (int i = 0; i < this->row; i++)
    {
        this->elements[i] = new double[this->column];
    }
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < this->column; j++)
        {
            this->elements[i][j] = matrix[i * this->column + j];
        }
    }
}

Matrix::Matrix(const Matrix& matrix)
{
    this->row = matrix.getRow();
    this->column = matrix.getColumn();
    this->elements = new double*[this->row];
    for (int i = 0; i < this->row; i++)
    {
        this->elements[i] = new double[this->column];
    }
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < this->column; j++)
        {
            this->elements[i][j] = matrix.getElement(i, j);
        }
    }
}

int Matrix::getRow() const
{
    return this->row;
}

int Matrix::getColumn() const
{
    return this->column;
}

void Matrix::setElement(int m, int n, double value)
{
    assert(m >= 0 && m < this->row && n >= 0 && n < this->column);
    this->elements[m][n] = value;
}

double Matrix::getElement(int m, int n) const
{
    assert(m >= 0 && m < this->row && n >= 0 && n < this->column);
    return this->elements[m][n];
}

Matrix Matrix::operator+(const Matrix& matrix)
{
    assert(this->row == matrix.row && this->column == matrix.column);
    Matrix result(this->row, this->column);
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < this->column; j++)
        {
            double elemValue = this->getElement(i, j) + matrix.getElement(i, j);
            result.setElement(i, j, elemValue);
        }
    }
    return result;
}

Matrix Matrix::operator-(const Matrix& matrix)
{
    return (*this + (-1 * matrix));
}

Matrix Matrix::operator*(const Matrix& matrix)
{
    assert(this->column == matrix.getRow());
    Matrix result(this->row, matrix.getColumn());
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < matrix.getColumn(); j++)
        {
            double elemValue = 0;
            for (int k = 0; k < this->column; k++)
            {
                elemValue += this->getElement(i, k) * matrix.getElement(k, j);
            }
            result.setElement(i, j, elemValue);
        }
    }
    return result;
}

Matrix Matrix::operator*(double multiple)// 成员函数，矩阵 * 数
{
    Matrix result(this->row, this->column);
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < this->column; j++)
        {
            double elemValue = multiple * this->getElement(i, j);
            result.setElement(i, j, elemValue);
        }
    }
    return result;
}

Matrix operator*(double multiple, const Matrix& matrix)// 全局函数，数 * 矩阵
{
    Matrix result(matrix.getRow(), matrix.getColumn());
    for (int i = 0; i < matrix.getRow(); i++)
    {
        for (int j = 0; j < matrix.getColumn(); j++)
        {
            double elemValue = multiple * matrix.getElement(i, j);
            result.setElement(i, j, elemValue);
        }
    }
    return result;
}

ostream& operator<<(ostream& output, const Matrix& matrix)
{
    for (int i = 0; i < matrix.getRow(); i++)
    {
        for (int j = 0; j < matrix.getColumn(); j++)
        {
            output << matrix.getElement(i, j) << '\t';
        }
        cout << endl;
    }
    return output;
}

Matrix& Matrix::operator=(const Matrix& matrix)
{// 类的成员 涉及到在 栈区 开辟数据时，赋值运算符要进行 深拷贝
    // 先释放内存，防止内存泄漏
    for (int i = 0; i < this->row; i++)
    {
        if (this->elements[i] != NULL)
        {
            delete[] this->elements[i];
            this->elements[i] = NULL;
        }
    }
    delete[] this->elements;
    this->elements = NULL;
    this->row = matrix.getRow();
    this->column = matrix.getColumn();
    // 重新申请内存进行复制
    this->elements = new double*[this->row];
    for (int i = 0; i < this->row; i++)
    {
        this->elements[i] = new double[this->column];
    }
    for (int i = 0; i < this->row; i++)
    {
        for (int j = 0; j < this->column; j++)
        {
            this->elements[i][j] = matrix.getElement(i, j);
        }
    }
    return *this;
}

Matrix Matrix::operator-() const
{
    return (-1 * (*this));
}

Matrix Matrix::Transpose()
{
    assert(this->getRow() > 0 && this->getColumn() > 0);
    Matrix matrix(this->getColumn(), this->getRow());
    for (int i = 0; i < matrix.getRow(); i++)
    {
        for (int j = 0; j < matrix.getColumn(); j++)
        {
            matrix.setElement(i, j, this->getElement(j, i));
        }
    }
    return matrix;
}

Matrix::~Matrix()
{
    for (int i = 0; i < this->row; i++)
    {
        if (this->elements[i] != NULL)
        {
            delete[] this->elements[i];
            this->elements[i] = NULL;
        }
    }
    delete[] this->elements;
    this->elements = NULL;
}


void test01()
{
    double a[12] = {1,0,0,1,0,1,0,1,1,1,1,0};
    double b[16] = {1,2,3,4,1,1,1,1,1,0,0,0,0,1,1,1};
    double c[12] = {1,1,1,1,0,0,0,1,0,0,1,1};

    // 构造函数测试
    Matrix A(3,4,a);
    Matrix B(4,4,b);
    Matrix C(3,4,c);
    cout << "A = " << endl << A << endl;
    cout << "B = " << endl << B << endl;
    cout << "C = " << endl << C << endl;

    Matrix D = A + C;// +
    Matrix E = A - C;// -
    Matrix F = A * B;// 矩阵 * 矩阵
    Matrix G = B * 2;// 矩阵 * 数
    Matrix H = 2 * A;// 数 * 矩阵
    cout << "A + C = " << endl << D << endl;
    cout << "A - C = " << endl << E << endl;
    cout << "A * B = " << endl << F << endl;
    cout << "B * 2 = " << endl << G << endl;
    cout << "2 * A = " << endl << H << endl;

    Matrix I,J;
    Matrix K(C);// 深拷贝测试
    I = J = A;// 赋值运算符测试
    J = -I;// 负号运算符测试
    cout << "I = A = " << endl << I << endl;
    cout << "J = -I = " << endl << J << endl;
    cout << "K = C = " << endl << K << endl;

    Matrix L = A.Transpose();
    cout << "L = A.Transpose() = " << endl << L << endl;
}

int main()
{
    test01();
    system("pause");
    return 0;
}
```
# Comments
- **常引用** 只能调用 **类的常成员函数**