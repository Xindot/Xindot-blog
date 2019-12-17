---
layout: post
title: jekyll博客装修日志：添加留言/评论等功能
tags: [jekyll]
categories: [it]

---

> **前言：** 搭建jekyll很久了，文章偶尔写写，不过总感觉缺少点什么，留言板？评论框？有多少读者？问题反馈？总之是缺少与用户交互的模块，没有互动感。最近觉得有必要对博客进行折腾一番了，于是就添加了 **“微博关注按钮”**、**“推荐课程”**、**“我的书架”**、**“留言/评论功能”** 四个模块，顿时感觉博客丰富了许多，(*^▽^*)，心得如下，献丑了：

## 1.微博关注按钮

来先看微博给到的*[文档](https://open.weibo.com/widget/followbutton.php){:target="_blank"}*里面的设置按钮样式、及部署三要素：

1.在HTML标签中增加XML命名空间

```
<html xmlns:wb="http://open.weibo.com/wb">
```

2.在HEAD头中引入WB.JS

```
<script src="https://tjs.sjs.sinajs.cn/open/api/js/wb.js" type="text/javascript" charset="utf-8"></script>
```

3.在需要部署微博关注按钮的位置粘贴WBML代码，<del>查看更多参数</del>

```
<wb:follow-button uid="3129142911" type="red_1" width="67" height="24" ></wb:follow-button>
```

###### 补充我的部署： 在`_layouts/post.html`中添加代码块

![微博关注按钮位置](http://img.6h5.cn/xindot-blog/paste/20191215183506.png)

效果如下：

![博客中添加微博关注按钮](http://img.6h5.cn/xindot-blog/paste/20191215190800.png)

---

## 2.推荐课程/我的书架

先不说别的，来看一下效果

![推荐课程](http://img.6h5.cn/xindot-blog/paste/20191215202124.png)

![我的书架](http://img.6h5.cn/xindot-blog/paste/20191215202155.png)

然后直接看代码，先设置好课程的数据

<small>注：这里是写死的数据，不是接口取得。不过不要失望，后面评论内容取得是接口</small>

![课程数据](http://img.6h5.cn/xindot-blog/paste/20191215202327.png)

然后是课程展示代码如下

<small>注：由于部分代码无法显示，只好截图了</small>

![课程展示代码](http://img.6h5.cn/xindot-blog/paste/20191215202716.png)

#### 我的书架功能同上

---

## 3.留言/评论功能

jekyll自带**disqus**评论社区，不过有博友反映国内速度慢，我想你懂得。如果你想尝试，这里推荐一篇文章：
[正确的Disqus使用姿势](https://www.jianshu.com/p/7e4453421b8f){:target="_blank"}<br/>
国内早期也有~~多说~~，不过不知为何也关闭了。这真不是个好消息。<br>

我的方案是自己建库写接口：nodejs（接口） + axios（客户顿请求）

下面是我写的五个接口，基本可以满足我的需求，更多可查看：[api接口文档](https://www.nianran.net/static/apiDoc/sun_api_v2.html){:target="_blank"}

<small>注：接口文档用的是[eolinker](https://www.eolinker.com/){:target="_blank"}，
然后转html自己部署到自己的服务器</small>

![接口文档](http://img.6h5.cn/xindot-blog/paste/20191215204522.png)

下面是mysql数据表

![mysql数据结构](http://img.6h5.cn/xindot-blog/paste/20191215204924.png)

可以看出，点赞我使用的是ip数组，没有用关联表，想到点赞数也不会太多，简单点好。同样，回复数据也是一样。

大致效果如下：

![留言效果](http://img.6h5.cn/xindot-blog/paste/20191215205613.png)

由于评论/留言功能代码行数太多，这里就不放了，需要的留言/评论哦。