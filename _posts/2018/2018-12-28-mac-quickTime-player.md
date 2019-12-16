---
layout: post
title: 如何用Mac自带软件录屏且只录制屏内或屏外声音
tags: [mac]

---

突然有个小需求，想录制一段视频。然后就找到了Mac自带的

![20191216173459](http://img.6h5.cn/xindot-blog/paste/20191216173459.png){:style="width:30%"}

![20191216173541](http://img.6h5.cn/xindot-blog/paste/20191216173541.png){:style="width:70%"}

![20191216173603](http://img.6h5.cn/xindot-blog/paste/20191216173603.png){:style="width:70%"}

然后录了一段视频，发现视频中有两个声音，一个是我音乐播放器里面的声音，一个是我所处环境产生的声音。但这显然不是我想要的。

不过很幸运，网上找了一篇文章，为了防止网址丢失，我就贴过来了，顺便做了部分修改和补充

为了防止大神骂我，[原文地址](http://www.i5seo.com/mac-own-software-recording-screen.html){:target="_blank"}也放一下  ~(*^__^*) ~

---

### 如何用mac自带软件录屏且录制屏内屏外声音？这个问题困扰了很多使用苹果mac笔记本的用户，本教程你能get到的3个技能点

> 1.用macbook自带软件录屏（无屏内屏外声音）<br/>
2.用macbook自带软件录屏+有屏内声音+无屏外声音（需要插件）<br/>
3.用macbook自带软件录屏+有屏内声音+有屏外声音（需要插件）<br/>

以及一些在操作过程中需要注意的地方

> 1.SOUNDFLOWER这个插件安装不了，提示来自身份不明的开发者怎么办<br/>
2.电脑里下载安装了SOUNDFLOWER，怎么删除<br/>
3.SOUNDFLOWER这个插件适合MAC什么版本<br/>
4.SOUNDFLOWER 2CH 和SOUNDFLOWER 64CH有什么区别<br/>
5.我本人在首次录屏操作失误地方的小提示<br/>
6.录屏结束后需要注意的一个地方

完整「视频教程」可以在我的B站频道观看。
[点击这里](https://www.bilibili.com/video/av31462592/)观看哟～

### 1、用macbook自带软件录屏（无屏内屏外声音）

需要用到的软件就是：

![20191216173753](http://img.6h5.cn/xindot-blog/paste/20191216173753.png){:style="width:30%"}

双击图标-单击菜单栏的文件-选择新建屏幕录制

![20191216173830](http://img.6h5.cn/xindot-blog/paste/20191216173830.png){:style="width:70%"}

![20191216174044](http://img.6h5.cn/xindot-blog/paste/20191216174044.png){:style="width:70%"}

录全屏：点击红色小圆点-点屏幕任一位置  就开始录制全屏了

录部分屏幕：点击红色小圆点-鼠标拖动想要录制的区域-点击开始录制 就开始录制部分屏幕

### 2、用macbook自带软件录屏+有屏内声音+无屏外声音（需要插件），首先需要下载一个插件soundflower

> ~(*^__^*) ~ 补充：要下载这个 [Soundflower-2.0b2.dmg](http://mysoft.6h5.cn/Soundflower-2.0b2.dmg){:target="_blank"} 这里提供一个地址 

![20191216174711](http://img.6h5.cn/xindot-blog/paste/20191216174711.png){:style="width:70%"}

2.1、soundflower这个插件安装不了，提示来自身份不明的开发者怎么办

![20191216174740](http://img.6h5.cn/xindot-blog/paste/20191216174740.png){:style="width:70%"}

（会弹一个类似这样的提示，图片来源网络）

这个时候找到系统偏好设置-安全性与隐私

![20191216174819](http://img.6h5.cn/xindot-blog/paste/20191216174819.png)

下方会看到一行警示的文字，然后选择：【仍要打开】即可安装。

![20191216174843](http://img.6h5.cn/xindot-blog/paste/20191216174843.png){:style="width:70%"}

2.2、设置部分

（1）在应用程序里找到-MIDI音频设置

![20191216174913](http://img.6h5.cn/xindot-blog/paste/20191216174913.png)

点击下方的“+”

创建【聚集设备】

![20191216175125](http://img.6h5.cn/xindot-blog/paste/20191216175125.png){:style="width:50%"}

勾选【内建麦克风】+【soundflower 64ch 或2ch】

![20191216175144](http://img.6h5.cn/xindot-blog/paste/20191216175144.png)

创建【多输出设备】

![20191216175200](http://img.6h5.cn/xindot-blog/paste/20191216175200.png)

（2）点击【系统偏好设置】-【声音】-输出那里选择【多数出设备】（其他地方不用管他）

![20191216175259](http://img.6h5.cn/xindot-blog/paste/20191216175259.png)

（3）现在可以开始用Quicktime player 开始录制屏内声音啦～

【soundflower 64ch 或2ch】（你前面在MIDI音频设置里选的是什么这里对应选什么）

![20191216175556](http://img.6h5.cn/xindot-blog/paste/20191216175556.png){:style="width:70%"}

![20191216175611](http://img.6h5.cn/xindot-blog/paste/20191216175611.png)

点击红点-点击屏幕任意位置-开始录制啦～-菜单栏里的白色点 点击他结束录制。

### 3、用macbook自带软件录屏+有屏内声音+有屏外声音（需要插件）

点击圆点旁边的【倒三角】-选择【聚集设备】-点击红点 后面录制的步骤一样的啦～

![20191216175714](http://img.6h5.cn/xindot-blog/paste/20191216175714.png)

### Q：电脑里下载安装了soundflower，怎么删除？

A：emmmmm你是在电脑里找不到这个插件的，无论是用聚集搜索还是在cleanmymac里的电脑插件都看不到，反正才58k，也不影响电脑，就不用删啦～

### Q：soundflower这个插件适合Mac什么版本？

A：之前看到有人说最新的Mac版本这个插件会不zici？开玩笑，我还用的是最新的 mojave beta版都大丈夫，所以请你们安心食用好了

![20191216175859](http://img.6h5.cn/xindot-blog/paste/20191216175859.png)

![20191216175913](http://img.6h5.cn/xindot-blog/paste/20191216175913.png)

### Q：soundflower 2ch 和soundflower 64ch有什么区别？

A：拖到pr里面 2ch 有2个重复的音轨  64ch 有8个音轨 7个是空白音轨，自行比较一下音质吧嘻嘻

![20191216175953](http://img.6h5.cn/xindot-blog/paste/20191216175953.png)

### Q：你在首次录屏操作失误地方的小提示是啥？

A：emmmmm这个地方的音量条千万不要拖动他，不然就会有回音，会有回音，有回音，回音，音….

![20191216180019](http://img.6h5.cn/xindot-blog/paste/20191216180019.png){:style="width:60%;"}

### Q: 录屏结束后需要注意的一个地方是啥？

A：【系统便好设置】-【声音】-输出这里选择调回【内置扬声器/耳机】

![20191216180111](http://img.6h5.cn/xindot-blog/paste/20191216180111.png)

如果忘记调回到【内置扬声器】，像图下这样，音量条是灰色的，你听歌看视频的时候只能调节播放器的音量，还想要更大声，就无法调节电脑音量咯。

![20191216180130](http://img.6h5.cn/xindot-blog/paste/20191216180130.png)

---

~(*^__^*) ~ 补充：录屏的软件还有几个也比较好用，比如：QQ、

![20191216180149](http://img.6h5.cn/xindot-blog/paste/20191216180149.png)

