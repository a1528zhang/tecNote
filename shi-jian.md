## 搭建一个nodejs服务器镜像

用于声网的视频录制功能，启动一个nodejs服务器运行录制api，但是每次在服务器安装环境太麻烦，使用docker将这个nodejs做成镜像，到服务器运行就好。

#### 使用node镜像

首先下载并安装好docker，安装傻瓜式就不说了

选择官方docker store提供的node镜像作为基础
`docker pull node`

#### DockerFile
之后新建一个DockerFile文件，内容如下:

`FROM node:8.9.3  // 使用8.9.3的node镜像`
我们需要将项目放入镜像中运行，这个node镜像中是有git的，但是如果在镜像中调用git的话会进行写操作，应该尽量避免，这里使用