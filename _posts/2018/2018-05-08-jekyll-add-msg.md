---
layout: post
title: jekyll博客装修日志：添加留言/评论等功能
tags: [jekyll]

---

> **前言：** 搭建jekyll很久了，文章虽然写的不多，但是总感觉缺少点什么，留言板？评论框？总之是缺少与用户交互的模块。最近觉得有必要对博客进行折腾一番了，于是就添加了**“微博关注按钮”**、**“推荐阅读”**、**“我的书架”**、**“留言/评论功能”**四个模块，顿时感觉博客丰富了许多，(#^.^#)，心得如下：

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

