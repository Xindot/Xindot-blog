---
layout: post
title: 发现：图片根据页面滚动逐渐变色的效果
tags: [css]
categories: [it]

---

> **前言：**网页要想做的好，视觉交互很重要。
最近在留意一些比较好的交互，也就当是学习了。
觉得这个还不错，来看效果：[Element](https://element.eleme.cn/2.11/#/zh-CN){:target="_blank"}

### 效果

![201911190001](https://img.6h5.cn/xindot-blog/gif/201911190001.gif)

![20191219170328](http://img.6h5.cn/xindot-blog/paste/20191219170328.png)

### 原理

> 其实原理简单，就是用了两个图片，图片完全重叠，并设置了上面图片显示的高度

![](https://element.eleme.cn/2.11/static/theme-index-blue.c38b733.png){:style="width:200px;display:inline-block;"}
![](https://element.eleme.cn/2.11/static/theme-index-red.c8e136e.png){:style="width:200px;display:inline-block;"}

### 代码

##### html 通过js监听滚动改变高度
```
<div class="jumbotron">
  <img src="https://element.eleme.cn/2.11/static/theme-index-blue.c38b733.png" alt="">
  <div class="jumbotron-red" style="height: 248px;">
    <img src="https://element.eleme.cn/2.11/static/theme-index-red.c8e136e.png" alt="">
  </div>
</div>
```

##### css 加了过渡效果
```
.jumbotron .jumbotron-red {
  transition: height .1s;
  background: #fff;
  position: absolute;
  left: 0;
  top: 0;
  overflow: hidden;
}
```