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

* `brew`, `OS X`的包管理工具, 没有的话请先安装<http://brew.sh/>
* `python`, 编程语言, 系统自带
* `ruby`, 编程语言, 系统自带
* `node`, 基于`v8`的`javascript`平台, `brew install node`
* `go`, 编程语言, Google出品, `brew install go`
* `R`, 编程语言, 擅长计算机统计和画图, <http://www.r-project.org/>
* `pip`, `python`的包管理工具, 如果没有的话, 先安装`easy_install pip`
* `gem`, `ruby`的包管理工具, 自带了
* `npm`, `node`的包管理工具, 安装完`node`就有了

## 用到的工具

* `curl`, 下载工具, 系统自带
* `wget`, 另一个下载工具, `brew install wget`
* `yajl`, `C`语言编写的`json`库, 安装: `brew install yajl`
* `pygmentize`, `ruby`语言的`Pygments`绑定, `Pygments`是用`python`编写的代码高亮工具
* `jq`, `C`编写的命令行`json`处理工具, `brew install jq`
* `json2csv`, `go`编写的`json`转`csv`工具, `go get github.com/jehiah/json2csv`
* `csvkit`, `python`编写的`csv`格式处理工具, `sudo pip install csvkit`
* `xml2json`, `javascript`编写的`xml`转`json`工具, `npm install -g xml2json-command`

## 获取`json`文件

1. 可以用`curl`, 比如`curl https://registry.npmjs.org > registry.json`
2. 还可以用`wget`, 比如`wget https://registry.npmjs.org -o registry.json`
3. 或者你从其他地方弄一个`json`文件过来

## 查看`json`文件

```shell
$ cat registry.json
```

```
{"db_name":"registry","doc_count":52964,"doc_del_count":4875,"update_seq":870607,"purge_seq":0,"compact_running":false,"disk_size":208315547783,"data_size":175867283928,"instance_start_time":"1388433643562558","disk_format_version":6,"committed_update_seq":870607}
``

## 校验`json`

### 1. yajl

```shell
$ cat registry.json | json_verify`
```


### 2. python

```
$ cat invalid.json | python -mjson.tool
```

## 格式化`json`

### 1. yajl

`cat registry.json | json_reformat`

### 2. python

`cat invalid.json | python -mjson.tool`

## 高亮

### 1. pygmentize

`cat registry.json | json_reformat | pygmentize -l javascript`

## 

