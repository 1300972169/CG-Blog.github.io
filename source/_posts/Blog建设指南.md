---
title: Blog建设指南
tags:
  - linux
  - Blog
categories:
  - Blog踩坑日志
description: '---经过2个多月的努力，我的Blog小站终于建设成功了；'
mathjax: true
abbrlink: Blog建设指南
sticky: 2
swiper_index: 2
updated: >-
  2023-05-01 22:00:00
  本博客基于Hexo+Butterfly+GithubPage开发，目前本地服务器部署在阿里云服务器，配套使用阿里云域名解析以及CDN网络加速，旨在记录我的程序猿进阶之路的各种坑
date: 2023-05-01 18:19:03
---
# 1 Hexo

Hexo是一个快速、简洁且高效的博客框架。
首先新建文件夹Blog（名字随意，位置随意）用于存放Hexo本地服务器源码,本文章使用BlogRoot代表博客根目录文件夹

## 1.1 安装node.js

下载地址：[下载 | Node.js 中文网 (nodejs.cn)](https://nodejs.cn/download/)，直接下载最新版本 No Problem
![下载node.js](/assets/image/nodejs-download.png)

检查是否安装成功

```shell
npm -v #输出版本号则安装成功
9.6.4
```
## 1.2 安装git

下载地址：下载地址为 [git-scm.com](git-scm.com)或者[gitforwindows.org](gitforwindows.org)
具体安装流程见 [Git 详细安装教程（详解 Git 安装过程的每一个步骤）](https://blog.csdn.net/mukes/article/details/115693833),一个非常详细的git安装教程，博主是个大佬
`上面的 git-scm 是 Git 的官方，里面有不同系统不同平台的安装包和源代码，而 gitforwindows.org 里只有 windows 系统的安装包`
`阿里镜像直接Ctrl+F 搜索最新版本前缀即可，如2.40.0`
![下载git](/assets/image/git-download.png)

## 1.3 安装Hexo

打开存放博客的根目录文件夹BlogRoot，右键单击空白处展开菜单，点击`Git Bash Here`,打开git终端、
![打开git](/assets/image/blog-deploy01.png)

# 2 Butterfly

# 3 Github Pages

# 4 域名解析

# 5 Vercel

# 6 CDN网络加速

# 7 图床加载
