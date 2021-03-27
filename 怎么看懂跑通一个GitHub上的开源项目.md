# 怎么看懂跑通一个GitHub上的开源项目

1. 了解项目是干什么的，有没有兴趣学习，可能用到的知识点和技术栈对你求职有没有帮助
   * Readme文档中会提到技术点
2.  怎么把项目跑起来，这样能够激发学习兴趣
   * IDEA工具的使用
3. 阅读项目源码并且进行调试
   * 结合某个运行起来的功能，从功能入手
   * 功能细化到组件
   * 通过控制台报错、日志、打印变量来查看逻辑
4. 改开源项目的东西，加自己的功能模块

******

Spring 最初利用“工厂模式”（DI）和“代理模式”（AOP）解耦应用组件。大家觉得挺好用，于是按照这种模式搞了一个 MVC框架（一些用Spring 解耦的组件），用开发 web 应用（ SpringMVC ）。然后发现每次开发都写很多样板代码，为了简化工作流程，于是开发出了一些“懒人整合包”（starter），这套就是 Spring Boot。

### 怎么阅读源码（以Halo为例子）

* spring boot项目的入口在src->main->java->Application
* src->main->resources->application.yaml配置文件，配置端口等信息，其余几个yaml文件也是
* resource存放静态资源templates存放前端模板
* 从controller文件夹开始看，controller是前端页面和后端程序交互的入口
* 再看service，service给controller提供service
* repository，跟数据库操作相关的接口
* model是数据库得到的数据对象

