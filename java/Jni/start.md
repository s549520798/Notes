JNI 简介
JNI 是 java native interface 的简称， 它允许在java虚拟机VM中运行的java代码和其他编程语言（C、C++和汇编）编写的应用程序和库进行互操作。

什么时候会用到JNI?
* 标准java库无法满足应用程序所需的依赖于平台的功能
* 已经有用另一种语言编写的库，并希望通过JNI代码来访问它
* 使用如汇编之类的较低级代码来实现一小部分对事件要求严格的代码

JNI能干什么？
* 创建，检查，更新java对象
* 调用java方法
* 捕获并抛出异常
* 加载类并获取类信息
* 执行运行时类型检查

