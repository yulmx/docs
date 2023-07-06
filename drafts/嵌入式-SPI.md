
GD25Q16BS为一款FLASH，以下举例：
![](Pasted%20image%2020230701232049.png)

CS：片选信号，CS为低电平，FLASH被选中。也就是CS低电平有效。
HOLD: 保持接口
WP:写保护接口
SO：即MISO（mater in slave out），主设备数据接收，从设备数据发送（主设备即master为芯片，从设备即slave为flash、其他组件芯片等）
SI：与SO相反，（mater out slave in）
全双工通信：SI、SO一起组成全双工通信，即可同时收发

SPI：SO、SI、SCLK、CS4个组成，即四线制
DSPI：由SO、SI、SCLK、CS4个组成，即也是四线制。与SPI的区别在于，SPI中的SO/SI只是单向，DSPI中的SO/SI可以双向，即SO不再只支持主设备接收从设备发送，而是支持主设备既可接收也可发送，即SO、SI都变成了双向的IO口。故传输数据量是SPI的两倍
QSPI：由SI SO HOLD WP CS SCLK 6根线组成，即六线制。与SPI的区别在于，HOLD、WP也可传输数据，即变成IO口

很多flash都同时支持这SPI DSPI QSPI三种模式，具体切换方式需查看Flash的DATASHEET。


[基础——SPI与QSPI的异同，QSPI的具体协议是什么，QSPI有什么用_qspi和spi接口的区别_口袋里のInit的博客-CSDN博客](https://blog.csdn.net/wangguchao/article/details/105593303)

[第24章 QSPI—读写串行FLASH - 野火_firege - 博客园 (cnblogs.com)](https://www.cnblogs.com/firege/p/9435349.html)