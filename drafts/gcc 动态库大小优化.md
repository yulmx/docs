
目标
1. 在不影响功能的情况下，缩小.so文件的大小；
2. 条件允许下，删除部分代码以得到更小的size

## 方法

1. 清除符号表信息 strip -s <exe>或gcc -Wl,-s [代码优化-清除符号表信息](drafts/代码优化-清除符号表信息.md)
2. 使用gcc编译优化选项 -Os
3. 链接时去掉未用的变量和函数
4. 未使用代码解耦

在一些业务场景下，需要对动态库的大小进行限制，主要有如下几种方法：

1. 编译选项使用-Os，表示以最小化大小为优化方向

2. 去除-g选项，进而去除调试信息

3. 通过strip裁剪符号及调试信息

4. 只导出必要符号

Linux默认导出所有符号，并不仅仅导出你开放的接口！

定义如下宏：

#define SYMBOL_EXPORT __attribute__ ((visibility("default")))

在你想导出的符号前加上SYMBOL_EXPORT就好。

同时，需要在脚本中增加如下编译选项：-fvisibility=hidden

譬如：导出符号是int add(int a, int b)；那么添加的结果就是SYMBOL_EXPORT int add(int a, int b)；

通过这种方式只导出想导出的符号，也可以减小库大小。

 

备注

“default”：用它定义的符号将被导出，动态库中的函数默认是可见的。”hidden”：用它定义的符号将不被导出，并且不能从其它对象进行使用，动态库中的函数是被隐藏的。

default意味着该方法对其它模块是可见的。而hidden表面该方法符号不会被放到动态符号表里，所以其它模块(可执行文件或者动态库)不可以通过符号表访问该方法。


[(避免踩坑@!)聊一聊动态链接库的小细节 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/363981042)

[在Linux环境下如何消减可执行文件或者动态库的大小-云社区-华为云 (huaweicloud.com)](https://bbs.huaweicloud.com/blogs/detail/173854)

[如果对一个动态链接库strip，那这个库还能用来链接了吗？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/437881590)