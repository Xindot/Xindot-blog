---
layout: page
title: About Me

---

{% comment %}
  This inserts the "about" photo and text from `_config.yml`.
  You can edit it there (jekyll needs restart!) or remove it and provide your own photo/text.
  Don't forget to add the `me` class to the photo, like this: `![alt](src){:.me}`.
{% endcomment %}

{% if site.author.photo %}
  ![{{ site.author.name }}]({{site.author.photo}}){:.me .rotate-infinite}
{% endif %}

{{ site.author.about }}

>*[@微博](http://weibo.com/603451688){:target="_blank"}*
>*[@简书](http://www.jianshu.com/users/423b873cad24/latest_articles){:target="_blank"}*
>*[@知乎](https://www.zhihu.com/people/Durling_Xie){:target="_blank"}*
>*[@豆瓣](https://www.douban.com/people/Durling/){:target="_blank"}*
>*[@SF](https://segmentfault.com/u/durling){:target="_blank"}*

![Mou icon](http://img.6h5.cn/xindot-blog/hangzhou.jpg)

###### 我的周边
>*[个人简历-IT](/2015/05/20/xin-resume/)<br/>*
>*[猫博客 · MaoMao日常](http://maomao.nuoluan.com){:target="_blank"}*

---

###### 友情链接
{% if site.attach.links %}
  {% for item in site.attach.links %} [{{ item[0] }}]({{item[1]}}){:target="_blank"} {% endfor %}
{% endif %}
