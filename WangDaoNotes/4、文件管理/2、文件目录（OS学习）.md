@[toc]
# 知识总览思维导图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071318255621.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
## 文件控制块
- FCB的有序集合称为“文件目录”，一个FCB就是一个文件==目录项==。FCB中包含了文件的==基本信息==（==文件名==、==物理地址==、逻辑结构、物理结构等），存取控制信息（是否可读/可写、禁止访问的用户名单等），使用信息（如文件的建立时间、修改时间等）
- 最重要，最基本的还是==文件名==、==文件存放的物理地址==。
- 目录文件中的一条记录就是一个“文件控制块（FCB）”
- FCB实现了文件名和文件之间的映射。使用户（用户程序入可以实现“按名存取”

### 目录操作

> - **搜索**：当用户要使用一个文件时，系统要根据文件名搜索目录，找到该文件对应的目录项
> - **创建文件**：创建一个新文件时，需要在其所属的目录中增加一个目录项
> - **删除文件**：当删除一个文件时，需要在目录中删除相应的目录项
> - **显示目录**：用户可以请求显示目录的内容，如显示该目录中的所有文件及相应属性
> - **修改目录**：某些文件属性保存在目录中，因此这些属性变化时需要修改相应的目录项（如：文件重命名）

## 目录结构
### 单级目录
- 早期操作系统并不支持多级目录，整个系统中只建立一张目录表，每个文件占一个目录项。
- 单级目录实现了“按名存取”，但是==不允许文件重名==。
- 在创建一个文件时，需要先检查目录表中有没有重名文件，确定不重名后才能允许建立文件，并将新文件对应的目录项插入目录表中。
- 显然，单级目录结构不适用于多用户操作系统。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071320544747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
### 两级目录
- 早期的多用户操作系统，采用两级目录结构。分为主文件目录（MFD， Master File Directory）和用户文件目录（UFD， User Flie Directory）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210713205823365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
### 多级目录结构
- 又称为树形目录结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210713210125958.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
当前目录的应用（相对路径）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210713210311881.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- ==树形目录结构==可以很方便地对文件进行分类，层次结构清晰，也能够更有效地进行文件的管理和保护。但是，树形结构==不便于实现文件的共享==。因此，提出了“<font color=red size=4>**无环图目录结构**</font>”.

### 无环图目录结构
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210713211103790.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
### 索引结点（FCB 改进）
![在这里插入图片描述](https://img-blog.csdnimg.cn/202107132136236.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)
- 平均查询目录项个数（320） = 【最大的目录项数（640） + 最小的目录项数（0）】/2  
- 平均启动磁盘数 = 40 / 2 = 20 


> - 当找到文件名对应的目录项时，才需要将索引结点调入内存，索引结点中记录了文件的各种信息，包括文件在外存中的存放位置，根据“存放位置”即可找到文件。
> - 存放==在外存中==的索引结点称为“==磁盘索引结点==”，当索引结点放入内存后称为“内存索引结点”.
> - 相比之下==内存索引结点中需要增加一些信息==，比如：文件是否被修改、此时有几个进程正在访问该文件 等

## 总结思维导图
==重要==
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210713214255883.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1F1YW50dW1Zb3U=,size_16,color_FFFFFF,t_70)

