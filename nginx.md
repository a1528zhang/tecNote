# **Nginx**

---

nginx 安装问题 ：使用brew在Mac上安装的时候，如果运行时报log文件不存在，是因为brew没有权限对某些文件夹做写操作的权限导致不能建立log文件，用brew doctor命令可以看到问题，修改过权限之后就可以了

路径
* 默认安装路径 ：/usr/local/etc/nginx/
* 日志 ：/var/log/nginx/ 
* 进程文件 ：/var/run/nginx.pid
命令
* nginx -t : 检查nginx.conf文件是否有语法错误，同时返回nginx.conf文件路径
配置
* worker_processes ：worker角色的工作进程的个数
* sendfile on ：开启高效文件传输模式
* server : 虚拟主机配置
    * location  / ：匹配所有的请求
        * root ：静态资源地址，可以将访问通向静态资源
        * rewrite ：重定向到新的地址
        * permanent ：返回301永久重定向，地址栏会显示跳转后的地址
        * proxy_pass ：反向代理地址