# 关于组件化的思考和总结

#### 1.主要解决本地业务组件之间的通信问题

组件化主要还是解决本地业务组件间的调用，至于跨App或者Hybrid页面通过openUrl方式调用页面和服务的方式其实是可以拆分成两个步骤的问题：

特定模块解析处理＋中间件调用。跨App通过info.plist配置的scheme跳转进入，hybrid页面通过JSBridge框架跳转进入，这部分都有特定的模块去解析完成。

在特定的模块中是否要调用其它业务组件的页面或者服务由特定模块自行决定，这不是组件化中间件要去完成的事情。

#### 2.从工程代码层面来说，组件化就是通过中间件解决组件间头文件直接引用、依赖混乱的问题；

从实际开发来说，组件之间最大的需求就是页面跳转，需要从组件A的pageA1页面跳转到组件B的pageB1页面，避免对组件B页面ViewController头文件的直接依赖。

这里我们希望通过RAC的双向绑定来实现。

#### 3.纯中间件只负责挂接节点的通信问题，不应涉及挂接点具体业务的任何逻辑。

中间件如果涉及到具体的业务逻辑，势必造成中间件对业务模块的直接依赖，所以中间件只需要抽象出业务通信的基本职责，规定好接口，完成调度功能即可。

而每个挂接节点（这里指业务组件）绑定中间件的接口完成挂接工作。

#### 4.中间件是否应该解决组件对外披露服务接口信息？

中间件解决了组件间的通信解藕问题，势必会将组件对外提供调用的信息隐藏起来，不然就不能达到解藕通信的目标。

所以组件对外应当是绝对密封的。

参考自：[iOS组件化思路－大神博客研读和思考](http://www.jianshu.com/p/afb9b52143d4)


