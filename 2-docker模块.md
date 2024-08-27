# node

# docker

## 知识讲解

### docker与虚拟机

![image-20230630211000299](image-20230630211000299.png)

#### 区别

- 虚拟机：虚拟机是通过Hypervisor(虚拟机管理系统，常见的有VMWare workstation、VirtualBox)，虚拟出网卡、cpu、内存等虚拟硬件，再在其上建立虚拟机，每个虚拟机是个独立的操作系统，拥有自己的系统内核。

- 容器：容器是利用namespace将文件系统、进程、网络、设备等资源进行隔离，利用cgroup对权限、cpu资源进行限制，最终让容器之间互不影响，容器无法影响宿主机。

#### docker的优势

1. 运行在容器上的docker的程序，直接使用的都是宿主机的硬件资源，因此在cpu、内存、利用率上，Docker将会在效率上具有更大的优势
2. Docker直接利用宿主机的系统内核，避免了虚拟机启动时所需要的系统引导时间和操作系统运行的资源消耗，利用Docker能够在几秒钟之内启动大量的容器，是虚拟机无法办到的。快速启动低资源消耗的优点，使Docker在弹性云平台自动运维系统方面具有很好的应用场景。
3. 容器的启动时间是秒级的，大量节约开发、测试、部署的时间。还有一个非常关键的点，就是Docker能够高效地部署和扩容，Docker容器几乎可以在任意平台上运行，包括虚拟机、物理机、公有云、私有云、个人电脑、服务器等，这种兼容性，可以让用户把一个应用程序从一个平台直接迁移到另外一个平台。
4. 但是，虚拟机的安全性比容器好一些，docker与宿主机共享内核、文件系统等资源，更有可能对其他容器、宿主机造成影响。

### docker基本组成

![image-20220408202608177](项目笔记.assets/image-20220408202608177.png)



![image-20220409103833416](项目笔记.assets/image-20220409103833416-1688130488044-5.png)

### docker运行流程



![image-20220409105709162](项目笔记.assets/image-20220409105709162.png)

### Docker的常用命令

#### 帮助命令

![image-20220409111655571](项目笔记.assets/image-20220409111655571.png)

#### 镜像命令

![image-20220409111953817](项目笔记.assets/image-20220409111953817.png)

![image-20220409112449895](项目笔记.assets/image-20220409112449895.png)

![image-20220409113208618](项目笔记.assets/image-20220409113208618.png)

![image-20220409113301508](项目笔记.assets/image-20220409113301508.png)

![image-20220409113323880](项目笔记.assets/image-20220409113323880.png)

![image-20220409113456722](项目笔记.assets/image-20220409113456722.png)

#### 容器命令

![image-20220409134513194](项目笔记.assets/image-20220409134513194.png)

![image-20220409134725256](项目笔记.assets/image-20220409134725256.png)

![image-20220409134925560](项目笔记.assets/image-20220409134925560.png)

![image-20220409135240720](项目笔记.assets/image-20220409135240720.png)

![image-20220409135312533](项目笔记.assets/image-20220409135312533.png)

#### 常用其他命令

![image-20220409140105230](项目笔记.assets/image-20220409140105230.png)

![image-20220409140526933](项目笔记.assets/image-20220409140526933.png)

![image-20220409140925017](项目笔记.assets/image-20220409140925017.png)

![image-20220409141012453](项目笔记.assets/image-20220409141012453.png)

![image-20220409141430933](项目笔记.assets/image-20220409141430933.png)

![image-20220409141534881](项目笔记.assets/image-20220409141534881.png)

#### 小结

![image-20220409141937423](项目笔记.assets/image-20220409141937423.png)

![image-20220409142005849](项目笔记.assets/image-20220409142005849.png)

![image-20220409142048697](项目笔记.assets/image-20220409142048697.png)

### Docker镜像讲解

#### 镜像是什么

![image-20220409154511526](项目笔记.assets/image-20220409154511526.png)

#### Docker镜像加载原理

![image-20220409154648678](项目笔记.assets/image-20220409154648678.png)

![](项目笔记.assets/image-20220409154802246.png)

![image-20220409155110422](项目笔记.assets/image-20220409155110422.png)

​                                 **黑屏-----通过加载------开机     开机完就可以卸载掉，所以bootfs这一部分是公用的**

​                                 **开机之后，就是rootfs系统，就是Linux，所以启动之后，容器就是一个小的虚拟机容器**

![image-20220409154927054](项目笔记.assets/image-20220409154927054.png)

![image-20220409161503973](项目笔记.assets/image-20220409161503973.png)

#### 分层理解

![image-20220409161730246](项目笔记.assets/image-20220409161730246.png)

![image-20220409161903406](项目笔记.assets/image-20220409161903406.png)

![image-20220409161923256](项目笔记.assets/image-20220409161923256.png)

![image-20220409162110443](项目笔记.assets/image-20220409162110443.png)

![image-20220409162227989](项目笔记.assets/image-20220409162227989.png)

![image-20220409162347863](项目笔记.assets/image-20220409162347863.png)

![image-20220409162558212](项目笔记.assets/image-20220409162558212.png)

### 容器数据卷

#### 什么是容器数据卷

![image-20220409164602538](项目笔记.assets/image-20220409164602538.png)

![image-20220409164529752](项目笔记.assets/image-20220409164529752.png)

​                                                                **总结：是为了容器的持久化和同步操作，容器间也是可以数据共享的**

#### 使用数据卷

![image-20220409165137838](项目笔记.assets/image-20220409165137838.png)

![image-20220409165310407](项目笔记.assets/image-20220409165310407.png)

![image-20220409165436199](项目笔记.assets/image-20220409165436199.png)

![image-20220409165526820](项目笔记.assets/image-20220409165526820.png)

### 初始Dockerfile

![image-20220409192708350](项目笔记.assets/image-20220409192708350.png)

![image-20220409192729050](项目笔记.assets/image-20220409192729050.png)

![image-20220409193228588](项目笔记.assets/image-20220409193228588.png)

![image-20220409193405354](项目笔记.assets/image-20220409193405354.png)

![image-20220409193422151](项目笔记.assets/image-20220409193422151.png)

![image-20220409193554728](项目笔记.assets/image-20220409193554728.png)

### DockerFile

#### DockerFile介绍

![image-20220409195315723](项目笔记.assets/image-20220409195315723.png)

![image-20220409195457545](项目笔记.assets/image-20220409195457545.png)

#### DockerFile构建过程

![image-20220409213511162](项目笔记.assets/image-20220409213511162.png)

![image-20220409213736442](项目笔记.assets/image-20220409213736442.png)

#### DockerFile的指令

![image-20220409214416680](项目笔记.assets/image-20220409214416680.png)

![image-20220409214432088](项目笔记.assets/image-20220409214432088.png)



## 依赖库安装

### /usr/local目录

/usr/local 目录是用来安装第三方软件的目录

所谓第三方软件其实就是用户自己安装的软件，区别于安装系统时自带的软件。

- `/usr`- 由操作系统安装（或提供）的所有系统范围的只读文件
- `/usr/local`- 由本地管理员（通常是自己）安装的系统范围的只读文件。*这就是为什么大多数目录名称都`/usr`在此处重复的原因。*

### abseil

Abseil 是 C++ 代码的开源集合（符合 C++14），旨在增强 C++ 标准库。

#### 安装介绍

https://github.com/abseil/abseil-cpp/blob/master/CMake/README.md

#### install

- 安装包下载

https://github.com/abseil/abseil-cpp/archive/refs/tags/20200225.2.tar.gz

### cmake

CMake 是一个跨平台、开源构建系统生成器

#### 官方文档

https://cmake.org/cmake/help/latest/index.html

#### install

https://github.com/Kitware/CMake/archive/refs/tags/v3.26.4.tar.gz

### protobuf

Protocol Buffers（又名 protobuf）是 Google 的语言中立、平台中立、可扩展的机制，用于序列化结构化数据

#### 安装介绍

需要先在计算机上安装[CMake](http://www.cmake.org/)、 [Git](http://git-scm.com/)和Abseil

https://github.com/protocolbuffers/protobuf/blob/main/cmake/README.md

#### install

https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protobuf-cpp-3.14.0.tar.gz

### grpc

gRPC 是一种现代、开源、高性能的远程过程调用 (RPC) 框架，可以在任何地方运行。gRPC 使客户端和服务器应用程序能够透明地通信，并简化连接系统的构建。

#### 安装介绍

https://github.com/grpc/grpc/blob/master/BUILDING.md#build-from-source

#### install

https://github.com/grpc/grpc/archive/refs/tags/v1.30.0.tar.gz

### qt

#### install

https://download.qt.io/archive/qt/5.12/5.12.9/qt-opensource-linux-x64-5.12.9.run

#### cuteci下载

##### 简介

https://pypi.org/project/cuteci/

CuteCI is a simple tool allowing you to install Qt framework with desired packages in headless mode.



### ldconfig

是一个动态链接库管理命令，其目的为了让动态链接库为系统所共享。

https://www.cnblogs.com/schips/p/10183111.html

## docker  file编写

### DEBIAN_FRONTEND

告知操作系统应该从哪儿获得用户输入。如果设置为"noninteractive"，你就可以直接运行命令，而无需向用户请求输入（所有操作都是非交互式的）。这在运行apt-get命令的时候格外有用，因为它会不停的提示用户进行到了哪步并且需要不断确认。非交互模式会选择默认的选项并以最快的速度完成构建。请确保只在Dockerfile中调用的RUN命令中设置了该选项，而不是使用ENV命令进行全局的设置。因为ENV命令在整个容器运行过程中都会生效，所以当你通过BASH和容器进行交互时，如果进行了全局设置那就会出问题。



## 脚本scripts

### xhost

xhost命令是X服务器的访问控制工具，用来控制哪些X客户端能够在X服务器上显示。

xhost [ + | - ] [ Name ]

"+"表示增加，"-"表示去除

当你从hostA登陆到hostB上运行hostB上的应用程序时，做为应用程序来说，hostA是client，但是对图形来说，是在hostA上显示的，需要使用hostA的Xserver，所以hostA是server。因此在登陆到hostB前，需要在hostA上运行xhost +来使其它用户能够访问hostA的Xserver。

####  示列

xhost + 是使所有用户都能访问Xserver.

xhost + local:root 只有本地的root用户可以访问Xserver

### DISPLAY

在Linux/Unix类操作系统上, DISPLAY用来设置将图形显示到何处. 直接登陆图形界面或者登陆命令行界面后使用startx启动图形, DISPLAY环境变量将自动设置为:0:0, 此时可以打开终端, 输出图形程序的名称(比如xclock)来启动程序, 图形将显示在本地窗口上, 在终端上输入printenv查看当前环境变量, 输出结果中有如下内容:

DISPLAY=:0.0

使用xdpyinfo可以查看到当前显示的更详细的信息.

DISPLAY 环境变量格式如下host:NumA.NumB, host指Xserver所在的主机主机名或者ip地址, 图形将显示在这一机器上, 可以是启动了图形界面的Linux/Unix机器, 也可以是安装了Exceed, X-Deep/32等Windows平台运行的Xserver的Windows机器. 如果Host为空, 则表示Xserver运行于本机, 并且图形程序(Xclient)使用unix socket方式连接到Xserver, 而不是TCP方式. 使用TCP方式连接时, NumA为连接的端口减去6000的值, 如果NumA为0, 则表示连接到6000端口; 使用unix socket方式连接时则表示连接的unix socket的路径, 如果为0, 则表示连接到/tmp/.X11-unix/X0 . NumB则几乎总是0.

# docker的等价比喻

dockerfile 文件------->等价于我们通过图纸先计划好，如何盖房子

docker build -f base.dockerfile  --->等价于盖房子过程

上面指令执行完，生成docker 镜像---->等价于房子盖好了，这个房子就在那个放，你没docker run (没钱)，你就使用不了

docker run ------->启动容器----->等价于我们拿到房子钥匙了

docker exec ----->进入容器，进行操作-------->等价于我们进入房子里面，可以任意使用房间内的所有东西