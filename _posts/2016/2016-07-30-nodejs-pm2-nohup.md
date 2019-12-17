---
layout: post
title: linux重定向及nohup不输出的方法【整理稿】
tags: [nodejs]
categories: [it]

---



pm2是一个内置负载均衡的nodejs应用的生产进程管理器；它能让您的应用永远保持活着，

pm2嵌入一个简单而强大的模块系统，安装一个模块是简单的：

	$ pm2 install <模块名称>

这里有一些pm2兼容模块（独立于pm2管理的nodejs的应用）：