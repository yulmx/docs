
优化优先级
-O0：无优化
-O1：默认缺省值
-O2
-O3：级别最高
-Os：相当于-O2.5，使用了所有-O2的优化选项，但又不增加代码尺寸

```
Level 2.5 (-Os)

The special optimization level (-Os or size) enables all -O2 optimizations that do not increase code size; it puts the emphasis on size over speed. This includes all second-level optimizations, except for the alignment optimizations. The alignment optimizations skip space to align functions, loops, jumps and labels to an address that is a multiple of a power of two, in an architecture-dependent manner. Skipping to these boundaries can increase performance as well as the size of the resulting code and data spaces; therefore, these particular optimizations are disabled. The size optimization level is enabled as:

gcc -Os -o test test.c
In gcc 3.2.2, reorder-blocks is enabled at -Os, but in gcc 3.3.2 reorder-blocks is disabled.
```


http://gcc.gnu.org/onlinedocs/gcc-3.4.6/gcc/Optimize-Options.html#Optimize-Options

[Optimization in GCC | Linux Journal](https://www.linuxjournal.com/article/7269)
