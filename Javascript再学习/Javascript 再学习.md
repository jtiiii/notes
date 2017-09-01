# Javascript 再学习

由于工作中也渐渐开始接触一些前端需求的功能。但是自身本身是专注于后台开发的。对于前端也不是很熟。但觉得自己前端开发效率很低，特此再开一次javascript学习计划。主要就是补充自己欠缺的部分知识。并非是完整的

笔记内容摘自泽卡斯（Zakas.NicholasC.）.JavaScript高级程序设计(第3版)(图灵程序设计丛书).人民邮电出版社.Kindle版本.

先从基本数据开始吧。感觉还是有点模糊：



# JavaScript数据类型

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


+ 数值范围

  Number.MAX_VALUE(最大值) -- 一般浏览器中为1.7976931348623157e+308
  Number.MIN_VALUE(最小值) -- 一般浏览器中为5e-24

  如果超出了最大值和最小值，就会成为**Infinity**和**-Infinity**(正无穷和负无穷)。而Infinity是无法被计算的。如果一段计算代码执行过程中得出了Infinity则后续计算会错误。但是可以被判断。使用**isFinite()**函数来判断这个值是否在范围内。

  ```javascript
  var result = Number.MAX_VALUE * 2;
  alert(isFinite(result)); //false
  ```

  > 访问Number.NEGATIVE_INFINITY 和 Number.POSITIVE_INFINITY也可以得到-Infinity和Infinity

+ **NaN**

  NaN，即非数值（Not a Number）。NaN被用来代表没有计算结果的值（比如10/0这样计算），这样在计算的时候不会爆出错误了，继续执行下面的代码。

  任何涉及NaN的操作都会返回NaN。NaN与任何值都不相等，包括NaN本身，针对这个特点，ECMAScript 定义了isNaN()函数：**所有不能转化为数值的数被返回为true**

  ```javascript
  var a = 1;
  var b = a / 0;
  alert(b); //NaN
  alert(a == NaN); //false
  alert(b == NaN); //false
  alert(isNaN(a)); //false
  alert(isNan("10")); //false
  alert(isNaN(b)); //true
  alert(isNaN("test")); //true
  ```

  > isNaN()也适用于对象，会首先调用对象的valueOf()方法进行判断，如果返回true，在调用toString()方法进行判断。
  >
  > 对于对象操作的isNaN()可以解释成如下：
  >
  > ```javascript
  > function isNaN(object){
  >     if(isNaN(object.valueOf())){
  >       return isNaN(object.toString());
  >     }
  >   return false;
  > }
  > ```

+ 数值转换

  数值转换有3个函数：Number()、parseInt()和parseFloat()

  Number() 可以用于任何数据

  parseInt()和parseFloat()则是专门用于把字符换成数值

  > **Number()转换规则如下**
  >
  > ```javascript
  > //Boolean 转化为 1 和 0
  > Number(true); //1
  > Number(false); //0
  > //null 转为 0
  > Number(null); //0
  > //往后不能转化为数字的字符串和undefined 转化为 NaN
  > Number(undefined); //NaN
  > Number(10); //10
  > Number("10"); //10
  > Number("010"); //10
  > Number("10A"); //NaN
  > //转换支持八进制十六进制
  > Number(070); //56
  > Number(0xf); //15
  > //空 返回0
  > Number(); //0
  > ```
  >
  > 如果转化的是对象，则调用valueOf的方法，若转化为NaN在调用toString();
  >
  > 可以解释成如下：
  >
  > ```javascript
  > function Number(object){
  >   var result = Number(object.valueOf());
  >   if(isNaN(result){return Number(object.);}
  >   return result;
  > }
  > ```
  >
  > **parseInt()转换规则如下**
  >
  > ```javascript
  > //parseInt()只用于转换字符串为整数
  >
  > //忽略非数字字符后的所有内容
  > parseInt("21sdbs123df"); //21
  > //葫芦也开头空格
  > parseInt("  123"); //123
  > //空为 NaN
  > parseInt(""); //NaN
  > //忽略小数点
  > parseInt("21.2");//21
  >
  > //支持八进制和十六进制
  > parseInt("070"); //56 
  > parseInt("0xA"); //10
  > /*
  > 不过在ECMAScript 5中已经去除了八进制解析能力
  > 主要原因是前导0不再被进制解析使用。
  > 不过可以指定基数来指定解析指定进制,解析失败则返回NaN
  > */
  > parseInt("70",2); //NaN
  > parseInt("10",2); //2
  > parseInt("70",8); //56
  > parseInt("56",10); //56
  > parseInt("a",16); //10
  > //大多数情况下我们要解析的的是10进制，因此为了保证稳定性，第二基数一般是必须的
  > ```
  >
  > **parseFloat()转换规则**
  >
  > parseFloat与parseInt类似。不过相比parseInt，pareseFloat始终会忽略前导0
  >
  > 而且只会解析十进制，但是能解析科学计数法
  >
  > ```javascript
  > parseFloat("22.5"); //22.5
  > parseFloat("1234sdfsd"); //1234
  > //无法解析八进制与十六进制，统一当做十进制处理
  > parseFloat("0xa"); //0
  > //忽略第二个小数点
  > parseFloat("22.5.34"); //22.5
  > //能解析科学计数法
  > parseFloat("3.125e7"); //31250000
  > ```



## String

String类型由多个16位的Unicode字符组成的字符序列，即字符串。

字符可由 （''）（ ""）单引号或者双引号表示：

```javascript
var str1 = "str1";
var str2 = 'str2';
//不过双引号开头的必须以双引号结尾，单引号同理
```

转义序列：

| 字面量    | 含义                       |
| ------ | ------------------------ |
| \n     | 换行                       |
| \t     | 制表                       |
| \b     | 空格                       |
| \r     | 回车                       |
| \f     | 进纸                       |
| \\\    | 代表字符“\”                  |
| \'     | 代表字符“ ' ”                |
| \"     | 代表字符“ " ”                |
| \xnn   | 以十六进制代码nn表示一个字符          |
| \unnnn | 以十六进制代码nnnn表示一个Unicode字符 |

```javascript
var text = "This is the letter sigm\x61: \u03a3.";
alert(text); //This is the letter sigma: Σ.
//unicode字符长度算1个,length方法并不能返回精确的字节数
alert(text.length); //28
```

ECMAScript中的字符串是不可变的，也就是说，字符串一旦创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新 值的字符串填充该变量。

**toString()**方法

Number，Boolean，Object和String都有toString()方法，但undefined和null没有。

数值调用toString()方法的时候，默认情况下为返回十进制，但是可以设置基数为参数来控制输出二进制，八进制，十六进制，乃至其他任意有效进制格式表示的字符串值。

```javascript
var num = 43;
num.toString(); //"43"
num.toString(2); //"101011"
num.toString(16); //"2b"

var flag = true;
flag.toString();//"true"

```

对于null和undefined而言，在不知道要转换的值是不是null或者undefined情况下还是可以使用String()来转型。

String()遵循以下规则：当有toString()方法时候，调用toString()，没有则返回结果。

```javascript
var test = undefined;
String(test); //"undefined"
var test2 = null;
String(test2); //"null"
```

> 要把某个值转化为字符串你也可以使用“+”操作符
>
> ```javascript
> undefined+'|sdf'; //"undefined|sdf"
> null+"";//"null|sdf"
> ```



## Object

ECMAScript中的对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。而创建Object类型的实例并为其添加属性和（或）方法，就可以创建自定义对象。



Object的每个实例都具有下列属性和方法。

+ Constructor：保存着用于创建当前对象的函数。对于前面的例子而言，构造函数（constructor）就是Object()。
+ hasOwnProperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名（propertyName）必须以字符串形式指定（例如：o.hasOwnProperty("name")）。
+ isPrototypeOf(object)：用于检查传入的对象是否是另一个对象的原型。
+ propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用for-in语句（本章后面将会讨论）来枚举。与hasOwnProperty()方法一样，作为参数的属性名必须以字符串形式指定。
+ toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应。
+ toString()：返回对象的字符串表示。valueOf()：返回对象的字符串、数值或布尔值表示。通常与toString()方法的返回值相同。



# 操作符

## +

数值相加

字符串与任意数据相加都为字符串

```javascript
1 + 1 = 2;
1 + "1" = "11";
"test" + undefined; // "test|undefined"
"test" + null; //"test|null"
"test" + 1; //"test1"
"test" + new Date(); //"test|Fri Sep 01 2017 15:50:23 GMT+0800 (中国标准时间)"
```

## -

数值相减

与“+”不同现将所需的计算值调用Number()转型。故转换为NaN的计算结果也为NaN

```javascript
3 - 1 ; //2
"1" - "2b"; //NaN
3 - "1"; //2
3 - undefined; //NaN
```



## ++

自加1，计算结果和“+”相同

```javascript
var test = 1;
test++; //1 先返回test，再自增
alert(test); //2

var test2 = 1;
++test2; //2 先自增再返回test
alert(test2);//2
```



## --

自减一，计算结果和“-”相同，计算结果为数值的时候，计算顺序和“++”相同。

 ```javascript
var test1 = "test";
test--;//NaN
var test2 = "1";
test--; //1
--test; //0
var o = {valueOf:function(){return -1;}};
o--;//-1
--o;//-3
 ```



# Boolean操作符

boolean操作符使用的时候都会调用Boolean()方法

## &&（AND）

略

```javascript
//undefined
true && undefined; //undefined
false && undefined; //false
undefined && undefined; //undefined
//null
true && null; //null
false && null; //false
null && null; //null
//NaN
true && NaN; //NaN
false && NaN; //false
NaN && NaN; //NaN
```



## ||（OR）

略

```javascript
//undefined
undefined || true; //true
undefined || false; //undefined
undefined || undefined; //undefined
//null
true || null; //true
false || null;//null
null || null; //null
//NaN
true || NaN; //true
false || NaN; //NaN
NaN || NaN;//NaN
```



## !（NOT）

略

```javascript
!undefined; //true
!null; //true
!NaN; //true

```

