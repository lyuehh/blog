---
layout: post
title: 命令行里学汉语
date: 2014-01-27 09:45
comments: true
categories: learn
---

## 1

汉语博大精深, 文字游戏也很好玩, 偶尔想不起来的时候就需要别人的帮助了, 有了下面这些工具, 生活就会更好玩一点...

## 2

下面这些工具都是一个`npm`模块, 你需要`npm`这个命令, 可以从<http://nodejs.org/download/>下载`nodejs`, 安装完就会有`npm`这个命令了  
然后执行 `npm install -g pinyinjs opencc-cli gtrs chengyu tangshi songci` 就可以安装以下需要用到的所有命令了

## 3

### 查拼音 

遇到不认识的字或者词, 可以用 `pinyin` 来查拼音, 示例如下:

```
~ ^_^ pinyin 魑魅魍魉
chī mèi wǎng liǎng

~ ^_^ pinyin 银行行长走在人行道上
yín háng háng cháng zǒu zài rén xíng dào shàng
```

有个问题是这个有时候处理不了多音字...

### 简转繁, 繁转简

有时候可能有这个需求, 那么可以用`s2t`和`t2s`来转换, 示例如下:

```
~ ^_^ s2t 曾经有一份真挚的爱情放在我面前，我没有珍惜，等我失去的时候，我才后悔莫及，人世间最痛苦的事莫过于此。
曾經有一份真摯的愛情放在我面前，我沒有珍惜，等我失去的時候，我才後悔莫及，人世間最痛苦的事莫過於此。

~ ^_^ t2s 如果上天能夠給我再來一次的機會，我會對那個女孩子說三個字：我愛你。如果非要在這份愛上加上一個期限，我希望是。。。一萬年！
如果上天能够给我再来一次的机会，我会对那个女孩子说三个字：我爱你。如果非要在这份爱上加上一个期限，我希望是。。。一万年！
```

### 英译汉, 汉译英

就是把汉语翻译成英语, 把英语翻译成汉语, 示例如下:

```
~ ^_^ gtrs 好玩
好玩: Fun

~ ^_^ gtrs fun
fun: 有趣 Yǒuqù

动词: 开玩笑
开玩笑: joke,fun,crack a joke,play a joke,trifle,spoof

名词: 玩笑,意思
玩笑: joke,fun,jest,pleasantry,raillery,josh
意思: meaning,sense,fun,connotation,pleasure,interest
```

还可以翻译句子, 比如:

```
~ ^_^ gtrs '今天天气不错啊'
今天天气不错啊: The weather today is good ah

~ ^_^ gtrs 'The weather today is good ah'
The weather today is good ah: 今天天气不错啊 Jīntiān tiānqì bùcuò a
```

上面的结果是[Google翻译](http://translate.google.cn/?hl=en)返回的..

### 查找成语

成语是个好东西, 简洁有强大, 可以使用`chengyu` 调用, 示例如下:

```
# 查找 AABB 这样的成语, 另外还支持 AABC ABCC ABBC

~ ^_^ chengyu -p AABB
七七八八
万万千千
三三两两
三三五五
三三四四
世世代代
.........

# 查找某个位置是某个字的成语

~ ^_^ chengyu -w 一xxx
一丁不识
一不扭众
一世之雄
一世龙门
一丘一壑
.........

# 查找包含某个字的成语

~ ^_^ chengyu -i 雪
万里雪飘
云起雪飞
以汤沃雪
傲雪凌霜
傲雪欺霜
傲霜斗雪
..........

# 查看所有的成语

~ ^_^ chengyu --all
一人敌
一刀切
一字师
一掊土
一溜烟
一牛鸣
一硼地
.........
```

## 学唐诗

唐诗也很好玩, 可以通过 `tangshi`命令调用, 示例如下:

```
# 查看某个作者的所有诗列表

~ ^_^ tangshi -a 李白
乐府杂曲·鼓吹曲辞·上之回 李白
三十六离宫，楼台与天通。阁道步行月，美人愁烟空。
恩疏宠不及，桃李伤春风。淫乐意何极，金舆向回中。
万乘出黄道，千旗扬彩虹。前军细柳北，后骑甘泉东。
岂问渭川老，宁邀襄野童。秋暮瑶池宴，归来乐未穷。
......

# 查看某一首诗

~ ^_^ tangshi -t 静夜思
静夜思 李白
床前看月光，疑是地上霜。举头望山月，低头思故乡。

# 查找标题中包含某个字或词的诗

~ ^_^ tangshi -s 心
伤心行 李贺
咽咽学楚吟，病骨伤幽素。秋姿白发生，木叶啼风雨。
灯青兰膏歇，落照飞蛾舞。古壁生凝尘，羁魂梦中语。
......

# 查找内容中包含某个字或词的诗

~ ^_^ tangshi -c 思故乡
静夜思 李白
床前看月光，疑是地上霜。举头望山月，低头思故乡。


春陪商州裴使君游石娥溪（时欲东归遂有此赠） 李白
裴公有仙标，拔俗数千丈。澹荡沧洲云，飘飖紫霞想。
剖竹商洛间，政成心已闲。萧条出世表，冥寂闭玄关。
我来属芳节，解榻时相悦。褰帷对云峰，扬袂指松雪。
暂出东城边，遂游西岩前。横天耸翠壁，喷壑鸣红泉。
寻幽殊未歇，爱此春光发。溪傍饶名花，石上有好月。
命驾归去来，露华生翠苔。淹留惜将晚，复听清猿哀。
清猿断人肠，游子思故乡。明发首东路，此欢焉可忘。
.......

# 查看所有的作者列表

~ ^_^ tangshi --authors
李世民
李治
李显
李旦
......

# 查看所有的诗的列表

~ ^_^ tangshi --poetries
帝京篇十首 李世民
秦川雄帝宅，函谷壮皇居。绮殿千寻起，离宫百雉馀。
连薨遥接汉，飞观迥凌虚。云日隐层阙，风烟出绮疏。
......

```

## 学宋词

和唐诗类似, 可以通过 `songci`命令调用, 示例如下:

```
# 查看某个作者的所有词列表

~ ^_^ songci -a 李清照
一翦梅 李清照
红藕香残玉簟秋。轻解罗裳，独上兰舟。云中谁寄锦书来，雁字回时，月满西楼。花自飘零水自流。一种相思，两处闲愁。此情无计可消除，才下眉头，却上心头。
......

# 查看某一首词

~ ^_^ songci -t 雨霖铃
雨霖铃 晁端礼
槐阴添绿。雨余花落，酒病相续。闲寻双杏凝伫，池塘暖、鸳鸯浴。却向窗昼卧，正春睡难足。叹好梦、一一无凭，帐掩金花坐凝目。　　当时共赏移红烛。向花间、小饮杯盘促。蔷薇花下曾记，双凤带、索题诗曲。别后厌厌，应是香肌，瘦减罗幅。问燕子、不肯传情，甚入华堂宿。
......

# 查找标题中包含某个字或词的词

~ ^_^ songci -s 心
水调歌头（登赏心亭怀古） 丘崈
一雁破空碧，秋满荻花洲。淮山淡扫，欲颦眉黛唤人愁。落日归云天外，目断清江无际，浩荡没轻鸥。有恨寄流水，无泪学羁囚。　　望石城，思东府，话西州。平芜千里，古来佳处几回秋。歌舞当年何在，罗绮一时同尽，梦幻两悠悠。杯到莫停手，唯酒可忘忧。
......

# 查找内容中包含某个字或词的词

~ ^_^ songci -c 兰舟催发
雨霖铃（双调） 柳永
寒蝉凄切。对长亭晚，骤雨初歇。都门帐饮无绪，留恋处、兰舟催发。执手相看泪眼，竟无语凝噎。念去去、千里烟波，暮霭沈沈楚天阔。　　多情自古伤离别。更那堪、冷落清秋节。今宵酒醒何处，杨柳岸、晓风残月。此去经年，应是良辰、好景虚设。便纵有、千种风情，更与何人说。
.......

# 查看所有的作者列表

~ ^_^ songci --authors
丁仙现
丁几仲
丁宥
丁察院
丁持正
丁无悔
......

# 查看所有的词的列表

~ ^_^ songci --poetries
绛都春（上元） 丁仙现
融和又报。乍瑞霭霁色，皇州春早。翠幰竞飞，玉勒争驰都门道。鳌山彩结蓬莱岛。向晚色、双龙衔照。绛绡楼上，彤芝盖底，仰瞻天表。　　　　缥缈。风传帝乐，庆三殿共赏，群仙同到。迤逦御香，飘满人间闻嬉笑。须臾一点星球小。渐隐隐、鸣鞘声杳。游人月下归来，洞天未晓。
......

```

## 4

用到的工具的源码的链接:

* <https://github.com/hotoo/node-pinyin>
* <https://github.com/lyuehh/opencc_cli>
* <https://github.com/lyuehh/google-translate-ci>
* <https://github.com/lyuehh/chengyu>
* <https://github.com/lyuehh/tangshi>
* <https://github.com/lyuehh/songci>


