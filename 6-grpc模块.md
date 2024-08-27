# grpc模块

https://grpc.io/docs/languages/cpp/quickstart/

## rpc

客户端在不知道调用细节的情况下，调用存在于远程计算机上的某个对象，就像调用本地应用程序中的对象一样。

比较正式的描述是：一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。

网络协议和网络IO模型对其透明：既然RPC的客户端认为自己是在调用本地对象。那么传输层使用的是TCP/UDP还是HTTP协议，又或者是一些其他的网络协议它就不需要关心了

![img](6-grpc模块.assets/2992488312e89696f62017acf2cb02f66571cb.webp)

## 什么是grpc

https://github.com/grpc/grpc

- gRPC 是一种现代、开源、高性能的远程过程调用 (RPC) 框架，**基于 HTTP2 协议设计**，可以在任何地方运行。gRPC 使客户端和服务器应用程序能够透明地通信，并简化连接系统的构建。

- 在 gRPC 中，客户端应用程序可以像本地对象一样直接调用不同机器上的服务器应用程序上的方法，从而使您可以更轻松地创建分布式应用程序和服务。与许多 RPC 系统一样，gRPC 基于定义服务的思想，指定可以远程调用的方法及其参数和返回类型。在服务器端，服务器实现这个接口并运行一个gRPC服务器来处理客户端调用。在客户端，客户端有一个存根（在某些语言中简称为客户端），它提供与服务器相同的方法。

![image-20230701094401757](6-grpc模块.assets/image-20230701094401757.png)

- gRPC 客户端和服务器可以在各种环境中运行并相互通信（从 Google 内部的服务器到您自己的桌面），并且可以用 gRPC 支持的任何语言编写。例如，您可以使用 Java 轻松创建 gRPC 服务器，并使用 Go、Python 或 Ruby 编写客户端。此外，最新的 Google API 将具有其接口的 gRPC 版本，让您可以轻松地将 Google 功能构建到您的应用程序中。

## grpc cpp 知识点

https://grpc.io/docs/languages/cpp/quickstart/

### protobuf使用

![img](6-grpc模块.assets/v2-720a4cc3f5e568a79d26454676a59832_720w.webp)

默认情况下，gRPC 使用[Protocol Buffers](https://protobuf.dev/overview)，Google 成熟的开源机制，用于序列化结构化数据（尽管它可以与 JSON 等其他数据格式一起使用）

- 使用协议缓冲区时的第一步是定义要在原始文件*中序列化的数据的结构：这是一个带有`.proto`扩展名的普通文本文件。Protocol buffer 数据被构造为 *消息*，其中每条消息都是一个小的逻辑信息记录，其中包含一系列称为字段的名称-值*对*。这是一个简单的例子：

```proto
message Person {
  string name = 1;
  int32 id = 2;
  bool has_ponycopter = 3;
}
```

然后，一旦指定了数据结构，您就可以使用协议缓冲区编译器`protoc`根据原型定义以您的首选语言生成数据访问类。它们为每个字段提供了简单的访问器，例如`name()`和`set_name()`，以及将整个结构序列化为原始字节或从原始字节解析整个结构的方法。因此，例如，如果您选择的语言是 C++，则在上面的示例上运行编译器将生成一个名为 的类`Person`。然后，您可以在应用程序中使用此类来填充、序列化和检索`Person`协议缓冲区消息。

您可以在普通的 proto 文件中定义 gRPC 服务，并将 RPC 方法参数和返回类型指定为协议缓冲区消息：

```proto
// The greeter service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
```

gRPC 使用`protoc`特殊的 gRPC 插件从原始文件生成代码：您将获得生成的 gRPC 客户端和服务器代码，以及用于填充、序列化和检索消息类型的常规协议缓冲区代码。要了解有关protocol buffers的更多信息，包括如何`protoc`使用您选择的语言安装gRPC插件，请参阅[protocol buffers文档](https://protobuf.dev/overview)

### 简要步骤

从文件中的服务定义开始`.proto`，gRPC 提供了用于生成客户端和服务器端代码的协议缓冲区编译器插件。gRPC 用户通常在客户端调用这些 API，并在服务器端实现相应的 API。

- 在服务器端，服务器实现服务声明的方法并运行 gRPC 服务器来处理客户端调用。gRPC 基础设施解码传入请求、执行服务方法并对服务响应进行编码。
- 在客户端，客户端有一个称为*存根（stub）*的本地对象，它实现与服务相同的方法。然后，客户端可以在本地对象上调用这些方法，并且这些方法将调用的参数包装在适当的协议缓冲区消息类型中，将请求发送到服务器，并返回服务器的协议缓冲区响应。

![img](6-grpc模块.assets/v2-7be92b1dd4b7698529ea9518262aa62e_720w.webp)

## 服务端

### 基本概念

#### ServerBuilder 

https://grpc.github.io/grpc/cpp/classgrpc_1_1_server_builder.html

用于创建和启动grpc::Server实例的构建器类

#### Server

https://grpc.github.io/grpc/cpp/classgrpc_1_1_server.html#details

代表 gRPC 服务器

#### GreeterServiceImpl 

创建服务实现类的实例

#### AddListeningPort

指定我们要用于侦听客户端请求的地址和端口

#### BuildAndStart

调用`BuildAndStart()`构建器为服务创建和启动 gRPC 服务器

### 代码解析

#### constexpr

![img](6-grpc模块.assets/v2-f45de959011fda57a26d5dadbe46a20a_720w.webp)

https://www.cnblogs.com/carpenterlee/p/5994681.html

##### **预处理**

预处理用于将所有的#include头文件以及宏定义替换成其真正的内容，预处理之后得到的仍然是文本文件，但文件体积会大很多

- 删除所有的注释
- 宏扩展
- 文件包含

##### 编译

这里的编译不是指程序从源文件到二进制程序的全部过程，而是指**将经过预处理之后的程序转换成特定汇编代码(assembly code)的过程**

![image-20230701105558042](6-grpc模块.assets/image-20230701105558042.png)

##### 汇编

**汇编过程将上一步的汇编代码转换成机器码(machine code)**，这一步产生的文件叫做**目标文件**，是二进制格式

##### 链接

**链接过程将多个目标文以及所需的库文件(.so等)链接成最终的可执行文件(executable file)**。

##### 作用

constexpr的作用：给编译器足够的信心在编译期去做被constexpr修饰的表达式的优化



## client

基本概念

1. 创建连接到远程服务器的 channel
2. 构建使用该channel的客户端stub
3. 通过stub调用服务方法，执行RPC调用

### Channel

`Channel` 是用于执行 RPC 请求的概念上的端点连接，基于负载和配置

### 认证

https://grpc.io/docs/guides/auth/

gRPC 身份验证概述，包括内置身份验证机制，以及如何插入您自己的身份验证系统

#### 没有加密或身份验证

```
grpc::InsecureChannelCredentials()
```

### grpc::ClientContext

```
// 设置超时时间
grpc::ClientContext context;
gpr_timespec ts;
ts.tv_sec = 10;
ts.tv_nsec = 0;
ts.clock_type = GPR_TIMESPAN;
context.set_deadline(ts);

```

