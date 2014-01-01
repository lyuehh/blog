---
layout: post
title: 命令行JSON,CSV数据处理工具简介
date: 2014-01-01 11:03
comments: true
categories: json
---

## 简介
`json`现在是最流行的数据交换格式了,但是在命令行中显示, 查找, 处理, 还是不如纯文本方便, 但是有了下面这些工具, 处理`json`数据可以易如反掌了。。
以下只介绍`OS X`平台, `Linux`下相应工具也都有, 建议自己折腾就不介绍了, 至于`windows`用户, 自己想办法。。。

## 准备工作

* `brew`, `OS X`的包管理工具, 没有的话请先安装, <http://brew.sh/>
* `python`, 编程语言, 系统自带, <http://python.org>
* `ruby`, 编程语言, 系统自带, <https://www.ruby-lang.org/en/>
* `node`, 基于`v8`的`javascript`平台, `brew install node`, <http://nodejs.org>
* `go`, 编程语言, Google出品, `brew install go`, <http://golang.org>
* `R`, 编程语言, 擅长计算机统计和画图, <http://www.r-project.org/>
* `pip`, `python`的包管理工具, 安装`easy_install pip`, <https://pypi.python.org/pypi/pip>
* `gem`, `ruby`的包管理工具, 自带了, <http://rubygems.org>
* `npm`, `node`的包管理工具, 安装完`node`就有了, <https://npmjs.org>

## 用到的工具

* `curl`, 下载工具, 系统自带, <http://curl.haxx.se>
* `wget`, 另一个下载工具, `brew install wget`, <http://www.gnu.org/software/wget/>
* `yajl`, `C`语言编写的`json`库, 安装: `brew install yajl`, <http://lloyd.github.io/yajl/>
* `pygmentize`, `ruby`语言的`Pygments`绑定, `Pygments`是用`python`编写的代码高亮工具, <http://pygments.org/>
* `jq`, `C`编写的命令行`json`处理工具, `brew install jq`, <http://stedolan.github.io/jq/>
* `json2csv`, `go`编写的`json`转`csv`工具, `go get github.com/jehiah/json2csv`, <https://github.com/jehiah/json2csv>
* `csvkit`, `python`编写的`csv`格式处理工具, `sudo pip install csvkit`, <https://github.com/onyxfish/csvkit>
* `xml2json`, `javascript`编写的`xml`转`json`工具, `npm install -g xml2json-command`, <https://github.com/parmentf/xml2json>

## 获取`json`文件

1. 可以用`curl`, 比如`curl https://registry.npmjs.org > registry.json`
2. 还可以用`wget`, 比如`wget https://registry.npmjs.org -o registry.json`
3. 或者你从其他地方弄一个`json`文件过来

## 查看`json`文件

```
cat registry.json
```

## 校验`json`


```
cat registry.json | json_verify
```

或者:

```
cat invalid.json | python -mjson.tool
```

## 格式化`json`

```
cat registry.json | json_reformat
```

或者:

```
cat invalid.json | python -mjson.tool
```

## 高亮

```
cat registry.json | json_reformat | pygmentize -l javascript
```

或者:

```
cat registry.json | jq .
```

## 在`json`中查找数据

以下以`https://registry.npmjs.org/underscore`这个`json`文件为素材, 可以使用
`curl https://registry.npmjs.org/underscore  > u.json` 获取这个文件

### 查看某个属性

```
jq '._id' u.json # 'underscore'
```

### 查看某2个属性

```
jq '._id, .description' u.json
# ->
# "underscore"
# "JavaScript's functional programming helper library."
```

### 看看一个数组

```
jq '.versions["1.0.3"].keywords' u.json # ["util","functional","server","client","browser"]
```

### 查看一个数组的第1个值

```
jq '.versions["1.0.3"].keywords[1]' u.json # "functional"
```

### 过滤属性

```
jq '.versions["1.0.3"] | .name, .author.name' u.json
# ->
# "underscore"
# "Jeremy Ashkenas"
```

更多的例子请参考 `man page`: `man jq`

## 转换`json`为`csv`

```
cat registry.json | json2csv -k db_name,doc_count,update_seq
# registry,52964,870607
```

## 处理`csv`格式的数据

### 排序 `csvsort`
### 查看 `csvlook`
### 保存到数据库里 `csvsql`

## 用XPath和CSS选择器进行HTML信息提取 scrape

```
curl -s 'http://en.wikipedia.org/wiki/List_of_countries_and_territories_by_border/area_ratio' | scrape -b -e 'table.wikitable > tr:not(:first-child)' 
```
## 把XML转换成JSON xml2json

```
curl -s 'http://en.wikipedia.org/wiki/List_of_countries_and_territories_by_border/area_ratio' | scrape -be 'table.wikitable > tr:not(:first-child)' | xml2json | jq -c '.html.body.tr[] | {country: .td[1][], border: .td[2][], surface: .td[3][], ratio: .td[4][]}' | head
```

未完待续...