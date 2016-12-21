---
layout: post
title: Git常用终端命令
tags: [git]
---

写在前面

>Git想必大家都熟悉了，由于现在Git的管理工具用的的确很方便，估计大家都用Git管理工具了，所以真正能够熟练用终端敲出常用的Git命令，想必没有多少人（当然也包括我）。<br><br>
我用Git比较无规律，都是混合使用的：终端Git命令（会一些常用的） + Xcode自带Git管理工具 + SourceTree。具体会使用哪种方式，完全看心情和操作的熟练度。
最近闲来无事（等后台哥们的接口），索性看了下常用的Git终端命令，顺便做了下笔记与大家分享，当然也方便了以后自己的查阅。<br><br>
本文Git常用命令知识点基本来自“廖雪峰 ”前辈的[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000){:target="_blank"}。若对Git没有些许的了解，只看常用命令可能对大家的帮助不是太大，所以建议大家有空的时候花点时间去看下“廖雪峰 ”前辈的[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000){:target="_blank"}，通熟易懂，相信会有所收获。<br><br>
最后，若文章有什么错误的地方，望评论指出。

## git init

>初始化一个Git仓库：把某个目录变成Git可以管理的仓库

## git add test.h

>把文件test.h添加到仓库

## git commit -m "添加了test.h文件"
	
>把文件提交到仓库。(git commit命令，-m后面输入的是本次提交的说明)

## git status

>查看工作区的状态

## git diff test.h

>查看test.h文件修改了什么（diff--->difference）

## git log

>显示从最近到最远的提交日志。如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数

## git reset --hard HEAD^

>回到上一个版本

## git reset --hard HEAD^^

>回到上上个版本

## git reset --hard HEAD~100

>回到上100个版本

## git reset --hard 791c95aa44cc5540d93a146d6d341e5d38936762

>根据提交的版本号进行版本的回退

## git reflog

>查看命令历史，以便确定要回到未来的哪个版本。

## git checkout -- readme.txt

>命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。<br><br>
总之，就是让这个文件回到最近一次git commit或git add时的状态。

## git reset HEAD 文件

>例如： git reset HEAD readme.txt <br><br>
可以把暂存区的修改撤销掉（unstage），重新放回工作区。若要丢弃工作区的修改，还需要git checkout -- readme.txt <br><br>
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。

## git remote add origin git@...................

>关联一个远程库

## git push

>把当前分支推送到远程

## git push -u origin master

>当远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

## git clone git@.............

>克隆

## git branch dev

>创建一个名称叫dev的分支

## git checkout dev

>当前的分支切换为dev分支

## git checkout -b dev

>创建一个dev分支，并且切换到dev分支（相当于是是前面两句命令的合并）

## git branch

>列出所有分支，当前分支前面会标一个*号

## git merge dev

>把dev分支的工作成果合并到当前分支上、git merge命令用于合并指定分支到当前分支

## git branch -d dev

>删除dev分支

## git branch -D dev

>若dev分支还没合并到所切出来的分支，则git branch -d 
dev将不能删除dev分支，可以通过git branch -D dev强行删除dev分支

## git log --graph

>查看分支合并图 <br><br>
git log --graph --pretty=oneline --abbrev-commit

## git merge --no-ff -m "备注的信息" dev

>将dev分支合并到当前分支的时候强制禁用Fast forward模式
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。<br><br>
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。<br><br>
合并分支时，加上--no-ff
参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward
合并就看不出来曾经做过合并。

## git stash

>可用来暂存当前正在进行的工作

## git stash list

>查看已暂存列表

## git stash apply

>恢复工作现场，但是恢复后，stash内容并不删除

## git stash drop

>删除stash内容

## git stash pop

>恢复的同时把stash内容也删了，相当于前面两个命令的结合

## git stash apply stash@{0}

>恢复指定的stash

## git remote

>要查看远程库的名称

## git remote -v

>显示更详细的远程库信息。显示可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址

## git push origin 本地分支的名称

>把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

## git branch -r

>查看远程分支

## git branch -a

>查看所有分支（会显示本地分支和远程分支）

git fetch

>个人粗浅的理解为将远程所有的分支信息拉取到本地

git checkout -b local-branchname origin/remote_branchname

>将远程分支映射到本地命名为local-branchname 的一分支（本地分支名称最好和远程分支名称一致）

git branch --set-upstream dev origin/dev

>指定本地dev分支与远程origin/dev分支的链接

git tag

>查看所有标签

git tag 标签名称

>打标签：默认标签是打在最新提交的commit上的

git tag 标签名称 commit的版本号

>例如：git tag v0.9 6224937
在制定的提交位置上打上标签

git show 标签名称

>查看标签信息

git tag -a 我是标签 -m "添加了标签" 3628164

>例如：git tag -a v0.1 -m "version 0.1 released" 3628164
创建带有说明的标签，用-a指定标签名，-m指定说明文字。经测试 -a可以去掉，也就可以写成
git tag 我是标签 -m "添加了标签" 3628164

git tag -d v0.1

>删除一个叫做 v0.1的本地标签

git push origin :refs/tags/<tagname>

>删除一个远程标签

git push origin 标签名称

>推送某个标签到远程

git push origin --tags

>一次性推送全部尚未推送到远程的本地标签

	文／chenfanfang（简书作者）
	原文链接：http://www.jianshu.com/p/87ab8acf4b87
	著作权归作者所有，转载请联系作者获得授权，并标注“简书作者”。
