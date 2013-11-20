---
layout: post
title: JavaScript学习笔记 - part2
date: 2013-11-120 20:35
comments: true
categories: javascript
---

### 数据类型

Undefined, Null, Boolean, String, Number, Object

### undefined

```javascript
var a;
alert(a); // "undefined"
alert(b); // error

alert(typeof a); // "undefined"
alert(typeof b); // "undefined"
```

### Number

```javascript
var a1 = 070; // 八进制的70等于十进制的56
var a2 = 079; // 无效的八进制，解析为十进制的79
// 进行算数计算时，八进制和十进制都被转换成十进制数值
```
* 默认情况下, 小数点后带有6个0以上的浮点数值转换为科学技术法表示的形式
* 5e-324 < n < 1.79…e+308
* 超出这个范围的负数为 -Infinity, 正数为 Infinity

### NaN

* NaN表示非数值
* NaN参与的操作，都会返回NaN
* isNaN(x)，如果x不能被转换为数值， 返回true，(10, "10", true)都返回false，(NaN, "asdf")返回true
* isNan(x), 如果x是object，则先调用x.valueOf(), 然后根据测试返回值，如果不能，调用x.toString()，测试返回值

### Number(x)

* Boolean true 1, false 0
* 数字 直接返回
* null 0
* undefined NaN
* 字符串, 只包含数字; 包含有效的浮点数; 包含有效的十六进制; 空字符串; 其他的
* 对象 valueOf(), toString()

### parseInt(x, base)

* 忽略空格，然后找到第1个非空格字符，如果不是数字或负号，返回NaN
* 转换数字字符
* 直到遇到非数字字符
* 一般设置base为10
* 会识别八进制，和十六进制, parseInt('070');// 56 in ECMAScript, 70 in ECMAScript

### parseFloat(x)

* 第1个小数点是有效的
* 十六进制字符串会被转换为0
* 会忽略前导的0

### String

* \xnn 以十六进制代码nn表示一个字符
* \unnnn 已十六进制nnnn表示一个字符
* toString(2), toString(10)
* null和undefined没有 toString()方法
* 如果x可能是null或undefined, 可以使用 String(x)，null -> 'null', undefined -> 'undefined'

### 操作符

* 一元操作符，++, --
* 一元加减操作符，+, -
* 位操作符，-18.toString(2); -> -10010

### 位操作符

* 非, ~, ~25 = -26, 操作数的负值 - 1
* 与, &, 25&3 = 1, 11为1,其他为0
* 或, |, 25|3 = 17, 有1为1, 其他为0
* 异或, ^, 25^3 = 26, 不同为1,相同为0
* 左移, <<, 2<<5 = 64, 不影响符号位
* 右移, >>, 64>>5 = 2, 不影响符号位
* 无符号右移, >>>, -64>>>5 = 134217726, 影响符号位
* 没有无符号左移

### 逻辑非

* !x
* !object -> false
* !"" -> true
* !"asdf" -> false
* !0 -> true
* !12 -> false
* !Infinity -> false
* !null -> true
* !NaN -> true
* !undefined -> true
* !!x 会返回x本身对应的布尔值,相当于 Boolean(x)

### 逻辑与

* x && y
* x是对象,返回y
* y是对象,则当x是true是才会返回此对象
* x,y都是对象,返回y
* 有1个是null,返回null
* 有1个是NaN,返回NaN
* 有1个是undefined,返回undefined
* 短路,如果x是false,则不会计算y

### 逻辑或

* x || y
* x是对象,返回x
* x求值结果为false,返回y
* x,y均为对象,返回x
* x,y都是null,返回null
* x,y都是naN,返回NaN
* x,y都是undefined,返回undefined
* 短路,x求值为true,则不会计算y

### 乘法 *

* x * y
* x,y都是数字,按照正常的计算,如果结果超过表示范围,则返回Infinity或-Infinity
* 如果有1个是NaN,返回NaN
* Infinity * 0 = NaN
* Infinity 乘以 非0,结果是Infinity或-Infinity,取决于另一个数的符号
* 如果有1个不是数字,则调用 Number(x),转换为数字

### 除法 /

* x / y
* x,y都是数字,按照正常的计算,如果结果超过表示范围,则返回Infinity或-Infinity
* 如果有1个是NaN,返回NaN
* Infinity / Infinity = NaN
* 0 / 0 = NaN
* 如果非0的有限数被0除,结果为Infinity或-Infinity,取决于那个数的符号
* 如果Infinity被任何非0数除,结果为Infinity或-Infinity,取决于那个数的符号
* 如果有1个不是数字,则调用 Number(x),转换为数字

### 求模 %

* x % y
* x,y都是数字,按照正常的计算,返回余数
* 如果被除数是无穷大值,而除数是有限大值,结果是NaN
* 如果被除数是有限大值,而除数是0,则结果是NaN
* 如果是Infinity 被 Infinity除,结果是NaN
* 如果被除数是有限大值,而除数是无穷大值,结果是被除数 ? 23 % Infinity = 0
* 如果被除数是0,结果是0
* 如果有1个不是数字,则调用 Number(x),转换为数字

### 加法 +

* x + y
* 有1个是NaN,返回NaN
* Infinity + Infinity = Infinity
* -Infinity + -Infinity = -Infinity
* Infinity + -Infinity = NaN
* +0 + +0 = +0
* -0 + -0 = -0
* +0 + -0  = +0
* 如果2个都是字符串, 则拼起来
* 如果只有1个是字符串,则将另一个转换为字符串,然后拼起来
* 如果有1个是对象,数值后者布尔,则调用他们的toString(),取得相应的字符串,然后应用前面的规则
* null和undefined会调用String()方法得到'null'和'undefined'

### 减法 -

* x - y
* 有1个是NaN,返回NaN
* Infinity - Infinity = NaN
* -Infinity - -Infinity = NaN
* Infinity - -Infinity = Infinity
* -Infinity - Infinity = -Infinity
* +0 - +0 = +0
* +0 - -0 = -0
* -0 - -0 = +0
* 如果有1个是字符串,布尔,null或undefined,则调用Number(x),转换为数值,然后在计算,如果转换得到NaN,则结果是NaN
* 如果有1个是对象,则调用valueOf(x),已取得数值,如果得到NaN,结果就是NaN,如果没有valueOf方法,则调用toString()方法,并将得到的字符串转化为数值

### 关系操作符 <, >, <=, >=

* 如果都是数字，则执行数字比较
* 如果都是字符串，比较字符串对应的字符编码值
* 如果1个是数字，则把另一个转化为数字，然后执行比较
* 如果1个是对象，则调用valueOf()方法，用得到的结果比较，如果没有valueOf()方法，则调用toString()方法，然后用得到的结果比较
* 如果有1个是布尔值，则先转换为数值，然后比较
* NaN参与比较，结果都是false
* null > 0; //false
* null >= 0; // true

### 相等操作符 ==,!=

* 如果有1个是布尔，则先转换为数值，true为1，false为0
* 如果1个是字符串，另一个是数值，则先将字符串转换为数字
* 如果1个是对象，另一个不是，则调用valueOf()，转化为基本类型然后再比较
* null和undefined是相等的
* 比较前，不能将null和undefined转化为其他值
* 如果1个是NaN,则判断相等时返回false，判断不相等时返回true，如果2个都是NaN，判断相等时也返回false
* 如果都是对象，则判断是不是同一对象，如果都指向同一对象，则相等，否则不相等

### 全等操作符 ===， !==

* 不进行转换，直接比较
* switch 语句使用的就是===，不会发生类型转换

## 变量，作用域，内存问题

### 基本类型和引用类型

* 基本类型，Undefined, Null, Boolean, Number, String
* 引用类型，Object
* js中，字符串是基本类型，不是引用类型
* ie, firefox下 typeof /sa/ -> 'object', chrome, safari下 typeof /sa/ -> 'function'

### 执行环境和作用域 73页

* 执行环境(execution context)
* 变量对象(variable object)
* 作用域链(scope chain)
* 活动对象(activation object)

### 延长作用域链 75页

* with语句，会将指定的对象添加到作用域链中
* catch语句，会创建一个新的变量对象，包含的是被抛出的错误对象的声明

### 执行环境总结

* 执行环境有全局执行环境和函数执行环境之分
* 每次进入一个新执行环境，都会创建一个用于搜索变量和函数的作用域链
* 函数的局部环境不仅有权访问函数作用域中的变量，还可以访问其包含环境(父环境), 乃至全局环境
* 全局环境只能访问在全局环境中定义的变量和函数，而不能直接访问局部环境中的任何数据
* 变量的执行环境有助于确定应该合适释放内存

### 引用类型

* `a = [1,2,3]; a.valueOf(); // [1,2,3] a.toString(); 1,2,3`
* `new Date().valueOf()`返回毫秒数
* ECMAScript 3中，正则表达式字面量始终共享一个RegExp实例，而使用构造函数创建的每一个新RegExp势力都是一个新实例
* ECMAScript 5中规定，正则表达式字面量每次都创建新的RegExp实例
* 正则表达式的valueOf()方法返回本身

### Function

* 函数是对象，函数名是指针
* 函数声明提升
* arguments.callee 指向拥有这个arguments对象的函数
* 函数.caller 保存着调用当前函数的函数的引用
* strict模式下，callee和caller均不允许访问
* `fun1.apply(this, [1,2,3])`
* `fun1.call(this, 1, 2, 3)`

### Boolean, Number

* 不建议使用包装对象

### String

```
str: hello world

slice(3): lo world
substring(3): lo world
substr(3): lo world

slice(3,7): lo w
substring(3, 7): lo w
substr(3, 7): lo worl

slice(-3): rld
substring(-3): hello world
substr(-3): rld

slice(3, -4): lo w
substring(3, -4): hel
substr(3, -4):
```

### prototype

通过构造函数创建的新实例的内部包含一个指针，指向构造函数的原型对象， [[ Prototype ]]，Firefox，Chrome里相当于是 __proto__，其他实现里，这个属性是不可见的。这个连接存在于实例和构造函数的原型对象之间，而不是实例和构造函数之间。

访问对象的属性时，如果对象实例包含这个属性，会直接返回这个属性，否则会查找对象的原型对象，看是否包含这个属性。

### inheritance

每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。

