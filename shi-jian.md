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
    VOLUME /root/agoraRecord    // 定义一个匿名数据卷
    VOLUME /root/recordVideo    // 定义录制文件存放的数据卷
    VOLUME /root/logs    // 日志数据卷
    or
    VOLUME [ "/root/recordMedia", "/root/logs", "/root/agoraRecordSDK", "/root/agoraRecord" ]
```

不用也可以，但是使用了可以防止程序在调用这个地址时找不到，预先定义，之后要在命令中挂载数据卷

`EXPOSE 80    // 将80端口对宿主暴露`

暴露端口之后要在run命令中进行映射才能生效

`CMD ["yarn", "start"]`

CMD是在运行容器之后马上执行的命令，如果用`CMD "yarn start"`的话会被解释成`CMD "sh -c yarn start"`，这样实际是在执行sh文件，当这个文件执行后，程序会马上退出。CMD只有一个，如果在run命令中带有执行语句的话，CMD会被覆盖

#### 构建镜像

`docker build .`

进入DockerFile文件目录后执行，会构建一个匿名的，只有id号的image

#### 运行容器

`docker run -t -i --mount type=bind,src=/Users/az/workspace/agoraRecordTest,dst=/root/agoraRecord -p 80:80 71bb1fa9b38e`

查看[命令行文档](https://docs.docker.com/engine/reference/commandline/run/#options)，-t分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上，-i 则让容器的标准输入保持打开。--mount 挂载一个路径到容器中，-p容器内外端口的映射，最后的乱码是镜像id，由于我们在镜像中使用了CMD，所以最后就不用再加上执行的指令了