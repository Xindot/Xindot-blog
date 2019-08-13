---
layout: post
title: 如何在Windows环境的Git Bash下使用rsync？
tags: [git]

---

> 前言：个人一直使用mac版的rsync，前一段时间有同事用的是windows，我便向他安利rsync。网上找了好几个安装方案，都不太好使，最终找到了下面这篇文章。鉴于国外网站安装包下载慢，我就把包放在了自己国内的服务器，欢迎下载使用。申明：下文非本人原创，属个人整理收藏使用。

---

`rsync`是非常高效的文件夹远程差异同步工具，我现在就用它来同步Jekyll博客系统的`_site`文件夹到我的Web服务器，不过以前都是在Macbook上操作，很是顺利，可在Windows上并没有官方的下载方式，折腾了很多办法，通过MingW下载的并不能在Git Bash上运行，可能是不兼容的。那么，今天我们就来看看如何获取Windows版的rsync。

## Solution

[Tiger Fok](https://blog.tiger-workshop.com/add-rsync-to-git-bash-for-windows/)在他的博客上告诉了我们一个非常好用的方法，那就是使用[pacman库](http://www2.futureware.at/~nickoe/msys2-mirror/msys/)中的rsync程序，里面i686代表32位系统，x86_64代表64位系统，也可以到下面~~我的百度网盘~~下载。（改为七牛云存储）

首先先安装Git Bash，然后下载rsync

## 32位Git Bash、rsync下载
```
http://mysoft.6h5.cn/win/Git-2.22.0-32-bit.exe
http://mysoft.6h5.cn/win/rsync.32.zip
```

## 64位Git Bash、rsync下载
```
http://mysoft.6h5.cn/win/Git-2.22.0-64-bit.exe
http://mysoft.6h5.cn/win/rsync.64.zip
```

下载完成后，用7Zip解压两次（百度网盘的我已经打包成Zip了），找到`rsync.exe`，把这个文件拷贝到Git Bash目录`C:\Program Files\Git\usr\bin`即可在Git Bash上使用了。

---

参考：[https://blog.tiger-workshop.com/add-rsync-to-git-bash-for-windows/](https://blog.tiger-workshop.com/add-rsync-to-git-bash-for-windows/)

来源：[https://done.moe/tutorial/2018/07/25/how-to-use-rsync-on-windows-git-bash/](https://done.moe/tutorial/2018/07/25/how-to-use-rsync-on-windows-git-bash/)

