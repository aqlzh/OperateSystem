> 我坚信，在考研过程中培养的品质，一定会在今后闪闪发辉

@[toc]
#  操作系统的概念定义
- 计算机系统的层次结构
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210629132310428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- **操作系统**（ Operating System，os）是指控制和管理整个计算机系统的硬件和软件资源，并合理地组织调度计算机的工作和资源的分配，以提供给用户和其他软件方便的接口和环境，它是计算机系统中最基本的系统软件。

# 操作系统的概念和目标
从以下三大方面进行阐述：
- 操作系统作为系统资源的管理者
- 操作系统作为用户与计算机硬件之间的接口
- 操作系统作为最接近硬件的层次
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021062913262140.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 系统资源的管理者
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630102842578.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 用户与计算机硬件之间的接口
- 命令接口：允许用户直接使用
- 程序接口：允许用户通过程序间接使用
- GUI：现代操作系统中最流行的图形用户接口
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630104310305.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630104622893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 联机命令又称为交互式命令     CMD  中的命令
- 脱机命令又称为批处理命令     `*.bat`  的命令   一次执行

- 程序接口：如`C：\ Windows\ System32 \ user32.dll`程序员在程序中调用user32.dll（该调用过程即为系统调用）即可实现创建窗口等功能。只能通过用户程序间接使用。


==注意==：系统调用=系统调用命令=`广义指令`


- **GUI**：图形用户界面（ Graphical User Interface）
用户可以使用形象的图形界面进行操作，而不再需要记忆复杂的命令、参数。
例子：在 Windows操作系统中，删除一个文件只需要把文件“拖拽”到回收站即可。

## 最接近硬件的层次
- 需要提供的功能和目标：实现对硬件机器的拓展
没有任何软件支持的计算机成为裸机。在裸机上安装的操作系统，
- 可以提供资源管理功能和方便用户的服务功能，将裸机改造成功能更强、使用更方便的机器。通常把覆盖了软件的机器成为扩充机器，又称之为虚拟机。


# 小结
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630223059979.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
# 操作系统的四个特征
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021063022430065.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 并发
- **并发**：指两个或多个事件在`同一时间间隔`内发生。这些事件宏观上是同时发生的，但微观上是交替发生的。
常考易混概念一一**并行**：指两个或多个事件在`同一时刻同时`发生。


- **操作系统的并发性**指计算机系统中同时存在着多个运行着的程序。
- 一个单核处理机（CPU）同一时刻只能执行一个程序，因此操作系统会负责协调多个程序交替执行（这些程序微观上是交替执行的，但宏观上看起来就像在同时执行）事实上，操作系统就是伴随着“多道程序技术”而岀现的。==因此，操作系统和程序并发是一起诞生的==。


## 共享
共享与并发的关系
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630232210182.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 虚拟
- 虚拟是指把一个物理上的实体变为若干个逻辑上的对应物。物理实体（前者）是实际存在的，而逻辑上对应物（后者）是用户感受到的。

- **问题**：这些程序同时运行需要的内存远大于4GB，那么为什么它们还可以在我的电脑上同时运行呢？
- **答**：这是虚拟存储器技术。实际只有4GB的内存，在用户看来似乎远远大于4GB。虚拟技术的==空分复用技术==

---
- **问题**：既然一个程序需要被分配CPU才能正常执行，那么为什么单核CPU的电脑中能同时运行这么多个程序呢？
- **答**：这是虚拟处理器技术。实际上只有一个单核CPU，在用户看来似乎有6个CPU在同时为自己服务

虚拟技术中的“==时分复用技术==”.微观上处理机在各个微小的时间段内交替着为各个进程服务

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630233041519.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 异步
- **异步**是指，在多道程序环境下，允许多个程序并发执行，但由于资源有限，进程的执行不是一贯到底的，而是走走停停，以不可预知的速度向前推进，这就是进程的异步性。

显然，如果失去了并发性，则系统只能串行地处理各个进程，每个进程的执行会一贯到底。只有系统拥有并发性，才有可能导致异步性。

# 小结
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210630233506178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

