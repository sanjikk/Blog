---
title:  "Introduction of Docker"
header:
  teaser: "docker-400x250.jpg"
categories: 
  - Docker
tags:
  - docker
author_profile: false
sidebar:
  - title: "Docker"
    image: docker-400x250.jpg
    image_alt: "docker"
    text: "Docker - Build, Ship, Run"
---
---

{% include toc title="Introduction of Docker" %}


## 1. Brief Introduction
因为公司最近想用Docker来封装在线回测和实盘模拟模块，所以抽空简单研究了一下。

Docker是一套轻量级操作系统虚拟化解决方案，它由go语言编写。它基于Linux容器技术（LXC），Namespace，Cgroup，UnionFS（联合文件系统）等技术。Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）。几乎没有性能开销,可以很容易地在机器和数据中心中运行。最重要的是,他们不依赖于任何语言、框架包括系统。

![image-center]({{ site.url }}{{ site.baseurl }}/images/docker-life-time.jpeg){: .align-center}

Docker的生命周期包含三个部分，镜像，容器，仓库，我们可以把镜像，容器想像成java的类和对象，即容器是由镜像实例化而来的。Docker运行的步骤大致如下：

  1. 编译镜像，放入仓库  -> Build
  2. 从仓库中拉取镜像到本地  -> Ship
  3. 运行镜像，成为容器   -> Run

## 2. 镜像Image
![image-center]({{ site.url }}{{ site.baseurl }}/images/docker-image-layer.jpg){: .align-center}

Docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统就是上文说到的UnionFS。在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。Docker在bootfs之上的一层是rootfs（根文件系统）。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。

## 3. 容器Container
将镜像实例化成一个容器，有点像java中new出来的对象。同一个镜像可以生成多个容器独立运行，互不干扰。

## 4. 仓库Registry
存储和共享镜像文件的地方。

[hub.docker.com](http://hub.docker.com)

[c.163.com](http://c.163.com)

## 5. 安装Installation

### Windows

  1. 下载[Docker Community Edition for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)
  2. 运行`InstallDocker.msi`进行安装
  3. 安装完成后，Docker会自动运行，查看任务栏中是否存在Docker图标![docker-windows]({{ site.url }}{{ site.baseurl }}/images/whale-x-win.png)
  
### Mac OS

  1. 下载[Docker Community Edition for Mac](https://store.docker.com/editions/community/docker-ce-desktop-mac?tab=description)
  2. 运行`Docker.dmg`安装
  3. 安装完成后，查看任务栏![docker-mac]({{ site.url }}{{ site.baseurl }}/images/whale-in-menu-bar.png)

### Linux

  * Requirement: 64-bit OS & Kernel above version 3.10
  * For RedHat & CentOS，参考刘老师的文章[在centos和redhat上安装docker](http://www.imooc.com/article/16448)
  * For Ubuntu:
    1. 打开terminal，使用root权限，su
    2. 
    ```
       curl -s https://get.docker.com|sh 或者
       apt-get install -y docker.io
    ```
    3. 启动服务。
    ```
    service docker start
    ```

## 6. 验证安装
  打开Terminal
  ```
  #check version
  docker version
  #run hello-world
  docker run hello-world
  ```