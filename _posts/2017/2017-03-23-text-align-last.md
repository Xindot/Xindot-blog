---
layout: post
title: text-align-last 实现几个汉字的两端分散对齐
tags: [js]
categories: [it]

---

### 1 左端对齐 -> 两端分散对齐

![20191219183527](http://img.6h5.cn/xindot-blog/paste/20191219183527.png){:style="width:48%;display:inline-block;"}
![20191219183422](http://img.6h5.cn/xindot-blog/paste/20191219183422.png){:style="width:48%;display:inline-block;"}

### 2 css代码
```
.el-input-group__prepend {
  text-align: justify;
  text-align-last: justify;
  text-justify: distribute-all-lines; // 兼容ie浏览器
  width: 42px;
}
```

### 3 兼容性

![20191219184539](http://img.6h5.cn/xindot-blog/paste/20191219184539.png)

> 参考:<br/>
[text-align-last 实现文本居中对齐](https://www.cnblogs.com/mengfangui/p/11445139.html){:target="_blank"}<br/>
[如何用css实现一段文字的两端对齐和分散对齐](https://zhidao.baidu.com/question/298189268.html){:target="_blank"}