
gcc链接是以section作为最小的处理单元，只要一个section中的某个符号被引用，该section就会被加入到可执行程序中去。

在编译时可以使用 -ffunction-sections 和 -fdata-sections 将每个函数或符号创建为一个sections，其中每个sections名与function或data名保持一致。而在链接阶段， -Wl,–gc-sections 指示链接器去掉不用的section（其中-wl, 表示后面的参数 -gc-sections 传递给链接器），这样就能减少最终的可执行程序的大小了。

```
CFLAGS += -ffunction-sections -fdata-sections
LDFLAGS += -Wl,--gc-sections
```