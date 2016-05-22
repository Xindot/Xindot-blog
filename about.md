---
layout: page
title: 关于博客
---

{% comment %}
  This inserts the "about" photo and text from `_config.yml`.
  You can edit it there (jekyll needs restart!) or remove it and provide your own photo/text.
  Don't forget to add the `me` class to the photo, like this: `![alt](src){:.me}`.
{% endcomment %}

{% if site.author.photo %}
  ![{{ site.author.name }}]({{ site.author.photo }}){:.me}
{% endif %}

{{ site.author.about }}

>*微博[@曾经小僧](http://weibo.com/603451688){:target="_blank"}*
>*简书[@曾经小僧](http://www.jianshu.com/users/423b873cad24/latest_articles){:target="_blank"}*

