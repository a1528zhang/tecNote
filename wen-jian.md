# **文件** 

---
    * chmod 775 name : 改变文件访问权限
    * chown [-R] 账号名称 文件或目录
    
    chown [-R] 账号名称:用户组名称 文件或目录：改变用户拥有者，-r是递归选项
    * ls -l : 查看文件权限，分别显示所有者（owner或者user）、所有组（group）和其他人（other）
    * mkdir : 创建文件夹
    * touch : 新建一个不存在的文件
    * grep : 文本搜索
    * find : 文件搜索
    * locate : 结果等于find -name，但是速度快，搜索的是/var/lib/locatedb数据库，这个库里有全部的文件位置信息
    * cat ：连接文件或标准输入并打印，这个命令常用来显示文件内容
    * mv [option] sourceFloder targetFloder: 移动文件, -b 备份后覆盖，-f 强制覆盖，-i 询问是否覆盖，-u 如果source比较新才更新，-t 指定mv的目标目录，用于将多个源文件移动到一个目录
    * rm -rf: rm 是删除命令，-r是循环删除内容，f是强制删除且不提示