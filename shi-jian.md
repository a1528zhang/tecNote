## 搭建一个nodejs服务器镜像

用于声网的视频录制功能，启动一个nodejs服务器运行录制api，但是每次在服务器安装环境太麻烦，使用docker将这个nodejs做成镜像，到服务器运行就好。

#### 使用node镜像

首先下载并安装好docker，安装傻瓜式就不说了

选择官方docker store提供的node镜像作为基础
`docker pull node`

之后新建一个DockerFile文件，内容如下:

`FROM node:8.9.3  // 使用8.9.3的node镜像`
