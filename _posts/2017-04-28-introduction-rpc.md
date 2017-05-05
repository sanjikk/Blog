---
title:  "Introduction of RPC"
header:
  teaser: "rpc-frame.png"
categories: 
  - RPC
tags:
  - RPC
author_profile: true
---

{% include toc title="Introduction of RPC" %}


## 1. 简介 Brief Introduction
RPC全称为Remote Procedure Call，一种进程间通信方式，允许程序调用另一个地址空间，比如共享网络上另一台机器上的过程或函数。在中大型分布式系统架构中，成千上万的服务分布在不同的项目，不同的机器上，为了解决如何快速高效的调用远端服务的问题使得RPC应运而生。这是一种能让我们像调用本地服务一样调用远程服务的方式，使得在提供强大的远程调用能力的同时又不失本地调用的语义间接性。


## 2. 调用分类 Call Types

  * 同步调用 Synchronous call

     客户方等待调用执行完成，返回结果

  * 异步调用 Asynchronous call 

     客户方调用后不等待结果，通过回调通知等方式获取结果，或者根本不关心结果

## 3. 框架结构 Framework

![image-center]({{ site.url }}{{ site.baseurl }}/images/rpc-frame.png){: .align-center}

RPC 服务方通过 RpcServer 导出（export）远程接口方法，而客户方通过 RpcClient 去引入（import）远程接口方法。 客户方像调用本地方法一样去调用远程接口方法，RPC 框架提供接口的代理实现，实际的调用将委托给代理 RpcProxy 。 代理封装调用信息并将调用转交给 RpcInvoker 去实际执行。 在客户端的 RpcInvoker 通过连接器 RpcConnector 去维持与服务端的通道 RpcChannel， 并使用 RpcProtocol 执行协议编码（encode）并将编码后的请求消息通过通道发送给服务方。
RPC 服务端接收器 RpcAcceptor 接收客户端的调用请求，同样使用 RpcProtocol 执行协议解码（decode）。 解码后的调用信息传递给 RpcProcessor 去控制处理调用过程，最后再委托调用给 RpcInvoker 去实际执行并返回调用结果。
{: .notice--info}


更多信息请参考[RPC原理详解](http://www.cnblogs.com/metoy/p/4321311.html)
