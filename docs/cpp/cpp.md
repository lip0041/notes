# C++ Memo
## 程序的编译和运行

*   常用的c++编译器是GNU编译器（还有微软的Visual Studio编译器）
*   默认运行GNU命令是`g++`:
    `$ g++ proc.cpp -o proc_name`
    其中`g++`调用GNU编译器，`proc.cpp`是我们写的程序名，`-o proc_name`是编译器参数，表示编译生成的可执行文件文件名--`proc_name`
    若不加-o参数，则win下默认生成`a.exe`文件，unix下生成`a.out`文件
*   运行可执行文件
    win下通过 `.\a`运行`a.exe`--后缀可以省略
    unix下通过`./a.out`运行`a.out`
*   获取程序返回值
    运行后通过`echo`命令获取程序的返回值
    win下键入`$ echo $ERRORLEVEL%`
    unix下键入`$ echo $?`

> 注： 命令中的第一个$是系统提示符，不用输入

## 声明与定义的关系

*   概念上看

1.  声明是使名字被程序所知，告诉程序又一个某种类型的变量/函数，规定了变量的类型和名字，并**不分配存储空间**。
2.  定义是负责创建于名字关联的实体，不仅规定变量的类型和名字，还会给这个变量**申请存储空间，也可能会默认赋初值**。

*   **变量能且只能被定义一次，但可以被多次声明**

*   声明一个变量而非定义，则需要在变量名前加关键字`extern`，且不要显示初始化，一旦初始化就抵消了`extern`的作用，变成了定义

    //声明了整型变量i,不是定义
    extern int i; 
    //声明并且定义了整型变量j,分配了存储空间，并一般默认赋初值
    int j;
    //显示初始化抵消了extern的作用，此为定义
    extern double pi = 3.1416; 

## 引用和指针及const

*   **引用(refers to)**，即别名。程序将引用和它的初始值绑定在一起，而不是将初始值拷贝给引用。引用不是对象，必须初始化。
*   **指针(point to)**，本身是一个对象，允许对指针赋值和拷贝，无需在定义时赋初值

> c++的空指针字面值为`nullptr`，它可以转换成任意其他的指针类型

*   `const`限定符，默认情况下，const对象仅在文件内有效，若想在多个文件中共享const对象，则需要在定义前加`extern`关键字

*   对`const`对引用：`const type &`，又称"常量引用"。

    const int ci = 1024;const int &r1 = ci; 
    // 正确，此时r1即为const常量ci的引用，不可通过r1改变ci的值int &r = ci; // 出错，不能将普通的引用&绑定到const常量上

*   const型指针`type *const`：**顶层const**表示指针/对象本身是个常量，**底层const**表示指针所指的对象是个常量--**用于声明引用的const都是底层const**

> 底层const的限制：执行对象的拷贝操作时，拷入和拷出的对象必须具有相同的底层const资格--指向的是个常量，或者两个对象的数据类型必须可以转换(如，非常量可以转换成常量，反之不行）

*   一个指针可以同时是顶层const和底层const，如

    const int *const p1 = p;
    // 靠右的const是顶层const--自身是常量，靠左的是底层constcont int &r = i; // r是底层const

*   c++11可以通过将变量声明为`constexpr`类型，使编译器自己验证变量是否为一个常量表达式（字面值也是常量表达式），当然，声明时必须用常量表达式初始化。限定符`constexpr`仅对指针/对象有效，对指针指向的对象无关，即是**顶层const**

## 类型别名(type alias)

*   传统方法：使用关键字`typedef`

    typedef double wages; // wages是double的同义词(synonym)

*   C++新标准：使用关键字`using`

    using SI = Sales_item; // SI是Sales_item的同义词

`auto`：编译器分析表达式所属的类型，auto定义的变量必须有初始值，一般忽略顶层const

`decltype`：选择并返回操作数的数据类型，只分析得到类型，而不计算表达式的值

    decltype(f()) sum = x; // sum类型为函数f的返回类型，并不调用f

> decltype((variable))的结果永远是引用，而decltype(variable)结果只有当variable本身是引用时才是引用

