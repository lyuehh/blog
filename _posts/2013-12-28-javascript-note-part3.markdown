---
layout: post
title: JavaScript学习笔记 - part3
date: 2013-12-28 15:35
comments: true
categories: javascript
---

## 值类型, 引用类型, 参数传递

```javascript

console.log('1:---');
(function() {
    var o1 = {
        name: 'a1'
    };
    var o2 = o1;
    o2.name = 'o2';
    console.log(o1.name);
})();


console.log('2:---');
(function() {
    var o1 = {
        name: 'a1'
    };
    var o2 = o1;
    o2.name = 'o2';
    o2 = {name: 'o3'};
    console.log(o1.name);
    console.log(o2.name);
})();

console.log('3:---');
(function() {

    function add(n) {
        n += 10;
        return n;
    }
    var a = 10;
    var b = add(a);
    console.log(a);
    console.log(b);
})();

console.log('4:---');
(function() {

    function setName(o) {
        o.name = '123';
    }
    var a = {};
    a.name = '456';
    setName(a);
    console.log(a.name);
})();

console.log('5:---');
(function() {

    function setName(o) {
        o.name = '123';
        o = {};
        o.name = 'aaa';
    }
    var a = {};
    a.name = '456';
    setName(a);
    console.log(a.name);
})();

```

## 块级作用域

```javascript
console.log('1:');
(function() {
    if (true) {
        var a = 'a';
    }
    console.log(a);
    if (false) {
        var b = 'b';
    }
    console.log(b);
})();

console.log('2:');
(function(){
    var a = '1';
    function f1() {
        console.log(a);
        var a;
    }
    f1();
})();


```

## 数组

```javascript
console.log('1:');
(function() {
    var a = [1,2,3,4];
    console.log(a.length);
    a.length = 2;
    console.log(a);
    a.length = 4;
    console.log(a);
})();

console.log('2:');
(function() {
    var b = [1,2,3];
    b[5] = 10;
    console.log(b.length);
    console.log(b);
})();

console.log('3:');
console.log(Object.prototype.toString.call([1,2,3]));
console.log(Array.isArray([1,2,3])); // only after es5

```

## 函数

```javascript
console.log('1:');
(function() {
    console.log(add(1, 2));
    function add(a, b) {
        return a + b;
    }
})();

console.log('2:');
(function() {
    //console.log(add(1, 2)); // ERROR
    var add = function (a, b) {
        return a + b;
    };
})();

console.log('3:');
a = 'a';
var o = {a: 'b'};
function showA() {
    console.log(this.a);
}
showA();
o.showA = showA;
o.showA();

console.log('4:');
function add(a, b) {
    return a + b;
}
console.log(add.name);
console.log(add.length);

console.log('5:');
a = 'a';
var o = {a: 'b'};
function showA() {
    console.log(this.a);
}
showA.call(this); // different in node and browser
showA.call(o);

```