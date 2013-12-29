---
layout: post
title: JavaScript学习笔记 - 一些quiz
date: 2013-12-29 17:45
comments: true
categories: javascript
---

## intro
共有50多到和js相关的题, 这里不提供答案, 建议不要直接贴到`console`里测试, 先思考一下, 然后去查资料, 知道为什么最好..   
注意这里有一小部分题是和平台有关的, 在ie下和在chrome, firefox里结果不一样, 这样的题不多, 注意着点...

## part1

```javascript
// http://dmitry.baranovskiy.com/post/91403200

//## 1
if (!("a" in window)) {
    var a = 1;
}
alert(a);

//## 2
var a = 1,
    b = function a(x) {
        x && a(--x);
    };
alert(a);

//## 3
function a(x) {
    return x * 2;
}
var a;
alert(a);

//## 4
function b(x, y, a) {
    arguments[2] = 10;
    alert(a);
}
b(1, 2, 3);

//## 5
function a() {
    alert(this);
}
a.call(null); 
```


## part2

```javascript

// http://dmitrysoshnikov.com/ecmascript/the-quiz/

//## 1
typeof typeof(null)


//## 2
typeof foo == 'undefined'
typeof foo === 'undefined'


//## 3
100['toString']['length']
'asdf'.['toString']['length']

//## 4
var a = (1,5 - 1) * 2


//## 5
var x = 10;
var foo = {
  x: 20,
  bar: function () {
    var x = 30;
    return this.x;

  }
};

console.log(
  foo.bar(),
  (foo.bar)(),
  (foo.bar = foo.bar)(),
  (foo.bar, foo.bar)()
);


//## 6
function f(x, y) {
  x = 10;
  console.log(
    arguments[0],
    arguments[1]
  );
}
f();


//## 7
var
  b = 10,
  c = (
    20,
    function (x) { return x + 100},
    function () { return arguments[0]}
  );
a = b + c
({x: 10}).x


//## 8
1..z


//## 9
({
  x: 10,
  foo: function () {
    function bar() {
      console.log(x);
      console.log(y);
      console.log(this.x);
    }
    with (this) {
      var x = 20;
      var y = 30;
      bar.call(this);
    }
  }
}).foo();


//## 10
// 这个不太明白...
foreach (k in {a: 10, b: 20})
{
  // ...
}
```


## part3

```javascript


 // http://www.nczonline.net/blog/2010/02/16/my-javascript-quiz/

//Example #1

var num1 = 5,
    num2 = 10,
    result = num1+++num2;

/*
Questions:
   * What is the value of result?
   * What is the value of num1?
   * What is the value of num2?
*/

//Example #2

var x = 5,
    o = {
        x: 10,
        doIt: function doIt(){
            var x = 20;
            setTimeout(function(){
                alert(this.x);
            }, 10);
        }
    };
o.doIt();

/*
Questions:
   * What value is displayed in the alert?
*/

//Example #3

var num1 = "10",
    num2 = "9";

/*
Questions:
   * What is the value of num1 < num2?
   * What is the value of +num1 < num2?
   * What is the value of num1 + num2?
   * What is the value of +num1 + num2?
*/

//Example #4

var message = "Hello world!";

/*
Questions:
   * What is the value of message.substring(1, 4)?
   * What is the value of message.substr(1,4)?
*/
//Example #5

var o = {
        x: 8,
        valueOf: function(){
            return this.x + 2;
        },
        toString: function(){
            return this.x.toString();
        }
    },
    result = o < "9";

alert(o);

/*
Questions:
   * What is the value result?
   * What is the value displayed in the alert?
*/

```


## part4

```javascript
// http://perfectionkills.com/javascript-quiz/

// ## 1
(function(){
     return typeof arguments;
})();

// ## 2
var f = function g(){ 
     return 23; 
}; 
typeof g(); 

// ## 3
(function(x){
     delete x;
     return x;
})(1); 

// ## 4
var y = 1, x = y = typeof x;
x;

// ## 5
(function f(f){
     return typeof f();
})(function(){
     return 1;
});

// ## 6
var foo = {
     bar: function() { 
          return this.baz; 
     }, 
     baz: 1
};
(function(){
     return typeof arguments[0]();
})(foo.bar); 

// ## 7
var foo = {
     bar: function(){
          return this.baz; 
     }, 
     baz: 1 
} 
typeof (f = foo.bar)(); 

// ## 8
var f = (function f(){
     return "1";
}, 
function g(){ 
     return 2; 
})();
typeof f; 

// ## 9
var x = 1;
if (function f(){}) { 
     x += typeof f; 
}
x; 

// ## 10
var x = [typeof x, typeof y][1];
typeof typeof x;

// ## 11
(function(foo) {
    return typeof foo.bar;
})({
    foo: {
        bar: 1
    }
});

// ## 12
(function f() {
     function f() {
         return 1;
     }
     return f();

     function f() {
         return 2;
     }
 })();

// ## 13
function f() {
    return f;
}
new f() instanceof f;

// ## 14
with(function(x, undefined) {}) length;

```


## part5

```javascript
http://madebyknight.com/javascript-scope/

// ## 1
function() {
    var a = 10;
    if(a > 5) {
        a = 7;
    }
    alert(a);
}

// ## 2
function() {
    if(true) {
        var a = 5;
    }
    alert(a);
}

// ## 3
var a = 5;
function first() {
    a = 6;
}


function second() {
    alert(a);
}

// ## 4
function first() {
    window.a = 3;
}

function second() {
    alert(a);
}

// ## 5
var a = 5;
function() {
    var a = 7;
    alert(a);
}

// ## 6
var a = 6;
function test() {
    var a = 7;
    function again() {
        var a = 8;
        alert(a);  // First
    }
    again();
    alert(a);  // Second
}
test();
alert(a);  // Third

// ## 7
function getFunc() {
    var a = 7;
    return function(b) {
        alert(a+b);
    }
}
var f = getFunc();
f(5);


```


## part6

```javascript

// ## 1
Function.prototype.toString.call({
    name: 'F',
    body: 'print("Javascript is hard")'
});

// ## 2
new String({
    toString : function (){ return this;},
    valueOf : function () {return this;}
});

// ## 3
typeof (new Date() + new Date());


// ## 4
typeof (void null);

// ## 5
function F() {}
F.prototype = new Function;
Object.prototype.toString.call(new F());

// ## 6
[].length = -2;

// ## 7
var D = Math.pow(2, 33);
(D | D) == D; 

// ## 8
'_string_'.replace(/^/, "$'");

// ## 9
eval('typeof F; function F() {}');

// ## 10
null > 0
null == 0
null >= 0

// ## 11
undefined > 0
undefined < 0
undefined == 0

// ## 12
NaN > 0 // false
NaN < 0 // false
NaN == 0 // false

```