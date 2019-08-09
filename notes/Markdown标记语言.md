# 标题
用来生成标题，从H1到H5。
~~~
# H1
## H2
### H3
#### H4
##### H5
###### H6
对于H1,H2还有另外两种特别的写法：

Alt-H1
======

Alt-H2
------
~~~

效果如下：  
# H1
## H2
### H3
#### H4
##### H5
###### H6

Alt-H1
======

Alt-H2
------

# 换行操作  
~~~
换行  测试
格式为：  （两个空格）
md语言与HTML一致，回车换行在上述两种语言无效，需要进行换行操作。
~~~
效果如下：  
Markdown语言  是最方便的标记语言。  

# 引用表现
~~~
> 鲁迅：“Markdown是最方便的标记语言”
格式为：>  （大于号加空格）

特殊用途：如果文字太长不利于阅读，可以用此方法变得易于阅读。
~~~
效果如下：  
> 鲁迅：“Markdown是最方便的标记语言”  
大段文字转换：  
> 7月，我国外汇市场运行保持平稳。”王春英说，她指出，国际金融市场上，受全球贸易局势、主要国家央行货币政策、英国脱欧前景、地缘政治因素等影响，主要货币相对美元汇率均有所下跌，全球债券指数有所上涨。汇率折算和资产价格变化等因素综合影响外汇储备规模。
# 增加分割线  
~~~
分割线以下有三种方法
---
***
___
格式为：文字加回车加三种符号
特别地，---与H2标题的标记方法类似，区别在于文字与---之间有无回车
Markdown是最方便的标记语言
---
以上为H2标题方法
Markdown是最方便的标记语言

---
以上为分割线方法
~~~
三种效果如下：  
Markdown是最方便的标记语言

---
#强调表现
~~~
1.斜体 格式为：*XXX* , _XXX_
2.粗体 格式为：**XXX** , ___XXX___
3.区域加粗 格式为：**XXX 和___XXX___**
4.删除线 格式为：~~XXX~~
~~~
效果如下：
*斜体* **粗体** **区域加粗，你看我粗不粗** ~~删除线~~  
#列表表示
~~~
无序列表
列表符号：-
列表符号：*
列表符号：+
格式如下：（上述符号加空格）
- 自拍
- 偷拍
- 国产专区
- 丝袜美腿
- 另类乱伦
有序列表
列表符号：数字.
格式如下：（数字加.加空格）（第一个数字必须是1，以后的数字可以写0，这样避免了以后在中间插入文字后造成顺序需要重新输入一次的麻烦。）
1 自拍
0 偷拍
0 国产专区
0 丝袜美腿
0 另类乱伦
需要添加层次，可以键入两个空格
- 自拍
  - 偷拍
  - 国产专区
- 丝袜美腿
- 另类乱伦
~~~
效果如下：
无序（带层次）： 
- 自拍
  - 日韩专区
  - 国产专区
- 偷拍
- 丝袜美腿
- 另类乱伦
有序：
1. 自拍
0. 偷拍
0. 国产专区
0. 丝袜美腿
0. 另类乱伦
# 超文本链接
~~~
方法1：
[Markdown github](https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet#headers)
方法2：
[Markdown github](https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet#headers "这是Markdown的主页")
方法3：
[这里放超连接名，后面是网址预留位置][这是网址预留位置]
[这里放超链接名，后面也可以用数字预留][1]
或者干脆前面直接省略[404网站]

预留位置在后面需要声明，否则是无效的。

格式如下：（冒号后面加一个空格）
[这是网址预留位置]： https://www.youtube.com
[1]： https://www.google.com
[404网站]: https://twitter.com
~~~
# 代码高亮显示
~~~
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```
可以用三个`或者三个~，后面跟着自定义指定语言

也可以在文字中插入代码。
例：你可以使用`add(x,y)`来计算x+y的和。
~~~
[Markdown支持的语言](https://highlightjs.org/static/demo/)
# 图片显示
~~~
格式1：
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

格式2：
![alt text][假装这里有个网址]

[假装这里有个网址]: htps://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"
~~~
格式1：
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")  
格式2：
![alt text][假装这里有个网址]

[假装这里有个网址]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"  
# 表格显示
~~~
|TH1|TH2|TH3|
|---|---|---|
|TD1|TD3|TD5|
|TD2|TD4|TD6|
表格外框可以省略不写

表格样式：
|左对齐|居中|右对齐|
|:---|:---:|---:|
|TD1|TD3|TD5|
|TD2|TD4|TD6|

在表格中也可以使用引用和强调样式：
Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
~~~
效果如下：
|左对齐|居中|右对齐|
|:---|:---:|---:|
|TD1|TD3|TD5|
|TD2|TD4|TD6|

---
Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
# 添加YouTube视频  
<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>




