# Javascript 再学习

由于工作中也渐渐开始接触一些前端需求的功能。但是自身本身是专注于后台开发的。对于前端也不是很熟。但觉得自己前端开发效率很低，特此再开一次javascript学习计划

先从基本数据开始吧。感觉还是有点模糊：



## Undefined

Undefined类型只有一个值，即特殊的undefined。

在使用var 声明变量但未对其加以初始化时，这个变量的值就是undefined

```javascript
var message;
alert(message == undefined); //true
```



## Null

Null类型的值也只有一个值，即特殊的null

从逻辑角度上看null值表示空指针。

Null则是为object类型准备的而,undefined则是对于“所有”类型而准备的

当要声明一个变量为object的时候最好初始化为null

```javascript
var car = null;
alert(typeof car); //"object"
```

>undefined其实派生与null
>
>ECMA-262规定它们要相等性测试返回true
>
>```javascript
>alert(null == undefined ); //true
>```
>
>



## Boolean

Boolean只有true和false两种类型，不过注意true和false区分大小写的。只有**true**和**false**才是Boolean类型，True和False都不是。

虽然只有true和false，但ECMAScript 总所有类型的值都要有与这两个boolean 值等价的值。可以调用转型函数Boolean()

```javascript
var str = "hello!";
var strAsBoolean = Boolean(str);
alert(strAsBoolean); //true
```

至于转换类型的取决于下表

| 数据类型      | 转换为true的值      | 转换为false的值 |
| --------- | -------------- | ---------- |
| Boolean   | true           | false      |
| String    | 任何非空子串         | ""         |
| Number    | 任何非零数字值（包括无穷大） | 0和NaN      |
| Object    | 任何对象           | null       |
| Undefined | n/a(不适用)       | undefined  |

在if中自动执行相应的转换类型

```javascript
var message = "hello";
if(message){ //自动执行Boolean(message)
    alert(message);
}// "hello"
```



## Number

Number较为复杂，既有整形也有浮点型，除了十进制外还可以通过八进制、十六进制来表示

八进制字面值第一位必须是**0**，然后就是八进制数字序列（0~7），若后面数字超出了八进制范围则当十进制处理

```javascript
var num1 = 070; //有效，解析为56
var num2 = 079; //无效，解析为79
var num3 = 08; //无效，解析为8
```

十六进制字面值前两位必须是**0x**，后面跟任何十六进制的数字（0~9,A~F）。其中不区分大小写

```javascript
var num1 = 0x1Ae; //有效，解析为430
```

> 在进行计算的时候，八进制和十六进制最终都会被转化为十进制进行计算



+ 浮点数值

  小数点前面可以没有整数，但不推荐！

  ```javascript
  var num1 = 1.1;
  var num2 = .1; //有效，被解析为0.1，但不推荐
  ```

  因为保存浮点值需要两倍的内存空间，所以ECMAScript则会优先使用整形来储存能代表整形的浮点数。比如：

  ```javascript
  var num1 = 1.; //被解析为整形1
  var num2 = 10.0; //被解析为整形10
  ```

  对于超大或者超小的数值，可以用带e的科学计数法表示的浮点数值表示,e为10的幂

  ```javascript
  var num1 = 3.124e7; //被解析为31240000
  var num2 = 3e-7; //被解析为0.0000003
  ```

  浮点值最高进度为17位小数。但由于计算机自身二进制限制问题，本身储存非5结尾的小数点数值是有误差的。例如0.1+0.2的结果不是0.3而是0.30000000000000004

  ```javascript
  //由于计算机二进制精度问题，非5结尾的浮点数计算是不准确的
  var a = 0.1;
  var b = 0.2;
  if(a + b == 0.3){ //千万不能这么去比较，除非为0.25+0.05或者0.15+0.15
      alert('You got 0.3');
  }
  //常规情况下哪怕是以5为结尾的数值，永远不要去测试浮点数值
  ```

  ​

+ 数值范围

  Number.MAX_VALUE(最大值) -- 一般浏览器中为1.7976931348623157e+308

  Number.MIN_VALUE(最小值) -- 一般浏览器中为5e-24