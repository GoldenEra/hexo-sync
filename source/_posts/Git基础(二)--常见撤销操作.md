---
title: Git基础(二)--常见撤销操作
date: 2017-02-23 14:40:27
tags:
- Git
- 版本管理
---
## 前言
Git 的安装以及基本配置已在前一节写了，现在你已经正式可以开始使用了。正如在 Word 操作中最常用到的是 Ctrl+Z一样，在 Git 中，你也可能经常需要撤销操作，在此之前，先得明白 Git 几个常见的概念，Git 的区域划分。然后，了解一次最常见的工作流是如何操作的，了解经过操作后文件会的状态如何，会在哪个区域，最后才学习如何撤销每一步操作。

## Git 区域划分
先看一张图
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-083817.jpg)
这张图很清晰明了的展示了 Git 的几个区域，分别为

* working directory，工作区，所有的文件修改在这进行
* staging area，暂存区，修改完毕后的文件，将文件快照放入暂存区
* local repo，本地仓库区，提交暂存区的文件，将文件快照永久性存储到 Git 仓库目录
* remote repo，远程仓库区，位于服务器，保存来自所有客户端的提交

## 一次完整的工作流
按照上图中的步骤，使用 `git status` 可以查看任何时刻仓库文件的修改状态
### 第一步：编辑文件，查看状态

    git status
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-101315.jpg)

修改了READEME.md文件，此时文件在工作区，状态为modified
### 第二步：添加文件到暂存区

    git add READEME.md
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-101420.jpg)
此时文件已经到了暂存区，等待被提交到本地仓库

### 第三步：提交到本地仓库 

    git commit -m "update READEME.md"
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-101511.jpg)
提交本地仓库成功

### 第四步：将服务器的拉取到本地仓库

    git pull origin master

### 第五步： 提交到服务器 

    git push -u origin master

![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-102619.jpg)


这里暂时没有提到多人协同工作时常见的 conflict(冲突) 问题以及开发新功能用到的分支，不用着急，Git 分支也会在接下来的文章中介绍。

## 每个步骤如何撤销

### 撤销工作区文件 
    git checkout filename
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-102939.jpg)
### 撤销暂存区文件至工作区 
    git reset filename
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-102833.jpg)
### 撤销本地仓库的某次至工作区 
    git reset commit
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-103340.jpg)
可以通过  `git log` 和 `git reflog` 查看最近的 commit，找到最近的那次提交，然后通过 reset 命令撤销该操作
![](http://7xscq6.com1.z0.glb.clouddn.com/2017-02-23-103515.jpg)

上面有的操作对象是文件，有的是 commit，为什么呢？先弄清一点，把缓存区的文件（一个或多个文件）提交到本地仓库之后，Git 就会以某种识别码的形式来记录这次提交，这个识别码是 **独一无二**的。所以只要是提交到本地仓库后，操作对象就由文件变为 commit.

## 总结
了解了基本的工作流和常见的撤销操作之后，再加上接下来介绍的分支操作，基本上就覆盖了日常大部分使用场景。如果能再了解下 Git 的工作原理，想必学习起 Git 来是事半功倍的。

想当时学习 Git 走了不要弯路，总是一股脑的把错误信息扔到搜索引擎，然后按照搜来的结果“不知其所以然”的贴到命令行，运气好的时候，问题会被解决（没有报错），运气不好，会接二连三的报错，这时就陷入了恶性循环，到最后，你都不知道最初的问题是什么了。所以，在学习 Git 的操作同时，也要了解 Git 的原理，结合 Git 自带的提示/报错信息，大部分错误都基本上可以很快的解决。

当遇到实在解决不了的问题时，恭喜你，你变强了！

## 参考
* [Git 简史](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-Git-%E7%AE%80%E5%8F%B2)
* [Git 基础 - 撤消操作](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)