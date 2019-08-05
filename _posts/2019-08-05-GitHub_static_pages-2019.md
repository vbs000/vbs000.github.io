---
layout:     post                    # 使用的布局（不需要改）
title:      GitHub静态博客探析              # 标题 
subtitle:   利用github提供的pages，来制作一个静态博客 #副标题
date:       2019-08-05              # 时间
author:     NXY                      # 作者
header-img: img/post-bg-hacker.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Github pages
    - github.io
    - 静态博客
---

## 描述

使用 GITHUB PAGES 搭建自己的静态页面。

## 所有的开始

1.GitHub映射了以这样（${username}.github.io）方式命名的仓库（Repository）。
2.而且，在该仓库的根目录默认以index.html作为首页。

## 什么是jekyll
快速生成静态网页的工具
1.主要结构
> 文件夹_layouts：用于存放模板的文件夹
文件夹_posts：用于存放博客文章的文件夹，里面是markdown格式的文章
文件夹css：存放博客所用css的文件夹
_coinfig.yml：jekyll的配置文件，里面可以定义相当多的配置参数，具体配置参数可以参照其官网
index.html：项目的首页

2.以markdown格式作为文章规范，可以让作者摆脱排版的困扰，专心写作。
