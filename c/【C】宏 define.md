作用

替换

  

生效时间

编译中的预处理阶段

  

作用

1. 替换大量相似或重复代码，减少代码量，易读性

  

## 常用操作

  

1. 无参数，替换字符串、数字、数组大小

```c

#define PI 3.14159265

```

  

2. 无参数，无宏值

```C

#define SYSTEM_API

```

  

3. 预定义宏

编译器在编译时，已经提前定义

  

```c

#define NULL ((void*)0)

```

  

4. 带参数

```c

#define MUL(x, y) x * y

  

#define MUL(x, y) ((x) * (y))  // 推荐

```

- 宏是简单的符号替换，不会检查参数类型，而函数会严格检查输入的参数类型

- 因为宏是在编译期进行的符号替换，所以在运行时，不会带来额外的时间和空间开销，而函数会在运行时执行压栈出栈的操作，存在函数调用的开销

- 宏是不可以调试的，而函数可以进行单步调试

- 宏不支持递归，函数支持递归

  

推荐且要求：每个参数添加括号，除了只要单个参数外，其他最外层也加括号

```c

#define XXX 12

#define YYY (1 << 2)

#define ZZZ(x, y) ((x) << (y))

```

  

5. # 和 ##

```c

#define STRING(x) #x

const char * str = STRING(test);  // str = "test"

  

#define VAR(index) INT##index

int VAR(1);   // 等价 int INT1;

```

  

6. 可变参数

常用在类似printf封装

```c

#define ERROR(fmt, ...) printf(fmt, ##__VA_ARGS__)

```

为什么要在`__VA_ARGS__`之前添加`##`符号，主要是因为，如果不添加的话，当只有fmt参数，`__VA_ARGS__`为空时，之前的逗号不会删除

  

```text

trace("got a number");   ==>  trace("got a number",);

```

  

从而导致编译错误，而加上`##`符号的话，将使预处理器去除掉它前面的那个逗号。

  

7. 多行宏

每行末尾添加反斜杠\

```c

#define ADD(x, y) do { int sum = (x) + (y); return sum; } while (0)

// 宏的内容比较长，也没有缩进，易读性较差，因此转为多行

#define ADD(x, y) \

do {\

    int sum = (x) + (y);\

    return sum;\

} while (0)

```

  

8. 取消宏定义

减少作用域

```c

#undef XXX

```

  

9. 编译器预定义宏

    1. FILE   const char*  当前编译文件的绝对路径

    2. LINE  int   当前所在行

    3. FUNCTION const char* 当前所在函数名

    4. DATE const char* 当前所在日期

    5. TIME const char* 当前所在时间

  

10. 宏调试

如何在编译时打印宏信息

  

```c

#define SOMEMACRO 123456

#define MACROTOSTR2(x) #x

#define PRINTMACRO(x) #x " = " MACROTOSTR2(x)

#pragma message(PRINTMACRO(SOMEMACRO))  // 编译时会打印输出"SOMEMACRO = 123456"

  
  

#define SOMEMACRO 123456

#define MACROPARAM(x) new int(x);

#define MACROTOSTR2(x) #x

#define PRINTMACRO(x) #x " = " MACROTOSTR2(x)

#pragma message(PRINTMACRO(MACROPARAM(SOMEMACRO)))  // 编译时会打印输出"MACROPARAM(SOMEMACRO) = new int(123456);"

```

  

11. 跨平台开发

预处理指令`_WIN32`

```C

#ifdef _WIN32 // Windows默认会定义该宏

    OutputDebugString("this is a Windows log");

#else

    NSLog(@"this is a mac log");

#endif

```

  

```C

#if defined(_WIN32) || defined(WIN32)   // Windows

    OutputDebugString("this is a Windows log");

#endif

```

  

12. if、ifdef、defined、#ifndef

```C

#if defined(_WIN32) || defined(WIN32)

    OutputDebugString("this is a Windows log");

#endif

  

#if SUPPORT_ADD 1     // if后面宏必须为整数

    Add();

#endif

  

#ifdef XXX           // 只要XXX定义即可

    Add();

#endif

  

#if defined(XXX) && defined(YYY)           // defined(XXX)是否定义过，等价#ifdef XXX

    Add();

#endif

  

#ifndef XXX    // 如果没有定义XXX

    Add();

#endif

  

#if !defined(XXX)   // 等价#ifndef XXX

    Add();

#endif

```

  

12. 防止重复包含文件

```C

#ifndef SYSTEM_API_H

#define SYSTEM_API_H

  

// 头文件的内容

...

  

#endif

```

  

13. 打印错误信息

包含文件名和函数名或行号

```C

printf("%s %d printf message %s\n", __FILE__, __LINE__, "some reason");

  

// 替换成

#define trace(fmt, ...) printf("%s %d "fmt, __FILE__, __LINE__, ##__VA_ARGS__)

// 这样在使用时可以这么写,同样可以输出当前行号和文件名

trace("printf message %s\n", "some reason");

```

  

14. 减少重复代码

如类中含有多个属性，每个属性都有get、set方法，将其提取出来用宏替换

  
  

## 技巧

  

1. 防止优先级变化，对每个参数使用()，且最外层也添加()

2. 宏命名冲突，使用全大写

3. 推荐使用do{ }while(0)，成为一个独立的语法单元，从而不会与上下文发生混淆，且绝大多数的编译器都能够识别do{…}while(0)这种无用的循环并进行优化，所以使用这种方法也不会导致程序的性能降低

4. 宏替换在编译前进行，不分配内存，变量定义分配内存，函数调用在编译后程序运行时进行，并且分配内存

5. 宏展开不占用运行时间，只占用编译时间，函数调用占运行时间（分配内存、保留现场、值传递、返回值）

6. 宏定义占用目标代码空间

## 条件编译

```C
#if

#ifdef

#ifndef

#endif

#else

#elif
```

宏如何与与或非连用

