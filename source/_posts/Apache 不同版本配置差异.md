---
title: Apache 不同版本配置差异
date: 2017-02-16 15:12:10
tags: 技术
---

## 前言
LAMP和WAMP的配置，网上已经有很多很详细的教程了，在此不再赘述。只是在配置Apache时有一点需要注意一下——不同版本的Apache配置不同。我在网上找到的大多中文教程都没有说到上面这一点，结果在因为版本的问题折腾了许久，最后终于从官方文档中找到了答案。

所以寻找问题的思路很重要，应该是查看报错信息 -> 查看错误日记 -> Google -> 官方文档 -> 求助他人，而不是一股脑的就把错误信息copy到搜索引擎中去，这样可能会浪费大量的时间。

下面描述的均是从2.2和2.4配置不同之处，如果是从2.0和2.2，请看参考

## 访问权限的配置

*  拒绝所有访问
```
#2.2 configuration:
Order deny,allow
Deny from all
#2.4 configuration
Require all denied
```

* 允许有来源访问
```
#2.2 configuration:
Order allow,deny
Allow from all
#2.4 configuration
Require all granted
```

* 仅允许特定域名访问
```
#2.2 configuration:
Order Deny,Allow
Deny from all
Allow from example.org
#2.4 configuration
Require host example.org
```

## [Keep-alive](https://en.wikipedia.org/wiki/Keepalive)参数
```
2.2 除了 ‘Off’ 和 ‘0’ 之外的所有值都被当作是 ‘On’
2.4 仅允许 ‘On’ 或 ‘Off’
```
这里只是列出了两个比较常见的配置，更多请参考官方文档。

## 参考
1. [2.0 to 2.2 upgrading document](http://httpd.apache.org/docs/2.2/upgrading.html)
2. [V2EX的Apache节点](https://www.v2ex.com/go/apache)
3. [keep-alive参数详解](https://en.wikipedia.org/wiki/Keepalive)
