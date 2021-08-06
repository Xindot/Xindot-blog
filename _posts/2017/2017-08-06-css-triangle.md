---
layout: post
title: CSS实现三角形、梯形
tags: [css]
categories: [it]

---

主要css代码如下：
```
//html
<div class="triangle-4"></div>

//css
.triangle-4 {
  width: 0;
  height: 0;
  display: inline-block;
  border-top: solid 100px red;
  border-right: solid 100px blue;
  border-bottom: solid 100px black;
  border-left: solid 100px salmon;
}
```

查看*[demo效果](/assets/demo/triangle.html){:target="_blank"}*