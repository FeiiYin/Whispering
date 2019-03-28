## C++ 其实我并不会 C++ 

+ 继承

不写继承方式，默认是private继承 class A : B

构造由父向子，析构由子向父

多继承，调用两个父亲的同名函数
```
    C c
    c.A::fun();
    c.B::fun();
```

+ virtual

father = & child; 时，可以调用孩子重写的方法

+ const 

```
    int const *A; 　//A可变，*A不可变
    int *const A; 　//A不可变，*A可变
```

const 是一个左结合的类型修饰符

```
    int Fun() const;
```

const 后置，在此函数的声明中和定义中均要使用const，不能修改类的数据成员，**不能在函数中调用其他不是const的函数**

+ define 和 inline 的区别

define 只进行简单的字符替换，无类型检测

inline 内联函数对编译器提出建议，是否进行宏替换，编译器有权拒绝
