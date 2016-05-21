---
layout: post
title: gitignore屏蔽不想push的文件
tags: [git]
---

node项目根目录添加文件.gitignore
内容如下：

	.DS_Store
	.project
	public/avatar/ .log
	nohup.out
	npm-debug.log

则在git push的时候则不会提交以上这些文件