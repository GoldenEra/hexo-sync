---
title: Git基础(三)--常见错误及解决方案
date: 2017-03-03 14:53:14
tags:
- Git
---
## 前言
了解一些常见的错误对了解 Git 的原理也是很有帮助的，下面就是在日常工作中常见的一些错误信息以及解决方案。不能保证每个人引起错误的原因都是一样的，下面的一些操作也不见得解决你遇到的问题，仅供参考。

## 常见错误
### You have unmerged files
```
$ git status
On branch master
You have unmerged paths.
(fix conflicts and run "git commit")
Unmerged paths:
(use "git add <file>..." to mark resolution)
both modified:      index.html
no changes added to commit (use "git add" and/or "git commit -a")
```
原因：见上面conflict的原因
解决方案：查看发生冲突的文件，手动修改后commit，通过 `git mergetool` 可以看到图形化的界面，便于直观的理解。
参考：[Git 分支 - 分支的新建与合并](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)

### add操作 warning
```
    $ git add -A
    warning: LF will be replaced by CRLF in file
    The file will have its original line endings in your working directory.
```
原因：Linux平台下的换行符是 LF，而Windows下则是 CRLF，所以当你再 Windows 保存文件时候，换行符会被保存为 
建议：统一换行符为 LF 
方案：
Git 命令行输入如下命令，禁止自动转换换行符
``` 
 git config --global core.autocrlf false
```
Sulime Text下的用户自定义增加以下配置：
```
    "default_line_ending": "unix",  
    "trim_trailing_white_space_on_save": true,
    "ensure_newline_at_eof_on_save": true,
```
### pull 失败
```
    You have not concluded your merge (MERGE_HEAD exists).
    Please, commit your changes before you can merge.
```
原因：之前进行 Pull 操作时自动合并失败，和原文件有冲突
解决方案：取消 Pull 操作然后手动合并

* 取消合并
```
    git merge --abort
    git reset --merge
```
* 解决冲突
* 重新 add and commit
* 拉取分支然后合并，`git pull`

参考：[You have not concluded your merge (MERGE_HEAD exists)](http://stackoverflow.com/questions/11646107/you-have-not-concluded-your-merge-merge-head-exists)   

### push error: failed to push some refs to ''
```
    $ git push origin master
    To john@githost:simplegit.git
    ! [rejected] master -> master (non-fast forward)
    error: failed to push some refs to 'john@githost:simplegit.git'
```
原因：之前有人进行过提交，本地项目并不是最新的，在提交之前，必须合并当前分支至最新
解决方案：`git merge origin/master`，当你直接在master分支的时候，可以`git pull`，相当于`git fetch + git merge`
参考：[分布式 Git - 向一个项目贡献](https://git-scm.com/book/zh/v2/%E5%88%86%E5%B8%83%E5%BC%8F-Git-%E5%90%91%E4%B8%80%E4%B8%AA%E9%A1%B9%E7%9B%AE%E8%B4%A1%E7%8C%AE)

### checkout : Unable to create '/path/project/.git/index.lock'

报错信息：
```
    Git - fatal: Unable to create '/path/my_project/.git/index.lock': File exists.
```

解决方案：`rm -f ./.git/index.lock`
参考资料：[stack参考](http://stackoverflow.com/questions/7860751/git-fatal-unable-to-create-path-my-project-git-index-lock-file-exists)

### 其他错误：fatal: object 0ffe6959ad4ca1exxx is corrupted

find the sha and delete it
```
    rm .git/object/0f/fe69
```
then you will get this error
error: fatal: bad object HEAD 
```
    git fetch origin 
    git reset --hard origin/master
```

## 总结
可以看到，每次错误信息出现，Git 都会有很详细的提示，有些时候还会有原因解释以及基本的建议解决方案。所以，不要一出错就复制错误信息到网上取搜索，然后复制一些你自己也不知道有什么作用的命令，有时候甚至会酿成大祸（有一次就删除了许多图片然后push到了服务器，幸亏有备份）。

退一步讲，如果你要复制网络上的命令，有一条准则谨记，**任何命令中带有 --hard 参数的都谨慎执行**，很有可能造成不可逆的损失。










