---
layout: post
title: J语言学习笔记
date: 2014-01-23 18:00
comments: true
categories: j
---



## 1 basic

### 基本运算

* `*:` 平方 *: 4 -> 16
* `|`  求余 2 | 4 -> 0
* 3*2+1 从右往左算, 3*(2+1) -> 9


### 赋值

* `x =: 3`
* 赋值语句也是表达式
* 区分大小写
* 在右侧只接收1个参数的叫做monadic, 简称monad, 比如 `*:`
* 在两侧接收参数的叫做dyadic, 简称dyad
* 有很多函数2者都是, 比如-作为负号或减号, %作为除号或者倒数

### 更多运算

* / join `+ / 2 3 4` -> 9
* true是1, false是0
* 数组长度 # 作为monad
* 过滤数组 # 作为 dyad
* 内置函数一般是1个或者2个字母, 2个字母的话第二个字母一般是:或者.
* 而且和1个字母的那个函数相关
* monad > 大于
* monad >. 向上取整 `>. 1.7` -> 2
* dyad >.  选择2个参数中大的一个 `2 >. 3` -> 3, `>. / 1 6 5` -> 6
* monad >: 给参数+1 `>: 1` -> 2
* dyad >: 大于或等于 `2 >: 2 3 4` -> 1 0 0

```
     x =: 5 4 1 9
     x > 2
1 1 0 1
     * / x > 2
0
     + / x > 2
3
     # x
4

     y =: 6 7 8 9 10
     1 1 0 1 0 # y
6 7 9

   y
6 7 8 9 10
   y > 7
0 0 1 1 1
(y>7) # y
8 9 10 
```

## 2 lists和table

* 表格语法 `table =: 2 3   $   5 6 7  8 9 10`
* 表格可以直接进行函数操作, +, * 等..
* monad $ 计算table的维度
* table 2 dimensions, list 2, single number 0 25页
* table 有2个dimensions, row和column
* array 用来统一称呼有一些dimension的数据结构
* $ 左边的数字就是这个数据结构的dimensions
* monad # 计算一个list的length
* monad $ 计算一个array的dimension
* rank 就是 dimension-count,
* shape 就是 list-of-dimension
* 字符串由单引号包裹, 2个单引号表示转义 `'123'`, `'12''3'`, `# ''` -> 0 

## array functions

* dyad , append, 合并 `a =: 1 2 b =: 3 4 a,b` -> 1 2 3 4



## select item

* dyad { from, select `Y =: 'abcd' 0 { Y` -> a `0 1 2 { Y` -> abc
* monad i. 生成一个range `i. 4` -> 0 1 2 3 4, `i. 2 3` -> `0 1 2 \n 3 4 5`
* dyad i. indexOf, 查询 `’abcd' i. 'a'` -> 0, 如果没找到, 则结果比最大的可能只大1 `'abcd' i. t` -> 4
* dyad -: match, 判断2个array是否相同 `x =: 'abc' x -: x` -> 1 , `'' -: 0 $ 0` -> 1
* dyad = equal, 判断2个参数中的元素是否相等 `y =: 1 2 3 4 , y = y` -> 1 1 1 1 , `y = 2` -> 0 1 0 0
* = 号的参数必须有相同的shape, 或者兼容的shape
* dyad ; link 将两个参数合并成一个list
* , 的参数类型必须相同, ; 的参数可以不同
* dyad ": format, 将数字转化为字符 `n =: 42 s =: ": n # s` -> 2, `ans is’ , s` -> ans is 42
* monad < box, create a box 
* monad > box, open a box,  scalars 标量




## 3 define function 

* rename, `square =: *: square 1 2 3` -> 1 4 9 
* insert, `sum =: + / sum 1 2 3` -> 6
* ordinary functions, * +  verbs
* compute functions from functions , / operators
* operator take arguments called adverbs , arguments at the left side
* + / -> adverb / is applied to the verb + , 副词修饰动词
* adverb dyad ,~ , change left and right arguments `1 ,~ 2` -> 2 1, `x f~ y` -> `y f x`
* bond, `double =: * & 2`, `(f & k) y means y f k`, `(k & f) y means k f y`
* conjunction: it conjoins two arguments
* functions in j: monadic verbs, dyadic verbs, adverbs , conjuctions
* every expression has a value of some type, function or data
* array called nouns, it’s not a verb, may have some dimensions
* composition of function: `sum square 1 2 3` -> 14
* dyad @: `sumsq =: sum @: square` `(f @: g) y` means f (g y)



## 更好记的

* square =: *:
* ceiling =: >.
* max     =: >.
* sum =: + /
* mod =: | ~
* sumsq =: sum @: square


未完待续...