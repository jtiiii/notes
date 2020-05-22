# Spring-整体架构

文章部分内容来源：https://blog.csdn.net/benhuo931115/article/details/74611464

先上图：

![](images/img1.png)

Spring 大致有20个模块，后续还会增多。（比如现在还多了一个Spring-boot）

这些模块被总结为以下几个部分：

- Core Container

  Core Container(核心容器)包含有Core、Beans、Context和Expression Language模块 
  Core和Beans模块是框架的基础部分，提供IoC(转控制)和依赖注入特性。这里的基础概念是BeanFactory，它提供对Factory模式的经典实现来消除对程序性单例模式的需要，并真正地允许你从程序逻辑中分离出依赖关系和配置

  - Core模块主要包含Spring框架基本的核心工具类
  - Beans模块是所有应用都要用到的，它包含访问配置文件、创建和管理bean以及进行Inversion of Control/Dependency Injection(Ioc/DI)操作相关的所有类
  - Context模块构建于Core和Beans模块基础之上，提供了一种类似于JNDI注册器的框架式的对象访问方法。Context模块继承了Beans的特性，为Spring核心提供了大量扩展，添加了对国际化(如资源绑定)、事件传播、资源加载和对Context的透明创建的支持。ApplicationContext接口是Context模块的关键
  - Expression Language模块提供了一个强大的表达式语言用于在运行时查询和操纵对象，该语言支持设置/获取属性的值，属性的分配，方法的调用，访问数组上下文、容器和索引器、逻辑和算术运算符、命名变量以及从Spring的IoC容器中根据名称检索对象

- Data Access/Integration

  - JDBC模块提供了一个JDBC抽象层，它可以消除冗长的JDBC编码和解析数据库厂商特有的错误代码，这个模块包含了Spring对JDBC数据访问进行封装的所有类
  - ORM模块为流行的对象-关系映射API，如JPA、JDO、Hibernate、iBatis等，提供了一个交互层，利用ORM封装包，可以混合使用所有Spring提供的特性进行O/R映射，如前边提到的简单声明性事务管理

- Web

  Web上下文模块建立在应用程序上下文模块之上，为基于Web的应用程序提供了上下文，所以Spring框架支持与Jakarta Struts的集成。Web模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。Web层包含了Web、Web-Servlet、Web-Struts和Web、Porlet模块

  - Web模块：提供了基础的面向Web的集成特性，例如，多文件上传、使用Servlet listeners初始化IoC容器以及一个面向Web的应用上下文，它还包含了Spring远程支持中Web的相关部分
  - Web-Servlet模块web.servlet.jar：该模块包含Spring的model-view-controller(MVC)实现，Spring的MVC框架使得模型范围内的代码和web forms之间能够清楚地分离开来，并与Spring框架的其他特性基础在一起
  - Web-Struts模块：该模块提供了对Struts的支持，使得类在Spring应用中能够与一个典型的Struts Web层集成在一起
  - Web-Porlet模块：提供了用于Portlet环境和Web-Servlet模块的MVC的实现

- AOP

  AOP模块提供了一个符合AOP联盟标准的面向切面编程的实现，它让你可以定义例如方法拦截器和切点，从而将逻辑代码分开，降低它们之间的耦合性，利用source-level的元数据功能，还可以将各种行为信息合并到你的代码中

  Spring AOP模块为基于Spring的应用程序中的对象提供了事务管理服务，通过使用Spring AOP，不用依赖EJB组件，就可以将声明性事务管理集成到应用程序中

- Test

  Test模块支持使用Junit和TestNG对Spring组件进行测试