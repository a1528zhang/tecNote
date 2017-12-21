## React Native

------

**错误**：
- ":CFBundleIdentifier", Does Not Exist 这次碰到的是第三方依赖没有正确安装问题，需要运行一遍检查命令 https://github.com/facebook/react-native/issues/14423
- error TS2304: Cannot find name 'PropertyKey’.  原因是ts的编译范围将js也算进去了，移除tsconfig的files和include 配置就好，使用默认配置的话ts会只读取ts、tsx文件的
- error TS2300: Duplicate identifier 'require’. 错误日志中同时是node和rn报错，可能是这两个的@types的包中的定义冲突, 解决原因：安装了多余的@types/node模块，移除了就行

**运行**：
- ```yarn global add react-native-cli```安装cli
- ```react-native init AwesomeProject```初始化项目
- ```cd AwesomeProject & react-native run-ios```运行
- [热更新说明](http://blog.lovezhouting.com/2017/09/03/expo/)
配置好热更新后先运行yarn start，再新开terminal运行react-native run-ios

**代码**：
- AsyncStorage.setItem()方法存入的数据是持久化的，关机后也不会删除