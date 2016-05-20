---
layout: post
title: linux重定向及nohup不输出的方法【整理稿】
tags: [nodejs]
---

先说一下linux重定向：
0、1和2分别表示**标准输入**、**标准输出**和**标准错误信息输出**，可以用来指定需要重定向的标准输入或输出。

>**在一般使用时，默认的是标准输出，既1**

当我们需要特殊用途时，可以使用其他标号。例如，将某个程序的错误信息输出到log文件中：./program 2>log。这样标准输出还是在屏幕上，但是错误信息会输出到log文件中。

另外，也可以实现0，1，2之间的重定向。

>**2>&1 将错误信息重定向到标准输出。**

Linux下还有一个特殊的文件/dev/null，它就像一个无底洞，所有重定向到它的信息都会消失得无影无踪。这一点非常有用，当我们不需要回显程序的所有信息时，就可以将输出重定向到/dev/null。
如果想要正常输出和错误信息都不显示，则要把标准输出和标准错误都重定向到/dev/null， 例如：

	ls 1>/dev/null 2>/dev/null

还有一种做法是将错误重定向到标准输出，然后再重定向到 /dev/null，例如：

	ls >/dev/null 2>&1

注意：此处的顺序不能更改，否则达不到想要的效果，此时先将标准输出重定向到 /dev/null，然后将标准错误重定向到标准输出，由于标准输出已经重定向到了/dev/null，因此标准错误也会重定向到/dev/null，于是一切静悄悄:-)

由于使用nohup时，会自动将输出写入nohup.out文件中，如果文件很大的话，nohup.out就会不停的增大，这是我们不希望看到的，因此，可以利用/dev/null来解决这个问题。

（1）舍弃标准输出，将错误输出到log文件中

	nohup node bin/www >/dev/null 2>log &

（2）如果错误信息也不想要的话：

	nohup node bin/www >/dev/null 2>&1 &

注：其中**node bin/www**是项目node启动

***

>**关于`重定向`，参考文章：[http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=484163](http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=484163){:target="_blank"}**



## 1. 基本概念

	a、I/O重定向通常与 FD有关，shell的FD通常为10个，即 0～9；（FD：file descripter，文件描述符）
	b、常用FD有3个，为: 0（stdin，标准输入）、1（stdout，标准输出）、2（stderr，标准错误输出），默认与keyboard、monitor、monitor有关；
	c、用 < 来改变读进的数据信道(stdin)，使之从指定的档案读进；
	d、用 > 来改变送出的数据信道(stdout, stderr)，使之输出到指定的档案；
	e、0 是 < 的默认值，因此 < 与 0<是一样的；同理，> 与 1> 是一样的；
	f、在IO重定向 中，stdout 与 stderr 的管道会先准备好，才会从 stdin 读进资料；
	g、管道“|”(pipe line):上一个命令的 stdout 接到下一个命令的 stdin;
	h、tee 命令是在不影响原本 I/O 的情况下，将 stdout 复制一份到档案去;
	i、bash（ksh）执行命令的过程：分析命令－变量求值－命令替代（``和$( )）－重定向－通配符展开－确定路径－执行命令；
	j、( )  将 command group 置于 sub-shell 去执行，也称 nested sub-shell，它有一点非常重要的特性是：继承父shell的Standard input, output, and error plus any other open file descriptors。
	k、exec 命令：常用来替代当前 shell 并重新启动一个 shell，换句话说，并没有启动子 shell。使用这一命令时任何现有环境都将会被清除，。exec 在对文件描述符进行操作的时候，也只有在这时，exec 不会覆盖你当前的 shell 环境。

## 2. 基本IO

	cmd > file              把 stdout 重定向到 file 文件中
	cmd >> file             把 stdout 重定向到 file 文件中(追加)
	cmd 1> fiel             把 stdout 重定向到 file 文件中
	cmd > file 2>&1         把 stdout 和 stderr 一起重定向到 file 文件中
	cmd 2> file             把 stderr 重定向到 file 文件中
	cmd 2>> file            把 stderr 重定向到 file 文件中(追加)
	cmd >> file 2>&1        把 stderr 和 stderr 一起重定向到 file 文件中
	cmd < file >file2       cmd 命令以 file 文件作为 stdin，以 file2 文件作为 stdout
	cat <>file              以读写的方式打开 file
	cmd < file              cmd 命令以 file 文件作为 stdin
	cmd << delimiter        Here document，从 stdin 中读入，直至遇到delimiter 分界符

