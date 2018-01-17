## 搭建一个nodejs服务器镜像

用于声网的视频录制功能，启动一个nodejs服务器运行录制api，但是每次在服务器安装环境太麻烦，使用docker将这个nodejs做成镜像，到服务器运行就好。

#### 使用node镜像

首先下载并安装好docker，安装傻瓜式就不说了

选择官方docker store提供的node镜像作为基础
`docker pull node`

#### DockerFile
之后新建一个DockerFile文件，内容如下:

`FROM node:8.9.3  // 使用8.9.3的node镜像`

我们需要将项目放入镜像中运行，这里使用挂载文件的方式将项目文件挂载进去，如果使用git clone的方式的话，在镜像构建的时候会clone一次代码，但是每次运行容器的时候不会再clone，当换一个环境构建镜像的时候，clone的代码很可能跟最开始就不同了，所以使用外部mount文件的方式

`WORKDIR /root/agoraRecord    // 将当前路径改变`

如果用RUN cd的方式跳转的话，离开这个RUN语句后就会回到上个WORKDIR，因为每次RUN会产生一个新的进程

```
    VOLUME /root/agoraRecord    // 定义一个匿名数据卷，存放项目文件
    VOLUME /root/recordMedia    // 定义一个匿名数据卷，存放录制文件
```

不用也可以，但是使用了可以防止程序在调用这个地址时找不到，预先定义，之后要在命令中挂载数据卷


