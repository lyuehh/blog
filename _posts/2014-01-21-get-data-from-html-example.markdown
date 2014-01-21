---
layout: post
title: 从HTML中抽取数据示例-双色球
date: 2014-01-21 17:30
comments: true
categories: json
---

# 从HTML中抽取数据示例-双色球


## 1

生在在天朝这种地方, 如果不是XXX或者XXX, 想要改变命运, 估计只能去买彩票了, 虽然彩票那东西也很可能不是真正的随机, 但是至少还是有一点盼头的...
万一不是真正的随机, 那可能还是有规律可循的, 要真是那样就太好了, 这里就想办法得到双色球的数据, 然后分析下有什么规律, 怎么分析还不知道,
我们先把数据拿下来再说...

## 2

经过google的搜索, 发现<http://www.3dcp.cn/zs/gonggao.php?type=ssq&year=2003>这个网站提供了从2003年到2014年的所有双色球数据,
有的还有中奖的注数, 奖金啥的, 那我们就想办法从这里拿到数据就可以了

## 3

知道了数据源, 然后就要选择趁手的工具了, 这里使用`curl`和一个`JavaScript`编写的工具`hquery`, 其他的工具, 编程语言也都是可以的, 
能赚到耗子的猫都是好猫..

```shell
for i in `seq 2003 2014`
do
    u="http://www.3dcp.cn/zs/gonggao.php?type=ssq&year=$i"
    echo $u
    curl -s $u | iconv -f gbk -t utf8  | hquery -p -r '$("table").eq(13).parent().html()' > $i.html
done
```

简单解释一下:  
从2003循环到2013, 然后curl得到html内容, 使用iconv将编码转换为utf8, 然后使用hquery从html中抽取出相应的table, 然后保存到对应年份的html里

## 4

html已经拿到了, 再写一个工具再次处理html即可..

编写一个js文件处理html, 保存在a.js, 代码如下:  

```javascript
a = _.reduce($("tr"), function(memo, v, i) {
    var $el = $(v);
    var obj = {};
    obj.id = $.trim($el.find('.end').text());
    obj.date = $el.find('td').eq(1).text();
    obj.red = $el.find('.STYLE13').html() && $el.find('.STYLE13').html().replace(/&nbsp;/g, ' ');
    obj.blue = $el.find('.STYLE12').text();
    if (obj.id !== '') {
        memo.push(obj);
    }
    return memo;
}, []);
console.log(JSON.stringify(a, null, 2));

```

然后再写一个小shell循环即可:

```shell
for i in `seq 2003 2014`
do
    echo $i
    cat ${i}.html | hquery -p -f a.js | sed '$d' > json/${i}.json
done
```
稍微解释一下:  
hquery 接受 -f参数, 将文件内容视为js代码执行, 然后将结果输出, `sed $d`将最后一行删除, 因为那是一个undefined....

## 5

搞定, 双色球数据就保存在 2003.json ~ 2014.json中了, 格式为:

```
{
    "id": "2003001",
    "date": "2003-02-23",
    "red": "10 11 12 13 26 28 ",
    "blue": "11"
}
...
```

这样就可以接下来的处理了...

hquery是我写的一个小工具, 基于jsdom, 包含了jQuery和underscore, 利用强大的eval, 实现了从html中抽取数据的工作...js的eval太强大了...

## links

* [code](https://gist.github.com/lyuehh/8537324)
* [hquery](http://github.com/lyuehh/hquery)




