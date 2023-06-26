代码效率包括两个方面内容：代码的大小和代码执行速度。如果代码精简和执行速度快，我们就说这个代码效率高


## 1. 减少逻辑错误但编译正确
1. 定义类型别名时，使用typedef，而禁止macro
``` C
typedef int* INT_PTR;
INT_PTR a, b; // int *a;int *b;

#define int* INT_PTR;
INT_PTR a, b; // int *a;int b;
```

1. 在条件语句中，常数项在左侧
不符合人性，但可将错误暴露出来
使用"="赋值运算符，替代==相等运算符，这是个常见的输入错误
``` C
int x = 4;if （x = 1）{ x = x + 2;printf（"%d",x）；// Output is 3 }

int x = 4;if （1 = x）{ x = x + 2;printf（"%d",x）； // Compilation error }
```

2. 使用无符号整数而不是整数，否则出现未预期的值
1. 确保值符合预期
2. 有些处理器处理无符号比有符号的运算速度更快

## 2. 高内聚低耦合

1. 除非会被其他源文件调用，否则使用static修饰函数和全局变量的声明和定义
作用：
1. 对外隐藏实现细节
2. 不同文件可同名，而不会发生重定义
3. 无外部符号处理，减少编译时间
4. 节约内存（内存对齐和填充）

## 3. 提高执行效率

1. switch-case语句中，对case发生频率排序，频率越高越靠前，减少平均执行时间
```
当switch语句中的case标号很多时，为了减少比较的次数，明智的做法是把大switch语句转为嵌套switch语句。把发生频率高的case标号放在一个switch语句中，并且是嵌套switch语句的最外层，发生相对频率相对低的case标号放在另一个switch语句中。比如，下面的程序段把相对发生频率低的情况放在缺省的case标号内。         pMsg=ReceiveMessage();  
        switch (pMsg->type)  
        {  
        case FREQUENT_MSG1:  
        handleFrequentMsg();  
        break;  
        case FREQUENT_MSG2:  
        handleFrequentMsg2();  
        break;  
        ......  
        case FREQUENT_MSGn:  
        handleFrequentMsgn();  
        break;  
        default:                      //嵌套部分用来处理不经常发生的消息        switch (pMsg->type)  
        {  
        case INFREQUENT_MSG1:  
        handleInfrequentMsg1();  
        break;  
        case INFREQUENT_MSG2:  
        handleInfrequentMsg2();  
        break;  
        ......  
        case INFREQUENT_MSGm:  
        handleInfrequentMsgm();  
        break;  
        }  
        }     如果switch中每一种情况下都有很多的工作要做，那么把整个switch语句用一个指向函数指针的表来替换会更加有效，比如下面的switch语句，有三种情况：        enum MsgType{Msg1, Msg2, Msg3}  
        switch (ReceiveMessage()  
        {  
        case Msg1;  
        ......  
        case Msg2;  
        .....  
        case Msg3;  
        .....  
        }

    为了提高执行速度，用下面这段代码来替换这个上面的switch语句。

        /*准备工作*/  
        int handleMsg1(void);  
        int handleMsg2(void);  
        int handleMsg3(void);  
        /*创建一个函数指针数组*/  
        int (*MsgFunction [])()={handleMsg1, handleMsg2, handleMsg3};  
        /*用下面这行更有效的代码来替换switch语句*/  
        status=MsgFunction[ReceiveMessage()]();

```

1. 全局变量，使用全局变量比向函数传递参数更加有效率，这样做去除了函数调用前参数入栈和函数完成后参数出栈的需要，但会造成内存占用增加 #空间换时间
2. 使用inline内联函数，请求编译器用函数内部的代码替换所有在被调用的函数中（类似宏替换） #空间换时间
作用：
1. 省去了调用指令需要的执行时间
2. 省去了传递变元和传递过程需要的时间
3. 增加程序代码size
在函数被频繁调用且只含几行代码时，最有效

4. 用指针运算代替数组索引
能产生又快又短的代码。与数组索引相比，指针一般能使代码速度更快，占用空间更少。使用多维数组时差异更明显。
```C
// 数组索引
while (1) {
	a = array[i++];
}

// 指针运算
p = array;
while (1) {
	a = *(p++);
}

// array的地址每次装入地址p后，在每次循环中只需对p增量操作。在数组索引方法中，每次循环中都必须进行基于i求数组下标的复杂运算
```

4. 尽量使用void
无函数参数；
当函数返回值不会被使用时，则不要返回值即返回void

5. 手动编写汇编指令
适当的使用内联汇编指令可以有效的提高整个系统运行的效率。

6. 使用寄存器变量
 在声明局部变量的时候可以使用register关键字。这就使得编译器把变量放入一个多用途的寄存器中，而不是在堆栈中，合理使用这种方法可以提高执行速度。函数调用越是频繁，越是可能提高代码的速度。

7. 使用增量和减量操作符
增量符语句比赋值语句更快，原因在于对大多数CPU来说，对内存字的增、减量操作不必明显地使用取内存和写内存的指令
x=x+1;    模仿大多数微机汇编语言为例，产生的代码类似于：    move A,x      ;把x从内存取出存入累加器A  
    add A,1       ;累加器A加1  
    store x       ;把新值存回x

   如果使用增量操作符，生成的代码如下：    incr x        ;x加1    显然，不用取指令和存指令，增、减量操作执行的速度加快，同时长度也缩短了。

8. 减少函数调用参数
   使用全局变量比函数传递参数更加有效率。这样做去除了函数调用参数入栈和函数完成后参数出栈所需要的时间。然而决定使用全局变量会影响程序的模块化和重入，故要慎重使用。



命名

函数命名，动宾结构还是宾动结构，如SendData或DataSend
static 是否需要添加前缀下划线

头文件、源文件最后预留一个空行

typedef XXX XXX_t   _t表示是typedef结构


