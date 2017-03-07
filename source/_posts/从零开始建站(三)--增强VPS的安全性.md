---
title: 从零开始建站(三)--增强VPS的安全性
date: 2017-02-16 11:51:20
tags: 
- 技术
- vps
- 安全
---

当你拥有一台新的 Linux Server 之后，为了增加安全性，可以做一些安全配置。
默认初始登录都是 root，以 root 用户来操作服务器是很不安全的，所以首要做的就是添加新用户，禁止root登录，改变默认端口。

## 第一步：添加新用户，然后设置密码

```
adduser apple
gpasswd -a apple sudo
```

## 第二步：禁止远程root登陆，修改默认端口，限制登陆次数

既然已经有了新用户，所以应该禁止root用户登录，还可以通过修改默认端口22，来达到增加安全性的目的，相关配置文件在`/etc/ssh/sshd_config`里

```
# 默认登陆端口
Port 2334
# 限制登陆次数
MaxAuthTries 10
```

当然，还有更有效的工具，[Fail2Ban](https://www.fail2ban.org/)，相关介绍和使用会在接下来的文章中介绍。
## 第三步：使改变生效

```
# 重启ssh服务
sudo service ssh restart
```
重启之后不要立即登出，先验证修改是否生效。打开一个新的命令行来验证刚才所作的改变。

第四步：使用更加安全的 `ssh_key` 来登陆

这一步不是必需的，只是为了方便和进一步增强安全性。配置ssh_keys之后，当你使用自己的电脑就不用输入密码。
ssh_key 的生成很简单 ，本地输入
```
ssh-keygen
```
这条命令会在 ～/.ssh/ 目录下生成 id_rsa 和 id_rsa.pub，即私钥和公钥。再在本地命令行输入
```
ssh-copy-id apple@SERVER_IP_ADDRESS
```
，然后键入密码，这时就会将本地的公钥添加至服务器 ~/.ssh/authorized_keys 里，里面的内容就是已通过认证的公钥，当你使用这些客户端登录时，就不用输入密码
至此，你的服务器几乎能避免绝大多数攻击，如果要进一步增加安全性，则可向着如下方向改进：

仅使用 ssh_key 登录，禁止普通用户登录
增加防火墙设置，将多次尝试登录的IP地址加入黑名单
添加安全证书的验证

## 参考：

1. [一些增强 SSH 安全性的技巧](https://www.v2ex.com/t/211641)
2. [Advanced SSH security tips and tricks](https://www.linux.com/learn/tutorials/305769-advanced-ssh-security-tips-and-tricks)