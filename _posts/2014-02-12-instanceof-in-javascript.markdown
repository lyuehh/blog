---
layout: post
title: JavaScript学习笔记 - instanceof运算符
date: 2014-02-12 15:30
comments: true
categories: javascript
---

## 1

`instanceof`运算符检查一个构造函数的`prototype`是否在一个对象的原型链中.

## 2

语法: 

```
a instanceof B
```

说明:

a 是一个对象, B是一个函数

## 3

规则:

如果  
`Object.getPrototypeOf(a) === B.prototype`, 或者    
`Object.getPrototypeOf(Object.getPrototypeOf(a)) === B.prototype`  
等等... 那么返回true, 否则返回false.

也可以这么理解:

如果 `a.__proto__ === B.prototype`, 或者 `a.__proto__.__proto__ === B.prototype`等等... 那么返回true, 否则返回false.

## 4

```
Function instanceof Object // ?
Object instanceof Function // ?
```

分析:

### Function instanceof Object

`Function` 是一个函数, 是`Function`构造函数的一个实例, 所以 `Function.__proto__ === Function.prototype`, `而Function.prototype` 是一个对象的实例,
所以 `Function.prototype.__proto__ === Object.prototype`, 也就是说 `Function.__proto__.__proto__ === Object.prototype`, 所以这个结果是true

### Object instanceof Function

`Object` 是一个函数, 也是Function构造函数的一个实例, `Object.__proto__ === Function.prototype`, 所以这个结果也是true

### 同理, 以下这些都是true

```
Function instanceof Function
String instanceof Function
Number instanceof Function
Boolean instanceof Function
Array instanceof Function
```

## 5
![prototype.jpg](http://lyuehh-img.qiniudn.com/prototype.jpg)

## 6

参考资料:

* <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof>
* <http://www.cnblogs.com/objectorl/archive/2010/01/11/Object-instancof-Function-clarification.html>

