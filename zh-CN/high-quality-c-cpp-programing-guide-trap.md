﻿# 《高质量C++/C编程指南》陷阱

Created @ 2011-04-14, recovered rev 2013-04-12, markdown @ 2015-09-14.

本文使用 CC-BY 3.0 发布。

此文硬伤不少，且相对谭XX的书而言隐晦许多，不建议新手学习。
主观的论述，合理的部分，就此略过。原文（点查看）疏漏之处也尽量忍住不吐槽。

## 第1章 文件结构

> 每个C++/C程序通常分为两个文件。

//错误。没有强调翻译单元的概念。

> 另一个文件用于保存程序的实现（implementation），称为定义（definition）文件。

//有误。实现不简单等同于定义。例如，类的完整声明也是类的定义，但不是完整的实现。头文件也可以存放其它定义（例如模板和内联函数的实现）。

### 1.2

> ####建议1-2-1####

> 在C++语法中，类的成员函数可以在声明的同时被定义，并且自动成为内联函数。这虽然会带来书写上的方便，但却造成了风格不一致，弊大于利。建议将成员函数的定义与声明分开，不论该函数体有多么小。

//这条建议一般不适用于类模板。

### 1.4

> 头文件能加强类型安全检查。如果某个接口被实现或被使用时，其方式与头文件中的声明不一致，编译器就会指出错误，这一简单的规则能大大减轻程序员调试、改错的负担。

//在使用合理的情况下，这基本上是正确的，但头文件可以导致其它方面——像重构（典型情况如重命名一个函数）的复杂化。

## 第2章 程序的版式

这章基本是主观内容。读者需要注意风格是有争议的，其中的“良好风格”或“不良风格”并非公认。

### 2.8

> 很多C++教课书受到Biarne Stroustrup第一本著作的影响，不知不觉地采用了“以数据为中心”的书写方式，并不见得有多少道理。

> 我建议读者采用“以行为为中心”的书写方式，即首先考虑类应该提供什么样的函数。这是很多人的经验——“这样做不仅让自己在设计类时思路清晰，而且方便别人阅读。因为用户最关心的是接口，谁愿意先看到一堆私有数据成员！”

//“Biarne Stroustrup”拼写错误。C++之父的名字是 Bjarne Stroustrup 。有些一厢情愿了： C++ 的类定义中既然允许显式地表示 `private` 成员，就不是纯粹的接口描述方式。以我个人的经验，数据成员写在后面可能会导致顺序阅读代码时需要回溯。当类定义长度较小时这点影响不大，但定义长度比较长的时候（例如 `Loki::Functor` 里的代码）就会需要较频繁地滚屏，影响代码阅读效率。

## 第3章 命名规则

这章也基本是主观内容。

### 3.1

> ####规则3-1-1####

> 标识符应当直观且可以拼读，可望文知意，不必进行“解码”。

//这点和此文建议使用的匈牙利命名法有一定程度的矛盾。

> ####规则3-1-3####

> 命名规则尽量与所采用的操作系统或开发工具的风格保持一致。

//尽管大部分人应该乐于支持这个观点，不过事实上有时候无法实现。例如同时使用标准库和Windows API 风格的代码。这时倒不妨直接约定允许根据上下文选择要使用的命名风格。要点是，应该让人看出某个名称是用哪个风格命名的，而不至于一眼就混淆来源。

### 3.2

> ####规则3-2-7####

> 为了防止某一软件库中的一些标识符和其它软件库中的冲突，可以为各种标识符加上能反映软件性质的前缀。例如三维图形标准OpenGL的所有库函数均以gl开头，所有常量（或宏定义）均以GL开头。

//在 C++ 中应该考虑是否可以用命名空间代替前缀。

## 第4章 表达式和基本语句

> 我真的发觉很多程序员用隐含错误的方式写表达式和基本语句，我自己也犯过类似的错误。

//作者似乎没搞清楚“错误”一词的含义。

### 4.3

> ####规则4-3-4####

> 不要写成

> ```
>        if (p== 0)  // 容易让人误解p是整型变量
>        if (p!= 0)
> ```        

//事实上，C++ 中的 `NULL` 典型地就是 `int` 字面量 `0` （考虑到成文时间，不提新标准的空指针类型），和 `int` 兼容。以 Bjarne Stroustrup 的观点，这样恰恰会使人误以为 `NULL` 不是整数，因此推荐用 `0` 而不是 `NULL` 。

### 4.3.5

> 或者改写成更加简练的return (condition ? x : y);

//这里的括号是多余的。

### 4.4

这节不是语言本身而是涉及语言实现的内容。以现在的观点来看，优化器会可能会在此做一些工作。当然了解一些相关原理大体上还是有益的。

## 第5章 常量

> 常量是一种标识符，它的值在运行期间恒定不变。C语言用 #define来定义常量（称为宏常量）。C++ 语言除了 #define外还可以用const来定义常量（称为const常量）。

//谭XX风格的信口开河。这段引文中逗号或者句号之间的内容，没一个能算得上是正确的。

### 5.2

> ####规则5-2-1####

> 在C++程序中只使用 const常量而不使用宏常量，即const常量完全取代宏常量。

//这是有问题的。事实上很多情况下 const 只能让编译器被修饰的对象当做只读变量，而非编译期的真正意义的常量进行处理。与 #define 的符号常量（字面量）相比，只读变量受到了一些限制，例如不能作 case 的标号。

## 第6章 函数设计

> C语言中，函数的参数和返回值的传递方式有两种：值传递（pass by value）和指针传递（pass by pointer）。

//错误。形式上， C 语言函数参数只按值传递。所谓的指针传递是按值传递的一种，只是传递参数的类型是指针而已。

### 6.1

> ####规则6-1-1####

> 参数的书写要完整，不要贪图省事只写参数的类型而省略参数名字。如果函数没有参数，则用void填充。

//不妥当。有时候参数的名称并非有意义，像 int max(int, int); 之类的原型，写了也不会让函数的意义更清楚。此外，并没有指出C函数没有参数时参数列表为 void ，这和省略参数列表（接受任意参数）是不同的。而 C++ 中省略参数列表和 void 参数相同，参数列表 ... 接受不确定个数的参数。

### 6.2

> ####规则6-2-3####

> 不要将正常值和错误标志混在一起返回。正常值用输出参数获得，而错误标志用return语句返回。

//在C++中可以不使用此规则而使用异常（在 C 中理论上也可以类似地使用 setjmp/longjmp ，但容易造成语义不明确，实际上基本不用）。

### 6.3

> ####规则6-3-1####

> 在函数体的“入口处”，对参数的有效性进行检查。

//在函数接口语义明确的情况下并非是必需的。例如 C 标准库 <string.h> 中以及 POSIX 标准中的许多函数。

> ####规则6-3-2####

> 在函数体的“出口处”，对return语句的正确性和效率进行检查。

//同样不是必需的。此外检查可能损失效率。

>要搞清楚返回的究竟是“值”、“指针”还是“引用”。

//注意返回对象的语义，但是刻意区分“值”和“指针”是不必要的，严格上是错误的——它们根本就不是可以比较的一类概念。

> ####建议6-4-2####

> 函数体的规模要小，尽量控制在50行代码之内。

//尽管为数不多，有些特殊情况，如编译器的某些分析程序，是明显的反例。

## 第7章 内存管理

> “640Kought to be enough for everybody

> —Bill Gates 1981”

//和本章主题无关。

### 7.1

> 内存分配方式有三种

//有误。内存分配具体方式由实现决定，语言只限制存储类。

### 7.2

漏了重复释放内存的错误（这通常会引起程序崩溃）。

> ####规则7-2-1####

> 用malloc或new申请内存之后，应该立即检查指针值是否为NULL。防止使用指针值为NULL的内存。

//对 C++ 而言是错误的。 ISO C++ 关于内存分配失败的默认行为是抛出 std::bad_alloc 异常。如果要使分配失败不抛出异常，使用 nothrow 版本，或者设置实现相关的编译选项。

> ####规则7-2-5####

> 用free或delete释放了内存之后，立即将指针设置为NULL，防止产生“野指针”。

//不一定必要。例如指针是自动变量，在退出所在的块作用域被自动释放时。

### 7.3.1

> 该语句企图修改常量字符串的内容而导致运行错误

//有误。 C 语言中字符串字面量（具有数组类型）未必是常量。当然还是应该避免修改字符串字面量，这是未定义行为。

### 7.9

> 为new和malloc设置异常处理函数。例如VisualC++可以用_set_new_hander函数为new设置用户自己定义的异常处理函数，也可以让malloc享用与new相同的异常处理函数。

//应该补充的是，标准库有 std::set_new_handler 。

## 第8章 C++函数的高级特性

> const与virtual机制仅用于类的成员函数。

//应该强调“非静态”成员函数，否则就是错误的。

（虽然似乎没有更多明显的错误，不过遗漏的地方一堆，坚决不吐槽……= =）

## 第9章 类的构造函数、析构函数与赋值函数

### 9.1

> Stroustrup的命名方法既简单又合理：让构造函数、析构函数与类同名，由于析构函数的目的与构造函数的相反，就加前缀‘~’以示区别。

//错误。构造函数和析构函数是无名的（这个细节决定了一些语言特性的限制，例如不能 using 声明基类的构造函数），看起来名称和类名相同的调用方式其实是语法的限制。

> 非内部数据类型的成员对象应当采用第一种方式初始化，以获取更高的效率。

//效率在这里倒是次要的（很容易被编译器优化掉），重要的是语义。另外，初始化列表的一些行为是受到特殊限制的，例如基类子对象和成员的初始化顺序和异常。

### 9.7

（仍然不想吐槽漏掉 swap & copy 这样高效可靠的方法而在 `operator=` 实现里分配内存……）

## 第10章 类的继承与组合

首先标题有点问题。类可以继承，组合的应该是类的实例而非本身。

> 如果将对象比作房子，那么类就是房子的设计图纸。所以面向对象设计的重点是类的设计，而不是对象的设计。

//因果关系不成立。而且观点是有问题的，仅适于经典的 class-based OOD 。

### 10.2

> ####规则10-2-1####

> 若在逻辑上A是B的“一部分”（a partof），则不允许B从A派生，而是要用A和其它东西组合出B。

//错误。尽管一般组合能够胜任这项工作，但并非绝对。可以使用private继承完成相同的任务，并且提供覆盖成员函数的特性。这是组合无法完成的。

## 第11章 其它编程经验

### 11.1.3

> 如果在编写const成员函数时，不慎修改了数据成员，或者调用了其它非const成员函数，编译器将指出错误

//错误：漏了 `mutable` 修饰的成员这个特例。

> ####建议11-3-8####

> 避免编写技巧性很高代码。

//不应该逃避。技巧性高不意味着难以理解；即使难以理解，也可以通过注释弥补。当然，前提是技巧要使用得合理。

> ####建议11-3-13####

> 把编译器的选择项设置为最严格状态。

//有时候现实不允许，例如考虑已有代码的兼容性，需要配置时会带来额外的复杂性。

## 附录C ：C++/C试题的答案与评分标准

> 标准答案示例：
> const float EPSINON = 0.00001;

> if ((x >= - EPSINON) && (x <= EPSINON)

//如果是“标准”的，为什么不用标准库的 `<float.h>`/`<cfloat>` 的 `FLT_EPSILON` 而自己重复发明轮子？

> 三、简答题（25分）

> 1、头文件中的ifndef/define/endif 干什么用？（5分）

> 答：防止该头文件被重复引用。

//错误。条件编译显然不只用于给头文件增加 header guard 。

> 四、有关内存的思考题（每小题5分，共20分）

> 答：程序崩溃。

> 因为GetMemory并不能传递动态内存，

> Test函数中的 str一直都是 NULL。

> strcpy(str, "hello world");将使程序崩溃。

//错误。未定义行为不等同于程序崩溃，尽管很可能是这样。

> 六、编写类String的构造函数、析构函数和赋值函数（25分）

> `String& String::operate =(const String &other)`

//关键字 `operator` 拼写错误。实现冗余就不说了。
