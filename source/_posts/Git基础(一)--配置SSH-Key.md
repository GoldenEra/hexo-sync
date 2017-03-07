---
title: Git基础(一)--安装和配置SSH-Key
date: 2017-02-16 15:24:44
tags: 
- Git 
- 技术
- 工具
---
## 前言
工欲先善其事，必先利其器。在工作之中，得心应手的工具能让你更多的专注于工作本身，提高效率。在编写程序方面，如何管理代码一直是一个很令人头痛的问题。尤其是代码规模越来越大的时候，如何记录每一次更改？如何在不更改源代码基础上开发一个新功能？如何做回滚？等等……这时候，Git应运而生。
  
首先，需纠正很多人，包括我从学校过度到工作之后的一个想法，就是无论做什么都必须先了解原理。这种想法在工作中不可取，工作是以优先完成任务为目的，深究原理会消耗大量工作时间。了解原理可以在空闲时间琢磨，切不可因此耽搁进程。

## Git和GitHub的区别
关于Git和Github的区别，一句话以概之。Git是一个开源代码版本管理工具，GitHub是基于该工具做的一个项目托管平台，和Github功能类似的还有[Bitbucket](https://bitbucket.org/product)、[Coding](https://coding.net/)，它们使用的工具都是Git，只是各自提供一些特色功能，如权限管理、issue提交、Group管理等。

## 安装
客户端大致分为两类，图形化客户端和命令行。图形化客户端口碑较好的有[SourceTree](https://www.sourcetreeapp.com/)，不过还是建议在命令行进行操作，这样对Git的原理能有一个更好的了解。参考里有下载方式。

安装完毕之后，我们需要对 Git 做一些基本的配置，这些配置都是为了日后能更方便、更便捷的使用 Git。这里所做的配置都是在命令行下完成的，这里还是建议大家尽量使用命令行工具进行 Git 操作，虽然初期可能稍有不便、需要查询各种命令的使用、命令行会报各种错误，但只要耐心得去查手册，去网上搜寻解决方案，相信要不了多久，你就能熟练地使用 Git，成为一个 Git 高手。

## 全局设置
Git 每次提交都会记录提交者的基本信息，例如名字、邮箱、提交时间等等，部分需要用户自己配置，下面是配置命令。
提交代码时显示的用户名
    
    git config --global user.name "Apple" 

邮箱，默认为登录邮箱

    git config --global user.email test@gmail.com 

设置编辑器，下面是针对Windows下设置sublime text为默认编辑器

    git config --global core.editor "'c:/user/sublime text 3.exe' -w"

Git会为大部分的输出打出颜色，如果git diff时的不同颜色的输出有助于快速定位

    git config --global color.ui true

输入自动补全功能

    git config --global core.autocrlf input

## 配置SSH-Key

如果你发现每次提交代码时，服务器都会要求验真你的身份，那么，接下来的配置会让你免去这个烦恼。
可以在自己电脑上生成两把钥匙，一把交给服务器，一把自己留着。那么，每次你提交代码，服务器就会看到你本地的钥匙是不是和我服务器的钥匙匹配，以此来达到验证的目的。
留在本地的是 private key，服务器保存的是 public key, 这也就意味着可以将同样的钥匙(public key)填入不同的服务器。下面来讲如何做

* 本地通过命令`ssh-keygen` 生成SSH公钥，首先 ssh-keygen 会确认密钥的存储位置（默认是 ～/.ssh/id_rsa），然后它会要求你输入两次密钥口令。如果你不想在使用密钥时输入口令，将其留空即可

* 复制 id_rsa.pub 中的 **全部** 内容,添加到[github](https://github.com/settings/ssh)/[bitbucket](https://bitbucket.org/account/user/your-name/ssh-keys/)中

* 测试成功与否 `ssh -T git@github.com`, 如果成功会有一段warning，yes即可

## 参考：

* [Git跟Github是什么关系](https://www.zhihu.com/question/21907548)
* [GitHub - 账户的创建和配置](https://git-scm.com/book/zh/v2/GitHub-%E8%B4%A6%E6%88%B7%E7%9A%84%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE)
* [Git命令行下载](https://git-scm.com/downloads)
* [SourceTree下载](https://www.sourcetreeapp.com/)
* [Generating SSH keys](https://help.github.com/articles/generating-an-ssh-key/)
