---
title: Git基础配置(一)--配置SSH-Key
date: 2017-02-16 15:24:44
tags: 
- Git 
- 技术
---
  工欲先善其事，必先利其器。在工作之中，得心应手的工具能让你更多的专注于工作本身，提高效率。在编写程序方面，如何管理代码一直是一个很令人头痛的问题。尤其是代码规模越来越大的时候，Git应运而生。
  
首先，需纠正很多人，包括我从学校过度到工作之后的一个想法，就是无论做什么都必须先了解原理。这种想法在工作中不可取，工作是以漂亮完成任务为目的，深究原理会消耗大量工作时间。了解原理的事可以空闲时间琢磨，切不可因此耽搁项目进程。
  
前提是已经有安装好的的Git客户端。

## 全局设置

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

许多Git服务器都是用SSH公钥进行验证。通过命令生成两个key，一个是public key填写在服务器端，一个是private，保存在本地。当客户端和服务端进行交流（如提交代码），服务端通过检测两个key是否匹配。

* 本地通过命令`ssh-keygen` 生成SSH公钥,首先 ssh-keygen 会确认密钥的存储位置（默认是 .ssh/id_rsa），然后它会要求你输入两次密钥口令。如果你不想在使用密钥时输入口令，将其留空即可

* 复制 id_rsa.pub 中的内容,添加到[github](https://github.com/settings/ssh)/[bitbucket](https://bitbucket.org/account/user/your-name/ssh-keys/)中

* 测试成功与否 `ssh -T git@github.com`, 如果成功会有一段warning，yes即可

## 参考：

* [GitHub - 账户的创建和配置](https://git-scm.com/book/zh/v2/GitHub-%E8%B4%A6%E6%88%B7%E7%9A%84%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE)

* [Generating SSH keys](https://help.github.com/articles/generating-an-ssh-key/)
