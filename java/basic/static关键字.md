# static 关键字

`static` 意味着静态，共享。

> PS：如果是我设计这个特性的话，我肯定选用share作为关键字感觉更符合其意义

如何理解这个共享这个概念呢？当每个对象都必须要有的某个**「相同的」**属性时候，如果有个能够一起**「共用」**那个属性的话就能够节省必要的开支。

在程序中，能共用的东西，就用 `static` 关键字可以有效的来节省资源开销。

如何判断这个**「共享」**的**「范围」**才是核心需要关注的问题

```shell
#先要了解各自的范围，再来思考共享的范围
jvm
  |- class
    |- field
    |- method
# jvm 包含着 class
# class 包含着 field 和 method
```





## static class

**class级别的共享，那只有内部类了**

`static` 能修饰的 `class` 只能是 `inner class` （内部类）。因为顶级 `class` 可以直接被 `import` 关键字引用，因此如果也使用 `static` 就有点多此一举了。

一般内部类是无法暴露在父类外的，例如无法被外部类进行 `new` 创建对象

E.g.

```java
public class Other{
  public static void main(String[] args){
    //这条语句会编译不通过报错
    Parent.Son s = new Parent.Son();
  }
}

class Parent{
  class Son{    
  }
}
```

加了 `static` 修饰的内部类才可以使用`new` 关键字

> **当外部类需要使用内部类，而内部类无需外部类资源，并且内部类可以单独创建的时候**
>
> **1.如果类的构造器或静态工厂中有多个参数，设计这样类时，最好使用Builder模式，特别是当大多数参数都是可选的时候。**
>
> **2.如果现在不能确定参数的个数，最好一开始就使用构建器即Builder模式。**
>
> ```java
> public class Outer {
>     private String name;
>     private int age;
> 
>     public static class Builder {
>         private String name;
>         private int age;
> 
>         public Builder(int age) {
>             this.age = age;
>         }
> 
>         public Builder withName(String name) {
>             this.name = name;
>             return this;
>         }
> 
>         public Builder withAge(int age) {
>             this.age = age;
>             return this;
>         }
> 
>         public Outer build() {
>             return new Outer(this);
>         }
>     }
> 
>     private Outer(Builder b) {
>         this.age = b.age;
>         this.name = b.name;
>     }
> }
> 
> /* ------------------ 
> 	使用 Builder来构造外部类对象
> */
> public Outer getOuter()
> {
>     Outer outer = new Outer.Builder(2).withName("Yang Liu").build();
>     return outer;
> }
> ```
>
> 
>
> ([出处](https://www.cnblogs.com/kungfupanda/p/7239414.html))



## static method

**method级别的共享，是针对class而言的**

被 `static` 修饰的 `method` 是**无需创建该类的对象就可以直接调用的**。



## static field

同上，但静态属性在 类加载的时候同时加载了。所以需要初始赋值。