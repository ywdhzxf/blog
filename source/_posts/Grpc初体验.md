
---
title: Grpc初体验
date: 2019-05-06 12:36:15
tags: 杂记,GoLang,Python
---


## Grpc初体验
### 前言
因为最近工作涉及到了grpc, 但是不是很了解这个框架, 所以就看了一手 [grpc官方文档](http://doc.oschina.net/grpc?t=56831), 克隆下来代码简单的了解一下

### 概念
定义一个服务， 指定其可以被远程调用的方法及其参数和返回类型。gRPC 默认使用 protocol buffers 作为接口定义语言，来描述服务接口和有效载荷消息结构。允许定义四种服务方法
```
1 单项 RPC，即客户端发送一个请求给服务端，从服务端获取一个应答，就像一次普通的函数调用

2 服务端流式 RPC，即客户端发送一个请求给服务端，可获取一个数据流用来读取一系列消息。客户端从返回的数据流里一直读取直到没有更多消息为止。

3 客户端流式 RPC，即客户端用提供的一个数据流写入并发送一系列消息给服务端。一旦客户端完成消息写入，就等待服务端读取这些消息并返回应答

4 双向流式 RPC，即两边都可以分别通过一个读写数据流来发送一系列消息。这两个数据流操作是相互独立的，所以客户端和服务端能按其希望的任意顺序读写，
```

### 主要使用
gRPC 提供 protocol buffer 编译插件，能够从一个服务定义的 .proto 文件生成客户端和服务端代码。通常 gRPC 用户可以在服务端实现这些API，并从客户端调用它们。

### 测试
#### 服务端
测试使用的话就是按照官方文档的教程来的
```
git clone https://github.com/grpc/grpc.git
```
拉一手代码然后直接进到demo目录就可以, 我主要看了一下 Python和 Go的, 目录 grpc/examples/python/helloworld, 里面的代码都是生成好的, 可以直接使用, 如果有兴趣的也可以按照教程从头开始

在目录里 greeter_server.py 是服务端, 在里面定义了一个Greeter的类, 包括里面的一个 SayHello 方法(接受参数, 返回响应)
```
class Greeter(helloworld_pb2_grpc.GreeterServicer):

    def SayHello(self, request, context):
        return helloworld_pb2.HelloReply(message='Yes, %s!' % request.name)


def serve():
    server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
    helloworld_pb2_grpc.add_GreeterServicer_to_server(Greeter(), server)
    server.add_insecure_port('[::]:50051')
    server.start()
    try:
        while True:
            time.sleep(_ONE_DAY_IN_SECONDS)
    except KeyboardInterrupt:
        server.stop(0)
```

可以看到在server里面首先定义了一个最大处理数为10的线程池, 然后将 Greeter 类作为服务添加, 在添加50051作为服务端口, start启动服务

#### 客户端
```
def run():
    # NOTE(gRPC Python Team): .close() is possible on a channel and should be
    # used in circumstances in which the with statement does not fit the needs
    # of the code.
    a = time.time()
    with grpc.insecure_channel('localhost:50051') as channel:
        stub = helloworld_pb2_grpc.GreeterStub(channel)
        response = stub.SayHello(helloworld_pb2.HelloRequest(name='小飞'))
        print(response)
    print("time = ", time.time()-a)
    print("Greeter client received: " + response.message)
```
客户端就比较简单了, 通过grpc 连上50051端口携带参数发起请求, 再接受服务端返回的详情就ok


### proto文件
gRPC 默认使用 protocol buffers 作为接口定义语言, 所以需要编写 proto文件定义 gRPC接口, 进行编译生成 helloworld_pb2 和helloworld_pb2_grpc文件, 也就是客户端和服务端之间的通信, 里面会定义接口接收参数和返回参数.

    