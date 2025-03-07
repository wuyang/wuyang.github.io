---
layout: post
title:  "Same name initialization in C++"
date:   2025-03-06 20:00:34 -0500
categories: C++
---
Can we initialize member variables using the same name constructor arguments in C++. For example:
{% highlight c++ %}
struct Node {
    int data;
    Node* next;
    Node(int data): data(data), next(nullptr) {}
    Node(int data, const Node* next): data(data), next(next) {}
};
{% endhighlight %}

Yes. It works well and makes the code easier to understand. And you will find that it is clearly allowed in [C++ standard 12.6.2][c++-standard] or [cppreference][cppreference]:

> Names in the expression-list or braced-init-list of a mem-initializer are evaluated in the scope of the constructor for which the mem-initializer is specified. [Example:
{% highlight c++ %}
class X {
  int a;
  int b;
  int i;
  int j;
  public: const int & r;
  X(int i): r(a), b(i), i(i), j(this -> i) {}
};

{% endhighlight %}
>initializes X::r to refer to X::a, initializes X::b with the value of the constructor parameter i, initializes X::i with the value of the constructor parameter i, and initializes X::j with the value of X::i; this takes place each time an object of class X is created. —end example] [Note: Because the mem-initializer are evaluated in the scope of the constructor, the this pointer can be used in the expression-list of a meminitializer to refer to the object being initialized. —end note ]

[c++-standard]: https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3797.pdf
[cppreference]: https://en.cppreference.com/w/cpp/language/constructor
