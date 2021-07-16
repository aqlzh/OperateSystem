@[toc]
# 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715180817359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
==本节属于交互知识点==
[对比链接](https://blog.csdn.net/QuantumYou/article/details/117529158)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715181336409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)



## 什么是I/ O设备
- I/O设备就是可以将数据输入到计算机，或者可以接收计算机输出数据的外部设备，属于计算机中硬件部件。

- UNIX系统将外部设备抽象为一种特殊的文件，用户可以使用与文件操作相同的方式对外部设备进行操作。
- `Write操作`：向外部设备写出数据
- `Read操作`：从外部设备读入数据

## I/O设备的分类一一按使用特性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715212813990.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 人机交互类外设：鼠标、键盘打印机等一一用于人机交互
- 存储设备：移动硬盘、光盘等一一用于数据存储
- 网络通信设备：调制解调器等一一用于网络通信

## I/O设备的分类一一按传输速率分类
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071521355798.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

- 低速设备：鼠标、键盘等一一传输速率为每秒几个到几百字节
- 中速设备：如激光打印机等一一传输速率为每秒数千至上万个字节
- 高速设备：如磁盘等传输速率为每秒数千字节至千兆字节的设备

## I/O设备的分类一一按信息交换的单位分类

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715213718622.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 块设备：如磁盘等一一数据传输的基本单位是“块"
- 字符设备：鼠标、键盘等一一数据传输的基本单位是字符
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715213942139.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)


## 总结思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071521580634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
# I /O控制器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715215854503.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

- I /O设备的==机械部件==主要用来执行具体I /O操作。
- 如我们看得见摸得着的鼠标/键盘的按钮；显示器的LED屏；移动硬盘的磁臂、磁盘盘面。
- I/ O设备的==电子部件==通常是一块插入主板扩充槽的印刷电路板。

## I/O设备的电子部件（I/O控制器）

- CPU无法直接控制I/O设备的机械部件，因此I/O设备还要有一个电子部件作为CPU和I/ O设备机械部件之间的“中介”，用于实现CPU对设备的控制。
- 这个电子部件就是I / O控制器，又称设备控制器。CPU可控制I/ O控制器，又由I /O控制器来控制设备的机械部件。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716083509393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

## I /O 控制器的组成
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071608530290.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

值得注意的小细节：
- ①一个I/ O控制器可能会对应多个设备
- ②数据寄存器、控制寄存器、状态寄存器可能有多个（如：每个控制/状态寄存器对应一个具体的设备），且这些寄存器都要有相应的地址，才能方便CPU操作。有的计算机会让这些寄存器占用内存地址的一部分，称为`内存映像I/ O`；另一些计算机则采用I/ O专用地址，即`寄存器独立编址`。

## 内存映像I/O v.s. 寄存器独立编址
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716085510145.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

## 总结思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716085846403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

