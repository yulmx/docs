[充分理解Linux GCC 链接生成的Map文件 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/502051758)

## 组成

### 1. 获取内存分区信息 `Memory Configuration`

> 显示每个内存块的位置、大小、使用情况

Name：内存块名称
Origin：起始地址
Length：大小size
Attribute：

## 2. 段信息 `Section`

Idx：index，索引，从0开始
Name：段名，如startup、stack、text、data、bss、heap、debug_***、comment等


### 3. Archive member included to satisfy reference by file（symbol）

> 记录所有静态库.a包含的所有目标文件.o

### 4. Allocating common symbols
> 记录所有符号信息，符号名，size，所在文件

### 5. Discarded input sections
> 丢弃段，指未被使用的变量和函数，不占size

### 6. Linker script and memory map

### 7. debug信息

### 8. Cross Reference Table
