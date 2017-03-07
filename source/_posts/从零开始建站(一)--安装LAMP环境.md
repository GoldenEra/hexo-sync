---
title: 从零开始建站(一)--安装LAMP环境
date: 2017-02-16 11:47:04
tags: 技术
---
## 关于VPS

可以将VPS理解为一台在世界某个角落的一台电脑，这台电脑上操作系统，配置都可以通过命令行（Linux系统）或界面（Windows系统）来完成，唯一和你手边电脑不同的是不能通过眼睛看到，手摸到。下面只针对世界上大部分使用的Linux服务器来说明如何远程操控这台“电脑”。

当你从VPS服务商（DIgitalOcean，Conhon，Lindo，搬瓦工）购买了一台虚拟主机之后，如何通过一步步的配置，使之成为一个能被正常访问的网站呢？Let’s try it step by step!

VPS提供商：Digitalocean
服务器环境：Ubuntu 12.04.5 x64
服务器配置：512MB Ram | 20GB SSD Disk | San Francisco
客户端：Windows7 旗舰版
目的：配置LAMP环境

## 关于LAMP

LAMP是一组用来搭建网站或者服务器的开源软件，他们本身都是独立的软件，LAMP则是Linux，Apache，MySQL，PHP的首字母缩写，因为我们使用的Ubuntu正是Linux的一个发行版，所以接下来只需要安装Apache，MySQL和PHP.

## 第一步：下载命令行客户端

由于Windows系统自带的命令行界面并不支持ssh命令，故需先下载一个命令行客户端，putty，Git都可。

## 第二步：登录VPS

打开命令行客户端，输入ssh root@SERVER_IP_ADDRESS, SERVER_IP_ADDRESS 是指你购买的VPS给你分配的IP，可以在VPS提供商的后台管理查到。然后再键入密码,服务商一般会发送root密码到邮箱，即可登录远程“电脑”。以下的所有操作都是在登录之后进行的。

## 第三步：安装Apache

Apache是一个免费、开源的网络服务器，键入如下两条命令安装Apache

更新软件源

    sudo apt-get update

安装Apache

    sudo apt-get install apache2
安装完之后在浏览器地址栏键入你的IP地址，若出现，即表明安装成功。So easy!

## 第四步：安装MySQL

MySQL也是一个免费、开源的数据库，继续在命令行键入如下命令

安装MySQL和相关组件

    sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql

之后就会出现设置root密码，直接enter则密码为空

## 第五步：安装PHP

PHP是一门开源的网络脚本语言，通过如下命令安装PHP

    sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt

PHP还有许多的扩展模块，通过他们可以实现很多其他功能，极大增强了语言的可扩展性。

## 第六步：安装PHP扩展

通过命令`apt-cache search php5-`可以搜索到所有模块，然后按需安装。

    php5-cgi - server-side, HTML-embedded scripting language (CGI binary)
    php5-cli - command-line interpreter for the php5 scripting language
    php5-common - Common files for packages built from the php5 source
    php5-curl - CURL module for php5
    php5-dbg - Debug symbols for PHP5
    php5-dev - Files for PHP5 module development
    php5-gd - GD module for php5
    php5-gmp - GMP module for php5
    php5-ldap - LDAP module for php5
    php5-mysql - MySQL module for php5
    php5-odbc - ODBC module for php5
    php5-pgsql - PostgreSQL module for php5
    php5-pspell - pspell module for php5
    php5-recode - recode module for php5
    php5-snmp - SNMP module for php5
    php5-sqlite - SQLite module for php5
    php5-tidy - tidy module for php5
    php5-xmlrpc - XML-RPC module for php5
    php5-xsl - XSL module for php5
    php5-adodb - Extension optimising the ADOdb database abstraction library
    php5-auth-pam - A PHP5 extension for PAM authentication

## 第七步：查看phpinfo

    sudo nano /var/www/info.php

添加如下代码

    <?php
    phpinfo();
    ?>

保存后退出。重启服务器

    sudo service apache2 restart

在浏览器地址栏键入SERVER_IP_ADDRESS/info.php 查看是否为如下信息

至此，LAMP环境基本搭建完毕。下面一节将讲如何配置虚拟主机。
