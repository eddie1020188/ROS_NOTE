---
typora-root-url: 出差ROS小车笔记图片
---

# 1.0 智能驾驶开发导论

### 1.1 ROS智能驾驶系统简介 6月17 

原文参考链接：https://blog.csdn.net/qq_25267657/article/details/84316111

#### 1.1.1 ROS概述

​      从下面这张图片来看，ROS是2007年诞生与斯坦福大学，斯坦福大学，世界名校，而且是专业研究机器人的，目前也在从事人工智能的研发，ROS诞生于这样的贵族，可见ROS的发展还是非常有前途的。 

​      ROS（机器人操作系统）是一个灵活的软件框架，专为机器人软件开发设计。尽管被称为操作系统，它实际上是一系列运行在传统操作系统上的程序和库的集合，提供了丰富的工具和库来简化机器人编程。它支持模块化设计，允许开发者将各种功能如传感器驱动、数据处理和执行算法等轻松集成。此外，ROS支持多种编程语言，包括Python和C++，使得开发者可以选择最适合特定任务的语言。它拥有一个活跃的全球社区，提供大量的资源和教程，这大大促进了机器人技术的研究与应用发展。 



**ROS又为什么来到这个世界上呢？**

这个问题可得询问斯坦福大学的机器人专家了，为什么开发了这样一个机器人操作系统，不过目前大家也都知道了。最初人们是想设计制造一个复杂的机器人，这个机器人能够类似于人一样能够感知，自我导航，能够自我控制去做一些复杂的工作。面对这么复杂的工作，在研发过程中肯定需要很多各样的有效资源的共享，但是目前很多资源要么难以共享，要么共享的资源之间不能直接拿过来用，所以，急需这样一个能够整合资源的框架和接口，使得资源之间能够共享使用，换个专业点的话说，就是使得各种功能、各种软件的重复利用率增加。因此为了 满足这一功能和作用，我们研发了ROS（robotics operating system）机器人操作系统，虽然表面上叫做操作系统，但是并不是真正的操作系统，说白了，就是一个框架，一个平台。



**ROS的发展又如何呢？**

 ROS目前应用得非常广泛，春晚的百度无人车队大家可以去搜一搜，看一看，百度花大价钱能够对ROS进行开发，说明这个东东确实还算是比较有价值的一个东东。 

ROS目前能够应用的是机器人领域，包括移动机器人和机械臂，移动机器人应该是应用最广泛的，主要是应用于机器人的建模、感知、导航、规划等，其可以和普通机器人结合进而控制真实机器人，功能的确强大，而且随着目前的发展势头，其功能是越来越强大。下面简单以几个例子来说明。
ROS用在机器人领域，机器人可以是移动机器人，也可以是机械臂，移动机器人就是类似于扫地机器人的那种，当然机器人也可以是移动机器人和机械臂的组合，比如下面这幅图的这个机器人。

 从这幅图可以看出，ROS能够完成的东西还是真的挺多的哈，用其搭建的机器人完全就可以当成一个服务机器人来用了，可以叠衣服、做饭，还可以陪你玩桌球。
下面这幅图是ROS用在无人车领域，可以自动构建地图、导航和规划行进路径，和前面所说的百度无人车类似。 

目前ROS能够结合的机器人也挺多的，国际上有名的工业机器人、协作机器人、服务机器人等绝大多数都已经用ROS开发过，所以在网上也是大把的资源。
但是ROS也有一些问题，就是目前实时性不是太强，所以ROS也推出了2.0版本，还有就是ROS在运行的时候容易崩溃，所以稳定性也有待提高，但是从总体上看，ROS运用在机器人领域还是蛮有优势的。



#### 1.1.2 基于ROS的智能驾驶系统

​    基于ROS的智能驾驶系统是一种集成了机器人操作系统（ROS）的先进驾驶辅助系统，主要用于增强汽车的自动化驾驶能力。这一系统利用ROS的强大功能，例如多语言支持、模块化设计以及庞大的开发者社区资源，来处理和协调车辆的各种传感器输入、控制命令和导航策略。

​    在智能驾驶系统中，ROS作为中间件，能有效管理来自车辆雷达、摄像头、GPS和其他传感器的数据流，支持实时数据处理和决策制定。系统通过ROS的通信机制，如主题发布/订阅、服务和动态参数配置，实现模块间的高效数据交换和同步，从而实现路径规划、障碍物检测、车道保持和自适应巡航控制等功能。

此外，ROS的开放性和灵活性使得基于ROS的智能驾驶系统可以轻松集成新的算法和技术，适应不断变化的驾驶环境和技术进步。这一系统不仅提高了车辆的自动驾驶性能，还增强了驾驶安全性，为未来的全自动驾驶技术发展奠定了坚实的基础。

### 1.2 ROS极简概念

1.Mini ROS小车附送资料\3.ROS开发手册

#### 1.2.1 节点

在ROS（Robot Operating System，机器人操作系统）中，节点（Nodes）和节点管理器（通常称为roscore）是ROS架构的基本组成部分。

1. **节点（Nodes）**：
   - 节点是ROS中的基本执行单元。一个节点通常是一个程序，负责一项特定的任务，比如控制摄像头、处理激光雷达数据或驱动电机。
   - 每个节点可以独立运行，并与其他节点通过消息传递进行通信。这种设计使得ROS系统可以很容易地模块化和扩展。例如，一个节点可以只负责读取传感器数据，另一个节点则负责根据这些数据做决策。
   - 节点间的通信主要通过两种方式：话题（Topics）和服务（Services）。话题用于发布/订阅模式的通信，例如一个节点发布摄像头图像，其他节点订阅这些图像进行处理；服务则用于请求/响应模式的通信，例如一个节点请求另一个节点执行某个动作或计算。

2. **节点管理器（roscore）**：
   - roscore是ROS运行的核心，负责协调网络中的各个节点。启动一个ROS系统之前，必须先启动roscore。
   - roscore包含几个关键部分：参数服务器（Parameter Server）、ROS主控（Master）和rosout日志节点。
     - **参数服务器**：为节点提供参数设置的存储和获取服务，节点可以在运行时从这里获取配置信息。
     - **ROS主控**：管理名称和注册，帮助节点相互找到并建立通信。当一个节点启动时，它会向ROS主控注册自己可以发布或订阅的话题以及提供的服务。
     - **rosout**：类似于系统的日志服务，所有节点的日志信息都可以发送到这里，方便集中查看和调试。

简单来说，节点是执行特定任务的程序，而roscore是使这些节点能够找到彼此并有效通信的管理系统。这种设计使得ROS非常适合于复杂且模块化的机器人软件开发。

#### 1.2.2工作空间

工作空间（workspace）通常指的是一个项目的整体工作环境，在这个环境中包含了你所需要的所有资源，比如代码文件、库文件、配置文件等。在不同的开发环境中，工作空间的具体内容和结构可能有所不同，但基本概念相同。这是为了确保在一个集中的地方可以进行代码编写、构建、调试和维护。

例如，文中提到的使用Keil IDE为STM32设置的工作空间，你可以把它理解为一个项目文件夹，其中包含了所有与你的STM32项目相关的资源。在这个工作空间中，你可以创建多个项目，每个项目包含其自己的源代码文件、库文件和其他相关设置。通过Keil IDE，你可以轻松管理这些项目，进行编译、调试和程序烧写。

简而言之，工作空间就是你所有开发活动发生的场所，你的代码、工具和设置都存储在这里，方便你进行系统的开发工作。

“简单理解为  存放了编译，下载工具 和代码等的一个工作文件夹  ”

#### 1.2.3 功能包

   功能包是放置源码的最小单元，源码（.cpp 文件或者.py 文件）必须放在功能包里面，功能包的路径一定要在 src 的路径下。除了源码文件，功能包还可以放置：cpp 的.h 头文件 launch 文件、param 参数文件、map 地图文件等。关于功能包的详细结构可以看下文的“2.2 功能包”小节。 

### 1.3 ROS小车硬件介绍

​      R550 是面向 ROS 教育入门场景的旗舰产品，R550 提供了多种底盘可选和源码级的视频教程（非演示教程），搭载高性价比雷达和深度相机等配件，可满足建图导航、深度学习、3D 视觉、机器人编队等方向的学习。提供技术支持，可以满足零基础入门和提高。 

####      1.3.1 STM32主控板介绍<img src="E:\出差\ROS小车笔记\图片\image-20240609100200015.png" alt="image-20240609100200015" style="zoom: 50%;" />



#### 1.3.2  鲁班猫1S介绍

##### 为什么需要STM32+工控机呢？

**STM32**：这是一个微控制器，主要用于处理实时任务，如电机控制、传感器数据读取和简单的数据处理。STM32在执行这些低层、实时任务时非常有效，因为它的实时操作能够保证快速和稳定的响应。

**树莓派或工控机**：这些设备是完整的计算机系统，拥有更强大的CPU和更多的内存，适合处理更复杂的任务，如图像处理、数据分析、复杂的算法运算，以及运行操作系统和ROS框架。这些任务对处理能力的需求远远超过了STM32的处理能力。

##### 鲁班猫1S开发板分析

​        鲁班猫是野火推出的高性能卡片电脑品牌，以鲁班为名，勉励工程师传承鲁班那样的工匠创新精神，争当当代鲁班； 以小猫为形，期盼大家如孩童如猫咪般充满好奇心，探索精神不止步，永远保持童心。 

![image-20240609100913006](E:\出差\ROS小车笔记\图片\image-20240609100913006.png)



 拥有不同性能的硬件型号，支持Ubuntu、Debian、Android等系统，提供多套教材，覆盖纯应用层用户以及系统开发用户，可以适合卡片电脑、教育机器人、家庭智能化中枢、Linux服务器、工业板卡等场景。 

鲁班猫官网：https://doc.embedfire.com/products/link/zh/latest/linux/ebf_lubancat.html

<img src="E:\出差\ROS小车笔记\图片\image-20240609103002485.png" alt="image-20240609103002485" style="zoom: 50%;" />

### 1.4环境搭建

#### 1.4.1 VMWARE下载

![image-20240611222756447](C:\Users\Eddie\AppData\Roaming\Typora\typora-user-images\image-20240611222756447.png)

双击安装

![image-20240611223006983](C:\Users\Eddie\AppData\Roaming\Typora\typora-user-images\image-20240611223006983.png)

![image-20240611223148029](C:\Users\Eddie\AppData\Roaming\Typora\typora-user-images\image-20240611223148029.png)

![miyap](C:\Users\Eddie\AppData\Roaming\Typora\typora-user-images\image-20240611223204820.png)

点击验证密钥 ，输入这段 密钥  MC60H-DWHD5-H80U9-6V85M-8280D

打开我们已经搭建好环境的虚拟机

![image-20240611224307297](E:\出差\ROS小车笔记\图片\image-20240611224307297.png)

![image-20240611225535665](E:\出差\ROS小车笔记\图片\image-20240611225535665.png)

打开虚拟机

![image-20240611225646633](E:\出差\ROS小车笔记\图片\image-20240611225646633.png)

成功！

#### 1.4.2 验证



### 1.5 LINUX基本知识点

入门：

 [Linux最常用的15个基本命令_linux系统基本操作命令-CSDN博客](https://blog.csdn.net/m0_67995737/article/details/130454560?ops_request_misc=%7B%22request%5Fid%22%3A%22171820747316800184162193%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=171820747316800184162193&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-130454560-null-null.142^v100^pc_search_result_base2&utm_term=linux基本操作命令&spm=1018.2226.3001.4187) 

进阶：

 [Linux命令大全（非常详细）从零基础入门到精通，看完这一篇就够了_linux常用命令-CSDN博客](https://blog.csdn.net/Javachichi/article/details/134610458?ops_request_misc=&request_id=&biz_id=102&utm_term=linux基本操作命令练习&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-134610458.142^v100^pc_search_result_base2&spm=1018.2226.3001.4187) 

LINUX下一切皆是文件

鼠标，键盘插上电脑都是文件。LINUX就是教授大家通过代码去操作文件。

#### 1.5.2 为什么要使用命令？

​    为什么要使用命令，即便我们看到LINUX中有操作界面，但是对它的操作是远不如指令高效方便和专业。

​    命令的本质实质上就是可执行的二进制文件。

​    linux下直接执行应用程序名然后回车即可。 

#### 1.5.3 LINUX目录的框架

在 Linux 系统中，所有内容都是以文件的形式保存和管理的，即「一切皆文件」。普通文件是文件，目录（Windows 下称为文件夹）是文件，硬件设备（键盘、监视器、硬盘、打印机）是文件，就连套接字（socket）、网络通信等资源也都是文件。

linux只有一个根目录，而且文件和目录被组织成一个单根倒置树结构，
此结构最上层是根目录，用“/”表示

根文件系统(rootfs)：root filesystem 标准Linux文件系统（如：ext4）

如下图：

![image-20240613163158176](/../图片/image-20240613163158176.png)

根目录不像windows可以分为C D E F盘等等，它只有一个，就叫/

/bin  -- 存放所有可执行的二进制文件  （相当于WINDOWS下的.exe文件）

![image-20240613163801605](/../图片/image-20240613163801605.png)

可执行文件都是用绿色来表示的

usr目录  -- 存放第三方库文件 --- 不属于LINUX操作系统提供的都是第三方库 比如标注的C库  第三方的可执行文件等

home目录 -- 家目录，也被称为用户目录，存放所有的当前用户数据，当前用户是？ wheeltec-client  后续的代码主要都是存放在HOME中的

 sbin  superbin 超级二进制文件 针对需要管理员权限才可执行的二进制文件

root  管理员目录

etc    存放LINUX操作系统下的环境变量 什么是环境变量呢？主要为了让操作系统可以找到对应的路径。

dev  设备目录  存放所有的硬件设备

 lib   库目录（LINUX系统提供的库文件等）

mnt 挂载目录 本质是在不同的操作系统之间架起一座桥梁 （鲁班猫中有一个LINUX系统 我可以稍后直接挂载到我的电脑的目录下 从而修改鲁班猫工控机中的代码）

#### 1.5.4 命令

linux执行一个应用程序 直接敲应用程序名 回车即可

#### （1） ls

```C
功能：显示当前所有的目录和文件
基础使用：ls
拓展    ：
      ls -a  显示所有隐藏文件   /*-a linux下的特殊符号 属性*/
      ls -l  显示所有文件的属性 
      ls -al 显示隐藏文件的属性 属性可叠加
```

```C
wheeltec-client@ubuntu:~$ ls
 1.ImageProcess.jpg    libuvc                         Videos
 5.ImageHistogram.py   Music                          wheeltec_arm
 cJSON                'nav_Astar&dijkstra.py'         wheeltec_hector
 cJSON.zip             Pictures                       wheeltec_robot
 Desktop               Public                         wheeltec_stepper_arm
 Documents             Realsense_install_2021.06.07   wheeltec_table_arm
 Downloads             SR2.2-HR1.1.3                  奥比中光上位机
 gazebo配置            SR2.2-HR1.1.3.zip              骨架识别依赖
 librealsense-master   Templates

 wheeltec-client@ubuntu:~$ ls -al
总用量 56208
drwxr-xr-x 36 wheeltec-client wheeltec-client     4096 6月  13 05:17  .
drwxr-xr-x  3 root            root                4096 2月   1  2023  ..

```

####  （2)  cd 

```c
功能：切换路径（cd:change dir）
用法：cd + 路径
路径的分类：
	1.绝对路径:从根目录开始计算的路径（路径以/开头）
	2.相对路径(逻辑路径)：从当前位置开始计算的路径
		. :当前所处的路径
		..:相对于当前路径的上一级路径。
		../..:上一级路径的上一级路径
```



#### （3)  sudo

```
功能：以管理员身份运行
用法：sudo + 需要执行的命名
```



#### （4）mkdir

```bash
功能：创建目录  make directory
用法：mkdir + 路径/目录名称 (路径不写，默认在当前路径下创建)

#实际用例1：
edu118@ubuntu:/$ cd /
edu118@ubuntu:/$ cd /home           #进入用户目录
edu118@ubuntu:/home$ cd ./edu118/   #进入edu118目录
edu118@ubuntu:~$                
edu118@ubuntu:~$ mkdir 231211   #在当前路径下创建231211目录
```



#### （5）mkdir

```
功能：显示当前所处的绝对路径
用法：pwd
实际用例：
edu118@ubuntu:/home$ cd ~
edu118@ubuntu:~$ pwd
/home/edu118
```



#### （6）chmod

修改指定文件的权限

```bash
0：没有权限（—）
1：执行权限（–x）
2：写权限（-w-）
3：写和执行权限（-wx）
4：读权限（r–)
5：读和执行权限（r-x）
6：读和写权限（rw-）
7：读、写和执行权限（rwx）
这里的每个数字代表文件所有者（owner）、文件所属组（group）和其他用户（others）的权限组合。

#示例  创建一个文件1218 并将权限改为最高
wheeltec-client@ubuntu:~/123$ mkdir 1218
wheeltec-client@ubuntu:~/123$ ls
1218   --> 蓝色
wheeltec-client@ubuntu:~/123$ chmod 777 1218
wheeltec-client@ubuntu:~/123$ ls
1218   --> 绿色 表示最高权限

权限的表达形式2：u g o a <+/-> r/w/x 
u:usr
g:group
o:other
a:all 
#将1218的当前用户和其它用户的读权限删除
例如： chmod uo-r 1218 
```

### （7）touch

```bash
功能：创建文件
用法：touch + 路径/文件名
```

```bash
#实际用例：
edu118@ubuntu:~/231211/1218$ cd ~/231211/1218
edu118@ubuntu:~/231211/1218$ touch 1.c 2.c 3.c 4.c
edu118@ubuntu:~/231211/1218$ ls
1.c  2.c  3.c  4.c
```

### （8）rm

```bash
功能：删除文件
用法：rm + 文件名
属性：
	-r:删除一个目录
	-f:强制删除
rm -rf:递归强制删除

```

```bash
#实际用例：删除1.c
edu118@ubuntu:~/231211/1218$ rm 1.c
edu118@ubuntu:~/231211/1218$ mkdir test1 test2 test3
#edu118@ubuntu:~/231211/1218$ rm test1
#rm: 无法删除'test1': 是一个目录
edu118@ubuntu:~/231211/1218$ rm -r test1  #删除test1目录
```

<img src="/E:/桌面/01-环境搭建和linux基础/3.课堂笔记/pic/image-20231218160236876.png" alt="image-20231218160236876" style="zoom:50%;" />

### （9）cp

```bash
功能：拷贝文件
用法：cp 源文件路径 目标文件路径
属性：
	-r:拷贝一个目录
```

```bash
#实际用例：
edu118@ubuntu:~/231211/1218$ cd ~/231211/1218
edu118@ubuntu:~/231211/1218$ ls
2.c  3.c  4.c  test2  test3
edu118@ubuntu:~/231211/1218$ cp /home/edu118/231211/1218/*.c ./test2/  #将所有的.c文件拷贝至test2目录下
#edu118@ubuntu:~/231211/1218$ cp ./test2 ./test3
#cp: 略过目录'./test2'
edu118@ubuntu:~/231211/1218$ cp -r ./test2 test3 # 将test2目录拷贝至test3目录下
```

### （10）mv

```bash
功能：移动一个文件或者目录（通常用于1.剪切文件 2.给文件修改名字）
用法：mv 源文件路径 目标文件路径
注意：
1.mv命名支持给移动后的文件/目录修改名称。
2.如果目标文件路径没有指定新的名称，则使用旧的名字。   
```

```bash
#实际用例1：将所有的.c文件移动到test3目录下
edu118@ubuntu:~/231211/1218$ cd ~/231211/1218
edu118@ubuntu:~/231211/1218$ ls
2.c  3.c  4.c  test2  test3
#将所有的.c文件移动到test3目录下
edu118@ubuntu:~/231211/1218$ mv ./*.c ./test3 

#实际用例2：test2目录移动到用户目录下，并且取名为newdir
edu118@ubuntu:~/231211/1218$ cd test3/  #进入test3
#将test2目录移动到用户目录下（~），并且取名为newdir
edu118@ubuntu:~/231211/1218/test3$ mv ./test2/ ~/newdir
edu118@ubuntu:~/231211/1218/test3$ cd ~
edu118@ubuntu:~$ ls
03-uart         FileTransfer            newdir        图片
```

## 作业：

```bash
1.注册一个csdn的账号
2.复习当天所有的实际用例（至少敲2遍）
3.自学一些linux的命令
4.每个同学自己定个目标和计划。
```



## 2.0 ROS基础干货讲解

### 2.1 工作空间和功能包

#### 2.1.1 环境变量

在说环境变量前，给大家做一个演示：

![image-20240614132100223](/../图片/image-20240614132100223.png)

![image-20240614132119389](/../图片/image-20240614132119389.png)

我们可以看到在文件的地址栏输入%systemroot%命令之后，跳转到了一条C盘目录之下。

systemroot就是系统的环境变量之一，那么什么是环境变量呢？我们搜索一下百度百科。

<img src="/../图片/image-20240614132508175.png" alt="image-20240614132508175" style="zoom: 50%;" />

总感觉看了和没看一样。

在我们看来，环境变量就是指明操作系统的重要目录在哪里.

<img src="/../图片/image-20240614133230526.png" alt="image-20240614133230526" style="zoom:50%;" />

​    windows存放的是windows系统，因此也被称为系统目录，假如有程序运行需要从系统目录中读取文件，大家觉得是让该程序去把所有的盘都找一遍找个文件还是直接告诉它在哪效率高呢？

显然，后者效率更高，而且更加优雅。因此systemroot其实本质是在指明系统所在的位置。给它一个高大上的名字就叫做环境变量，有了环境变量后，程序可以通过它立刻找到文件的位置。

环境变量包含systemroot，可当然不止它一个哦。

<img src="/../图片/image-20240614133730064.png" alt="image-20240614133730064" style="zoom: 33%;" />

<img src="/../图片/image-20240614133813600.png" alt="image-20240614133813600" style="zoom:33%;" />

<img src="/../图片/image-20240614134027228.png" alt="image-20240614134027228" style="zoom:33%;" />

这些就是大家自己的环境变量。每个人的变量不一定相同，但是和编程相关的path肯定大家都有 。

按下win+r 

<img src="/../图片/image-20240614134408588.png" alt="image-20240614134408588" style="zoom: 50%;" />

![image-20240614134427826](/../图片/image-20240614134427826.png)

跳出这个界面，但是如果我们换成QQMUSIC 则会报错。

<img src="/../图片/image-20240614134507276.png" alt="image-20240614134507276" style="zoom:50%;" />

![image-20240614134738950](/../图片/image-20240614134738950.png)

这是因为，系统会尝试在Path指明的目录下找到cmd这个文件，找到就运行，否则提示找不到文件。

我们看一下cmd的路径

![image-20240614135210188](/../图片/image-20240614135210188.png)

再查看path环境变量的内容

![image-20240614140214622](/../图片/image-20240614140214622.png)

发现system32就在这个环境变量之下，这意味着系统可以找到CMD程序并运行它，而我们的test不属于它。

接下来我们做一个实验。

![image-20240614140502471](/../图片/image-20240614140502471.png)

复制QQMUSIC这个文件所在的路径到PATh的环境变量中，一定要点击确定去保存一下。这样就可以通过命令去执行QQmusic啦

![image-20240614140731407](/../图片/image-20240614140731407.png)

回到LINUX中，在不使用UI界面的情况下要去打开某个文件，则需要先添加一个环境变量。



#### 2.1.3 Cmakelist.txt的作用

​    在 ROS (Robot Operating System) 中，`CMakeLists.txt` 文件是使用 CMake 构建系统来配置和生成软件包的构建脚本。它定义了如何编译和链接代码，以及如何处理包的依赖关系。

 



### 2.2 lauch文件

#### 2.2.1lauch概述

​    在 ROS (Robot Operating System) 中，launch 文件（通常是 .launch 文件）用于启动和管理多个节点的运行。launch 文件使用 XML 语法编写，并提供一种简便的方法来启动一组节点、设置参数、定义节点之间的依赖关系和通信方式。



































































































# 1.1 程序修改编译

 

小车开机，连接 WIFI，密码：dongguan。NFS 挂载(wheeltec-client 密码：dongguan)：

![img](file:///C:/Users/邵俊武/AppData/Local/Temp/msohtmlclip1/01/clip_image007.gif)sudo mount -t nfs 192.168.0.100:/home/wheeltec/wheeltec_robot /mnt ssh 登录到服务端，并修改服务端系统时间为现在：

sudo date -s "2020-12-30 00:00:00"

这一步是因为树莓派/Nano/TX2/NX/工控机的系统时间在没有连接互联网时， 系统时间可能会混乱。同时我们程序修改是需要编译后才能生效的，而编译规则是只编译最新时间的修改，同时修改时间在未来即大于当前系统时间的不编译。

上一次修改时间>此次修改时间：不编译此次修改时间>当前系统时间：不编译

![img](file:///C:/Users/邵俊武/AppData/Local/Temp/msohtmlclip1/01/clip_image008.gif)修改程序

![img](file:///C:/Users/邵俊武/AppData/Local/Temp/msohtmlclip1/01/clip_image009.gif)编译使程序修改生效(.c、.cpp、.h 文件需要编译，如果修改的是.py、.launch、.yaml、.urdf 等文件则不需要编译)：

cd /home/wheeltec/wheeltec_robot (打开工程所在路径) catkin_make (编译)

多线程编译：catkin_make -j2 -l2

-j2，j 是 job 的意思，代表允许 2 个编译命令同时进行，一般是以 CPU

的核心数目的两倍为宜

-l2，l 是 load-average 的意思，代表系统加载的任务数，数目一般与-j 的数目保持一致。

指定编译编译单个功能包：

catkin_make -DCATKIN_WHITELIST_PACKAGES="功能包名"

解除指定功能包编译：

catkin_make -DCATKIN_WHITELIST_PACKAGES=""

![img](file:///C:/Users/邵俊武/AppData/Local/Temp/msohtmlclip1/01/clip_image005.gif)重要功能：

中文界面：Tools->Install Package Control，

Preference->Package Control->Package Control: Install Package，搜索“ChineseLocalizations”，点击，等待安装完成。

切换语言：Help->Language

记住文件格式对应打开方式：右下角->Open all with current extension as...

界面分栏：View->Layout，Alt+Shift+(数字) 全局搜索：Find->Find in Files...，Ctrl+Shift+F 主题风格：Preference->Color Scheme...

Preference->Color Theme

多字符选中同时修改：Ctrl+D

快速跳转函数定义：Ctrl+P，输入：函数所在文件关键词@函数关键词(输入函数关键词后可以通过方向键选择函数文件)

快速跳转函数/变量定义：将鼠标悬停在符号上，就可以以跳转到其定义的文件。

自定义按键绑定：Preference->Key Bindings

![img](file:///C:/Users/邵俊武/AppData/Local/Temp/msohtmlclip1/01/clip_image011.gif)常规快捷键： Ctrl+Z：撤销修改Ctrl+Y：恢复修改Ctrl+F：查找关键字Ctrl+Shift+K：删除整行Ctrl+/：注释单行Ctrl+Shift+/：注释多行Tab ：向右缩进Shift+Tab：向左缩进

Ctrl+M：光标移动至括号内结束或开始的位置官方下载链接：http://www.sublimetext.cn/3

官方中文文档：http://www.sublimetext.cn/support



# 1.2 查看里程计和IMU

IMU 一般指的是陀螺仪，



列出当前小车的所有话题

```c
roslaunch turn_on_wheeltec_robot turn_on_wheeltec_robot.launch
```



查看当前存在话题

```C
rostopic list
```



# 1.2 STM32

## 1.2.1USB一键下载

1.打开FLYMCU软件

(需要安装CH9102驱动)

2.连接单片机、电脑

XYD_ROS资料\1.Mini ROS小车附送资料\6.STM32运动底盘源码\适配STM32控制板_D版_2022.05.17-现在\Mini小车_D版STM32源码_2023.04.21(默认GMR编码器)\OBJ

3.设置串口、波特率、DTR低电平复位、RTS高电平进BL

4.选择HEX文件，开始下载

## 1.2.2硬件原理图讲解

XYD_ROS资料\1.Mini ROS小车附送资料\7.原理图\原理图和资源分配表_D版

![image-20240529232510842](C:\Users\邵俊武\AppData\Roaming\Typora\typora-user-images\image-20240529232510842.png)

 看时间决定是否分析原理图 

### 1.2.3源码讲解



**主函数**

![image-20240531000448648](C:\Users\邵俊武\AppData\Roaming\Typora\typora-user-images\image-20240531000448648.png)

![image-20240531000609169](C:\Users\邵俊武\AppData\Roaming\Typora\typora-user-images\image-20240531000609169.png)



#### FREERTOS

为什么要用FREERTOS实时操作系统？

可以创建多个任务让它们同时执行，并设置优先级。使用中断也可以实现并行，但是如何中断太多管理起来很复杂，使用FREERTOS可以很方便的管理。

###### 任务

1 控制小车Balence_Task 运动控制

2 MPU9250 陀螺仪读取数据任务

3 show 显示任务

4 led灯闪烁的任务

5 手柄控制任务 

6 串口发送数据任务 （串口3 串口1 CAN）



###### 	PID

```C
//此任务以100Hz的频率运行（10ms控制一次）
vTaskDelayUntil(&lastWakeTime,F2T(RATE_100_HZ));
 
//3000*10 = 30000ms = 30s 
if(Time_count<3000) Time_count++;
//Time_count的作用 串口1和串口3做了判断，前十秒接收到数据不处理
```

 usartx.c

在串口1 2 3中都会看到这样一个判断，即小于10s中不处理，直接退出。

```c
if(Time_count<CONTROL_DELAY)
// Data is not processed until 10 seconds after startup
//开机10秒前不处理数据
 return 0;	
```

接下来则是获取编码器数据，速度与转速成正比

```C
Get_Velocity_Form_Encoder();  
//获取编码器数据，即车轮实时速度，并转换位国际单位
```

 以4.3麦伦举例来看

![image-20240603211938249](C:\Users\邵俊武\AppData\Roaming\Typora\typora-user-images\image-20240603211938249.png)

根据对称来看，左边的轮子转动的方向应当和右边的小车相反。在下图的代码中可以看到AD是正向的 BC是负向的。

```C
case Mec_Car:  Set_Pwm( MOTOR_A.Motor_Pwm, -MOTOR_B.Motor_Pwm, -MOTOR_C.Motor_Pwm, MOTOR_D.Motor_Pwm, 0  );
```

为什么需要更新陀螺仪？小车运行一段时间 漂移累计 ，按下按键更新陀螺仪零点。

