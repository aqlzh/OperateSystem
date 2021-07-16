@[toc]
# I /O核心子系统
## 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716120151920.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 这些功能要在哪个层次实现？
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716162032681.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## IO 调度
- **I /O调度：用某种算法确定一个好的顺序来处理各个I /O请求。**
- 如：磁盘调度（先来先服务算法、最短寻道优先算法、SCAN算法、C-SCAN算法、LOOK算法、C-LOOK算法）.当多个磁盘I /O 请求到来时，用某种调度算法确定满足I /O请求的顺序
- 同理，打印机等设备也可以用先来先服务算法、优先级算法、短作业优先等算法来确定I/ O调度顺序。

## 设备保护
- 操作系统需要实现文件保护功能，不同的用户对各个文件有不同的访问权限（如：只读、读和写等）.
- 在UNIX系统中，设备被看做是一种特殊的文件，每个设备也会有对应的FCB.当用户请求访问 ,某个设备时，系统根据FCB中记录的信息来判断该用户是否有相应的访问权限，以此实现“设备保护”的功能。（参考“文件保护”小节）

## 小结思维图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716162529515.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
# 假脱机技术（SPOOLing技术）
## 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716162632900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

## 什么是脱机技术
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716162756885.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- Tips：为什么称为“脱机”一一脱离主机的控制进行的输入/输出操作。
- 引入脱机技术后，缓解了CPU与慢速I /O设备的速度矛盾。另一方面，即使CPU在忙碌，也可以提前将数据输入到磁带；即使慢速的输出设备正在忙碌，也可以提前将数据输岀到磁带。

- “假脱机技术”，又称“ SPOOLing技术”是用==软件的方式==模拟脱机技术。 SPOOLing系统的组成如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716163229780.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- “输入进程” 模拟脱机技术输入时的外围控制机
- “输出进程” 模拟脱机输出时的外围控制机

- 要实现 SPOOLing技术，必须要有==多道程序技术==的支持。系统会建立“输入进程”和“输出进程”


> 注意：输入缓冲区和输出缓冲区是在内存中的缓冲区 ， 在输入进程的控制下，“**输入缓冲区**”用于暂存从输入设备输入的数据，之后再转存到输入井中 ， 在输出进程的控制下，“**输出缓冲区**”用于暂存从输出井送来的数据，之后再传送到输出设备上



## 共享打印机原理分析
- 独占式设备——==只允许各个进程串行使用的设备==。一段时间内只能满足一个进程的请求。
- 共享设备一一允许多个进程“同时”使用的设备（宏观上同时使用，微观上可能是交替使用）.可以同时满足多个进程的使用请求。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716165013422.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 虽然系统中只有一个台打印机，但每个进程提出打印请求时，系统都会为在输出井中为其分配一个存储区（相当于分配了一个逻辑设备），使每个用户进程都觉得自己在独占一台打印机，从而实现对打印机的共享。
- SPOOLing技术可以把一台物理设备==虚拟==成逻辑上的多台设备，可将==独占式设备改造成共享设备==。

## 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210716165201737.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

