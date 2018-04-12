# JNDI

JNDI 全拼是 Java Naming and Directory Interface。

直译过来就是Java名称与文件夹的接口，是 J2EE 中最重要规范之一。

虽然仅仅是个规范，但是在这开源的时代中对于开发过程中进行资源设计编写起到了非常重要的作用。能让人快速读懂源码。

文章内容来源：https://www.cnblogs.com/zhchoutai/p/7389089.html



那么JNDI是规范了什么？

JNDI 要求所有 J2EE 容器都有其规范实现。JAVA程序都可以使用JNDI 来调用J2EE 服务器开放的接口服务

下面我们来看一下在数据源的获取使用JNDI和不使用JNDI的区别。



没有使用JNDI的时候，一般使用代码直接获取数据库连接：

```Java
Connection conn=null;  
try {  
  //加载驱动
  Class.forName("com.mysql.jdbc.Driver");  
  //获取数据库连接
  conn=DriverManager.getConnection("jdbc:mysql://ip:port?user=test&password=test");
  
  //执行操作后关闭
  conn.close();  
} catch(Exception e) {  
  e.printStackTrace();  
} finally {  
  if(conn!=null) {  
    try {  
      conn.close();  
    } catch(SQLException e) {}  
  }  
```

使用JNDI之后，

我们可以在J2EE 服务器上配置好数据库，然后使用JNDI规范来调用J2EE 上的数据库连接：

```java
try {  
  Context ctx=new InitialContext();  
  Object datasourceRef=ctx.lookup("java:MyDataBase"); //引用数据源  
  DataSource ds=(Datasource)datasourceRef;  
  conn=ds.getConnection();  
  ......  
  c.close();  
} catch(Exception e) {  
  e.printStackTrace();  
} finally {  
  if(conn!=null) {  
    try {  
      conn.close();  
    } catch(SQLException e) { }  
  }  
```



可以见得，在代码量上，使用JNDI与不使用JNDI其实都差不多。

不过JNDI起到了解耦作用。因为是从J2EE 容器上获取数据源，我们可以在J2EE上修改配置来修改其连接的数据库，而不是在代码层面上修改。

并且我们不需要关心具体的数据库后台是什么，JDBC驱动程序是什么，JDBC URL格式是什么，访问数据库的用户名和口令是什么。

>  还有一种常见的对于数据库连接进行解耦配置的方式就是使用配置文件。
>
> E.g.
>
> datasouce.properties:
>
> ```properties
> mysql.database.url=jdbc:mysql://ip:port/db?useUnicode=true&characterEncoding=UTF-8&useSSL=false
> mysql.database.username=root
> mysql.database.password=root
> ```
>
> 然后从配置文件中读取信息获取连接。也可以起到不修改源代码的情况来修改数据源，但是配置文件还是脱离不了配套程序的范围，不好跨应用或者服务器。
>
> 但是对于J2EE规范，可以让数据源由J2EE 容器来负责处理。JAVA程序只关心使用即可。即数据源全部由J2EE 容器提供，此时JAVA程序可以跨服务，跨应用来访问资源。



当然JNDI对于规范肯定不只有数据库。

JNDI的规范范围是整个J2EE 的资源访问。JNDI 在 J2EE 中的角色就是“交换机” 。在 J2EE 中，JNDI 是把 J2EE 应用程序合在一起的粘合剂，JNDI 提供的间接寻址允许跨企业交付可伸缩的、功能强大且很灵活的应用程序。这是 J2EE 的承诺，而且经过一些计划和预先考虑，这个承诺是完全可以实现的。是J2EE里面的解耦方案。





