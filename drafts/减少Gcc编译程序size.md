> 1、禁用调试信息
> 
>      Release编译时不要加上-g开关。
> 
> 2、使用-Os编译程序。
> 
>     不要使用-funroll-loops等可以加速程序执行但是会大大增加目标代码体积的开关。

> 3、编译后的程序使用strip去除符号和偏移（限于可执行程序和共享库，其他易出问题）。
> 
> 4、如果你不需要RTTI，编译时加入-fno-rtti。
> 
> 5、如果你不需要处理C++异常，编译时加入-fno-exceptions。
> 
> 6、使用UPX之类的可执行程序压缩程序（只推荐用于可执行程序，用于其他也可，但是较浪费内存）。

编译参数`CFLAGS`: `-Os -ffunction-sections -fdata-sections` （去掉`-g`参数，不启动调试）  
链接参数`LDFLAGS`: `-Wl,-Map=object.map,--cref,--gc-section`


- 好好写代码，减小代码段体积，别人300代码的逻辑你50行搞定，程序体积肯定有机会更小一些，这个就得考验开发者自己的编程功底了
- 使用strip，像脱衣服一样，移除程序的所有符号，这也是很多开发者常用的方式
- strip只会清除普通符号，不会动态符号表中的符号，某些动态符号其实也可以隐藏掉，进而来减小库的体积，可以使用-fvisibility=hidden命令
- 巧用.bss段，未初始化的全局变量和局部静态变量会存在.[bss段](https://www.zhihu.com/search?q=bss%E6%AE%B5&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1755070166%7D)中，这些变量不占用程序空间。
- inline-limit：内联过多会导致代码段体积较大，可以通过此选项减少内联的数量
- 开启Os编译，这是产生较小代码体积的优化选项
- 编译选项-[fdata-sections](https://www.zhihu.com/search?q=fdata-sections&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1755070166%7D)和-ffunction-sections
- 考虑链接动态库而非[静态库](https://www.zhihu.com/search?q=%E9%9D%99%E6%80%81%E5%BA%93&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1755070166%7D)

[Linux如何优化程序的体积大小？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/446899354)


如果是我们自己的程序，那我们可以通过编译debug或release版本来控制生成文件的大小。一般来说我们在开发阶段编译debug版本，这样出现问题我们可以通过gdb等工具进行调试；而在发布阶段编译release版本，这样可以大幅减小目标文件的大小。如果我们使用gcc/g++编译器的话，-g和-ggdb参数会生成debug版本

动态库
若该动态库是debug版本，可使用objcopy --strip-debug XXX.so去除Debug信息

怎么判断程序是debug还是release版本
readelf -S 程序文件 | grep debug，如果没有任何内容输出即是release版本，如果看到类似如下的信息就是debug版本。
```
.debug_aranges
.debug_info
.debug_abbrev
.debug_line
.debug_str
.debug_ranges
```