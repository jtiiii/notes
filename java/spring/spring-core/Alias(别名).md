# Alias

Spring 中的Alias是一个非常重要的功能。

`Bean`有自己的唯一`id`外，还可以有`name`属性来进行使用别的名称，但是`name`是可以多个`Bean`重复的。

假如我想要该bean能拥有多个唯一id怎么办，这时候就是alias所要解决的情况。

比如：我`A应用`获取的数据源bean的id是 `dataSource-A`，`B应用`获取的数据源bean的id是`dataSource-B`..

但是我想`A应用`和`B应用`一起使用一个id为`dataSouce`的数据源bean。这时候我可以使用alias给id为`dataSouce`的bean起多个别名：

```xml
<!-- 数据源bean -->
<bean id="dataSource" class=".." />
<!-- 给dataSource的bean增加别名 -->
<alias name= "dataSource" alias="dataSource-A,dataSource-B" />
```

Java中也可以使用别名直接获取Bean

```java
DataSource sourceA =  applicationContext.getBean("dataSource-A",DataSource.class);  
```



