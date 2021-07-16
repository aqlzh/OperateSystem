@[toc]
# I/O  控制方式 (重要)
## 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071609045031.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 程序直接控制方式
<font color=red size=4>1、完成一次 读/写  操作的流程 （轮询）</font >

- 见下图2  的程序流程图
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716091036151.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716092047203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
<font color=red size=4>2、CPU 干预的频率</font>
- 很频繁，I /O操作开始之前、完成之后需要CPU介入，并且在等待I /O完成的过程中CPU需要不断地轮询检查。


<font color=red size=4>3、数据传送的单位</font>
- 每次读 / 写一个字


<font color=red size=4>4、数据的流向</font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716092540476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

<font color=red size=4>5、主要缺点和主要优点</font>
- **优点**：实现简单。在读/写指令之后，加上实现循环检查的一系列指令即可（因此才称为“程序直接控制方式”）
- **缺点**：CPU和 I /O设备只能串行工作，CPU需要一直轮询检查，长期处于“忙等”状态，CPU利用率低。

## 中断驱动方式
- 引入==中断机制==。由于I /O设备速度很慢，因此在CPU发出读/写命令后，可将==等待I /O的进程阻塞==，先切换到别的进程执行。当I/O完成后，控制器会向CPU发出一个中断信号，CPU==检测到中断信号==后，会保存当前进程的运行环境信息，转去执行中断处理程序处理该中断。处理中断的过程中，CPU从I/O控制器读一个字的数据传送到==CPU寄存器，再写入主存。接着，CPU恢复等待I/O的进程（或其他进程）的运行环境，然后继续执行==。

> 注意：
>  ①CPU会在每个**指令周期的末尾**检查中断；
> ②中断处理过程中需要保存、恢复进程的运行环境这个过程是需要一定时间开销的。可见，如果中断发生的频率太高，也会**降低系统性能**。


<font color=red size=4>1、完成一次 读/写  操作的流程 （轮询）</font >
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716093906540.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

<font color=red size=4>2、CPU 干预的频率</font>
每次I/O操作开始之前、完成之后需要CPU介入。
**等待I /O完成的过程中CPU可以切换到别的进程执行**。


<font color=red size=4>3、数据传送的单位</font>
每次读 / 写**一个字**


<font color=red size=4>4、数据流向</font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716103025114.png)
<font color=red size=4>5、主要优点和缺点</font>
- **优点**：与“程序直接控制方式”相比，在“中断驱动方式”中，I /O控制器会通过中断信号主动报告I/ O已完成，CPU不再需要不停地轮询。==CPU和I /O设备可并行工作==，CPU利用率得到明显提升。
- **缺点**：每个字在I/ O设备与内存之间的传输，都需要经过CPU.==而频繁的中断处理会消耗较多的CPU时间==。

## DMA 方式

- 与“中断驱动方式”相比，==DMA方式==（ Direct Memory Access，直接存储器存取。主要用于块设备的  (I/ O控制）有这样几个改进

> ①  ==数据的传送单位是“块==”.不再是一个字、一个字的传送； 
> ② 数据的流向是从设备直接放入内存，或者从内存直接到设备。不再需要CPU作为“快递小哥”.
> ③仅在传送一个或多个数据块的开始和结束时，才需要CPU干预。


<font color=red size=4>1、完成一次读 / 写操作的流程</font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716104345238.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
<font size=5>**DMA  控制器**</font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716105447226.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

- `DR`（ Data Register，数据寄存器）：暂存从设备到内存，或从内存到设备的数据。
- `MAR`（ Memory Address Register，内存地址寄存器）：在输入时，MAR表示数据应放到内存中的什么位置；输出时MAR表示要输出的数据放在内存中的什么位置。
- `DC`（ Data Counter，数据计数器）：表示剩余要读/写的字节数。
- `CR`（ Command Register，命令/状态寄存器）：用于存放CPU发来的 I /O命令，或设备的状态信息。


<font color=red size=4>2、CPU  的干预频率</font>
仅在传送一个或多个数据块的开始和结束时，才需要CPU干预。


<font color=red size=4>3、数据传送的单位</font>
每次读/==写一个或多个块==（注意：每次读写的只能是连续的多个块，且这些块读入内存后在内存中也必须是连续的）


<font color=red size=4>4、数据的流向（不需要经过 CPU）</font>
读操作（数据输入）：I /O设备→内存
写操作（数据输出）：内存 ->I /O设备


<font color=red size=4>5、主要缺点和优点</font>
- **优点**：数据传输以“块”为单位，CPU介入频率进一步降低。数据的传输不再需要先经过CPU再写入内存，数据传输效率进一步增加。CPU和 I /O设备的并行性得到提升。
- **缺点**：CPU每发出一条I /O指令，只能读/写一个或多个==连续==的数据块。如果要读/写多个离散存储的数据块，或者要将数据分别写到不同的内存区域时，CPU要分别发出多条I /O指令，进行多次中断处理才能完成。


## 通道方式
- <font color=red size=4>**通道**</font>：一种硬件，可以理解为是“弱鸡版的CPU” (*与CPU相比，通道可以执行的指令很单一，并且通道程序是放在主机内存中的，也就是说通道与CPU共享内存*).通道可以识别并执行一系列通道指令

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716110817484.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)


<font color=red size=4>1、完成一次读/写操作的流程（见下图)</font>

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716111920906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

<font color=red size=4>2、CPU干预的频率</font>
极低，通道会根据CpU的指示执行相应的通道程序，只有完成一组数据块的读/写后才需要发出中断信号，请求CPU干预。
<font color=red size=4>3、 数据传送的单位</font>
每次读/写一组数据块
<font color=red size=4>4、数据的流向（在通道的控制下进行）</font>
读操作（数据输入）  I/O设备→内存
写操作（数据输出）：内存--->I /O设备
<font color=red size=4>5、主要缺点和主要优点</font>
**缺点**：实现复杂，需要专门的通道硬件支持
**优点**：CPU、通道、O设备可并行工作，资源利用率很高。



## 总结思维表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716112020450.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 一个通道可以控制多个 I/O 控制器 ，一个I/O控制器可以控制多个设备

#  I/O软件层次结构
## 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716112638853.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

## 用户层软件
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071611321652.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 设备独立性软件
- ==设备独立性软件==，又称==设备无关性软件==。与设备的硬件特性无关的功能几乎都在这一层实现。

**系统调用**主要实现的功能：
- <font color=skyblue size=4>**①向上层提供统一的调用接口（如read/ write系统调用）**</font>

- <font color=skyblue size=4>②**设备的保护** 原理类似与文件保护。设备被看做是一种特殊的文件，不同用户对各个文件的访问权限是不一样的，同理，**对设备的访问权限也不一样**。</font>

- <font color=skyblue size=4>③**差错处理** 设备独立性软件需要对一些设备的错误进行处理</font>

- <font color=skyblue size=4>**④设备的分配与回收**</font>


- <font color=skyblue size=4>**⑤数据缓冲区管理**  可以通过缓冲技术屏蔽设备之间数据交换单位大小和传输速度的差异</font>
- <font color=skyblue size=4>⑥建立**逻辑设备名到物理设备名**的映射关系；根据设备类型选择调用相应的驱动程序</font>
用户或用户层软件发出I/O操作相关系统调用的系统调用时，需要指明此次要操作的I / O设备的逻辑设备名（eg：去学校打印店打印时，需要选择打印机1/打印机2/打印机3，其实这些都是==逻辑设备名==）
==设备独立性软件==需要通过“逻辑设备表（LUT， Logical UnitTable）”来确定逻辑设备对应的物理设备，并找到该设备对应的==设备驱动程序==




![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716114848360.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 思考：为何不同的设备需要不同的设备驱动程序？
- 不同设备的内部硬件特性也不同，这些特性只有厂家才知道，因此厂家须提供与==设备相对应的驱动程序==，CPU执行驱动程序的指令序列，来完成设置设备寄存器，检查设备状态等工作

## 设备驱动程序
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716115150945.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

## 中断处理程序
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716115644252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 总结思维图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716115800630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 对逻辑设备表（LUT）有了解
