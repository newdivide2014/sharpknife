---
title: "c++ 智能指针"
date: 2023-03-22T09:39:58+08:00
description: Smart Pointer
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["c++", "Smart Pointer"]
categories: ["c++"]
---

C++中智能指针，有`shared_ptr`，`unique_ptr`，`weak_ptr`

## shared_ptr

`shared_ptr`是多个指针指向一块内存。 
被管理对象有一个引用计数，这个计数记录在每个指针上，有几个shared_ptr指向它，这个引用计数就是几，当没有任何shared_ptr指向它时，引用计数为0，这时，自动释放对象。

```c++
#include <iostream>
#include <memory>
using namespace std;

class A{
public:
    A();
    explicit A(int a);
    ~A();
};

A::A() {
    cout << "A()" << endl;
}

A::A(int a) {
    cout << "A(int a)" << endl;
}

A::~A() {
    cout << "~A" << endl;
}

int main() {
    auto p = new A;
    shared_ptr<A> sp(p);
    cout << sp.use_count() << endl; // 1
    {
        shared_ptr<A> sp1(sp);
        cout << sp.use_count() << endl; // 2
    }
    cout << sp.use_count() << endl; // 1
    return 0;
}
```
**注：同一个对象只能用同一套内存管理体系，如果它已经有智能指针了，那么再创建智能指针时，需要通过原来已有的智能指针创建，而不能重复用原始空间来创建。**

```c++
int main() {
    auto p = new A; 
    shared_ptr<A> sp1(p1); 
    shared_ptr<A> sp2(p1); 
    return 0;
}
```
这段程序会`double free detected` 
这里用了两个智能指针管理同一块内存，因为`sp1` 和`sp2`不知道彼此的存在，所以也会重复释放。

## unique_ptr

一个`unique_ptr`“拥有”它所指向的对象，与`shared_ptr`不同，某个时刻只能有一个`unique_ptr`指向一个给定对象。当`unique_ptr`被销毁时，它所指向的对象也被销毁。

`unique_ptr`没有类似`shared_ptr`中`make_shared`的标准库函数返回一个`unique_ptr`，定义一个`unique_ptr`时，需要将它绑定到一个`new`返回的指针上，并且不能直接将`new`的结果用赋值运算符“=”赋值给`unique_ptr`（初始化方式必须采用直接初始化方式）。

因为`unique_ptr`所指向的对象只能有一个`unique_ptr`指针，也就是一个引用计数。因此`unique_ptr`不支持普通的拷贝和赋值操作。 

虽然两个`unique_ptr`不可以同时指向同一个内存对象，但是可以将一个即将销毁的`unique_ptr`指针拷贝或赋值给1另一个`unique_ptr`。 
函数的参数传递和返回值就是很好的例子，在函数内部的`unique_ptr`指针随着作用域的结束会自动销毁，因此可以将其作为返回值，然后将内存传递给另一个`unique_ptr`指针管理。

`unique_ptr`之间不能拷贝与赋值。但是可以使用`release`和`reset`函数来将指针的所有权从一个（非const）`unique_ptr`转移给另一个`unique`。
`unique_ptr`调用`release`函数之后必须将返回值传递给另一个`unqiue_ptr`，否则就会内存泄露。

```c++
unique_ptr<int> p1; //正确
unique_ptr<int> p2(new int(3)); //正确
unique_ptr<int> p3 = new int(3);//错误

unique_ptr<int> p4(new int(5));
unique_str<int> p5(p4.release());

//主动释放unique_ptr
//unique_ptr当离开作用域范围就会自动释放
//但是有时希望可以主动释放unique_ptr指向的内存空间
//直接把nullptr赋值给智能指针就可以了
int main()
{
    std::unique_ptr<int> p(new int(1));
    p = nullptr; //主动释放

    return 0;
}
```

## weak_ptr

虽然`shared_ptr`是用来避免内存泄漏，可以自动释放内存。但`shared_ptr`在使用中可能存在循环引用，使引用计数失效，从而导致内存泄漏的。

`weak_ptr`叫弱引用指针。是一种不控制对象生命周期的智能指针, 它指向一个`shared_ptr`管理的对象。`weak_ptr`设计的目的是为了协助`shared_ptr`而引入的一种智能指针，它可以解决`shared_ptr`循环引用的问题。 
`weak_ptr`只可以从一个`shared_ptr`或另一个`weak_ptr`对象来构造, 它的构造和析构不会引起引用记数的增加或减少。 

`weak_ptr`在使用前需要检查合法性。调用`expired()`函数判断指针所指的内存空间是否被释放掉/指针是否为空/是否还有`shared_ptr`指针指向weak_ptr指向的内存空间。
```c++
#include <iostream>
#include <memory>
using namespace std;

int main()
{
    shared_ptr<int> p = nullptr;
    weak_ptr<int> p1(p);
    cout  << p1.expired() << endl; // 1
    return 0;
}
```

## `explicit`关键字

`explicit`关键字有两个用途：

1. 指定构造函数或转换函数 (C++11起)为显式, 即它不能用于隐式转换和复制初始化。
2. 可以与常量表达式一同使用. 当该常量表达式为 true 才为显式转换(C++20起)。

与它相对应的另一个关键字是`implicit`, 意思是隐藏的，类构造函数默认情况下即声明为`implicit`(隐式)。

`explicit`关键字只对有一个参数的类构造函数有效, 如果类构造函数参数大于或等于两个时, 是不会产生隐式转换的, 所以`explicit`关键字也就无效了。 
但是也有一个例外, 就是当除了第一个参数以外的其他参数都有默认值的时候，`explicit`关键字依然有效, 此时, 当调用构造函数时只传入一个参数, 等效于只有一个参数的类构造函数, 