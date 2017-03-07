---
title: Fail2Ban的使用
date: 2017-02-22 14:59:27
tags:
- vps
- 安全
- 翻译
---
## 前言
在前面的[增强 VPS 的安全性]()中已经说到，可以通过简单的配置`/etc/ssh/sshd_conf`文件来增强服务器的安全性，但是如果有更进一步的需求呢？这里介绍一个功能更加强大，配置更加灵活的第三方工具 Fail2Ban。
PS：以下内容大致翻译自文章 [How To Protect SSH with Fail2Ban on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04)，有所删减，部分加上自己的理解，如果遗漏之处，请见谅，也可以查看原文。

## 介绍
通过 SSH 来登陆服务器是很安全的，为了相应客户端的登陆请求，服务器端会驻留 SSH 相关服务以保证你在任何时候登陆都会得到服务器响应。现在问题来了，SSH 服务是暴露在互联网之上的，换句话说，任何人都可以在任何时候通过IP/域名尝试登陆你的服务器。如果你看过 ssh 登陆日志的话，可以看到每天都有很多失败的登陆尝试。

Fail2Ban 可以在一定程度上缓解这个问题，通过该工具的自定义规则结合 `iptables` 防火墙配置来禁止某些尝试次数过多的IP地址。
下面就是安装和配置过程，操作系统为 Ubuntu 14.04。

## 安装
通过 Ubuntu 自带的包管理命令即可安装该工具，命令如下
```
sudo apt-get update
sudo apt-get install fail2ban
```
## 配置
安装完毕后，所有和 fail2ban 的有关配置文件都位于 `/etc/fail2ban` 目录下。默认的配置文件名为 `jail.conf`。
不过，在升级 fail2ban 的时候，配置文件会被覆盖，配置也就失效了。所以，我们不能直接修改 `jail.conf` 文件。可以复制一份名为 `jail.local` 的文件，将你的自定义配置写在里面去覆盖 `jail.conf` 里的内容，默认配置还是位于 `jail.conf`。

```
awk '{ printf "# "; print; }' /etc/fail2ban/jail.conf | sudo tee /etc/fail2ban/jail.local
```

现在我们可以打开`jail.local`看看具体有哪些配置选项。

请注意，在[DEFAULT]标签下会被所有 



## 参考
* [How To Protect SSH with Fail2Ban on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04)
