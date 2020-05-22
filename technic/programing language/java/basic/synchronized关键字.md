# synchronized 关键字

`synchronized` 意味同步



## synchronized method

被 `synchronized` 修饰的 `method` 在该对象中同时只能执行一次，即时是并发，也会一次一次的执行。



## synchronized static method

同上，只不过范围到类外了。因为是static 方法



## synchronized( object ){ … }

执行某段代码块时候，锁住某个对象。

即，当执行`synchronized`修饰的这部分`{...}` 代码块时候，对象 `object` 会被锁住，即对`object` 的访问不管是写入还是读取都会被暂时锁住。



## synchronized的问题

synchronized只有两种情况下才会撤锁

+ 程序执行出错，jvm自动撤锁
+ 程序执行完毕

这样的情况下，万一遇到线程阻塞了，那它就一直阻塞了...