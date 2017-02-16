---
title: 从零开始建站(二)--VirtualHost的配置
date: 2017-02-16 11:49:23
tags: 技术
---

## 前言

当LAMP环境搭建好之后，已经能通过ip地址访问到默认的index.html页面了，默认网站根目录是/var/www，在从零开始建站（一）– 安装LAMP环境 最后直接访问IP就是访问的该目录。但是，为了方便管理，一般为每个站都单独建一个目录，一个配置文件。

## 第一步：新建目录

在`/var/www`新建目录
新建目录

    sudo mkdir -p /var/www/mysite.com
给予访问权限

    sudo chown -R $USER:$USER /var/www/mysite.com
## 第二步：新建test page

    vi /var/www/mysite.com/index.html
输入以下内容

    <html>
      <head>
        <title>Welcome to mysite.com!</title>
      </head>
      <body>
        <h1>Success!  The example.com virtual host is working!</h1>
      </body>
    </html>

## 第三步：针对每一个网站增加一个虚拟配置文件
复制默认的配置文件
    
    cp /etc/apache2/site-available/default /etc/apache2/site-available/mysite.com

编辑配置文件

    vi mysite.com.conf 

建议的配置文件内容

    <VirtualHost *:80>
        ServerAdmin yourEmail@gmail.com
        ServerName www.yoursite.com
        DocumentRoot /var/www/example.com
        ErrorLog ${APACHE_LOG_DIR}/mysite.com/error.log
        CustomLog ${APACHE_LOG_DIR}/mysite.com/access.log
    </VirtualHost>

## 第四步：激活配置文件
激活配置文件

    sudo a2ensite mysite.com.conf
重启apahce

    sudo service apache2 restart

## 参考：
(How To Set Up Apache Virtual Hosts on Ubuntu 14.04 LTS)[https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts]