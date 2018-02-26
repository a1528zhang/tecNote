# **node.js**

---


**首先，nodejs 是一个js的运行环境，由于正常的js是的运行环境是由浏览器提供的，后端没有浏览器，所以要运行js就要一个编译器，内核是v8，跟Chrome一样**

**[nodemon](https://nodemon.io/)**:
用于监听启动的服务器，被监听的文件改变时就可以重启服务器，用于热启动，[简单中文教程](http://bubkoo.com/2014/12/02/use-nodemon-with-node-applications/);

**typescript**:
[node与ts整合的简单教程](https://segmentfault.com/a/1190000007574276)

**[Express](http://expressjs.com/)**：
一个nodejs的web框架[参考教程](http://javascript.ruanyifeng.com/nodejs/express.html#toc12)

**变量**
- __dirname: node的全局变量，结果与path.dirname(__filename)方法相同，path.dirname(path)方法返回path参数的绝对路径，__filename返回当前文件的路径（包括文件名）

**问题日志**：
- PanResponder优先于onPress事件，两者冲突，不能同时触发