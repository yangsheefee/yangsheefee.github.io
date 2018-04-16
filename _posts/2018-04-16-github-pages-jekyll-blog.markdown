---
layout: post
title:  "使用Jekyll搭建GitHub Pages博客"
date:   2018-04-16 14:07:45 +0800
categories: tips
---
<h1>什么是GitHub Pages</h1>

<h1>什么是Jekyll</h1>

[Jekyll官网](https://jekyllrb.com/)有一条非常醒目的介绍

>Transform your plain text into static websites and blogs.

意思就是将纯文本转换成静态博客网站

<h1>搭建运行环境</h1>

Jekyll运行在`Ruby`环境，因此首先需要安装`Ruby`，从[Ruby官网](https://rubyinstaller.org/downloads/)下载最新版本的安装包，点击安装，只要注意安装目录没有空格，其他默认就好，比如我的安装目录`C:\Jekyll\Ruby\Ruby25-x64`。

然后打开`CMD`使用`Ruby`的`gem`命令安装`jekyll`和`bundle`
```
gem install jekyll
gem install bundle
```

<h1>创建博客目录</h1>

打开`CMD`进入到指定目录，创建博客
```shell
PS C:\Windows\system32> cd C:\Jekyll\Pages\
PS C:\Jekyll\Pages> jekyll new Jekyll
```
创建的目录结构如下
![1](/images/2018/04/16/1.png)

其中_posts目录存放的就是博客文章，通过在本地运行Jekyll可以预览博客效果
```shell
PS C:\Windows\system32> cd C:\Jekyll\Pages\Jekyll\
PS C:\Jekyll\Pages\Jekyll> jekyll s
Configuration file: C:/Jekyll/Pages/Jekyll/_config.yml
            Source: C:/Jekyll/Pages/Jekyll
       Destination: C:/Jekyll/Pages/Jekyll/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.42 seconds.
 Auto-regeneration: enabled for 'C:/Jekyll/Pages/Jekyll'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

<h1>同步发布博客</h1>

建立一个`username.github.io`（username换成你的GitHub ID）的`repository`，将该仓库pull至本地，拷贝Jekyll目录结构至此，再push至GitHub

<h1>绑定独立域名</h1>

首先，注册一个域名，例如[万网](https://wanwang.aliyun.com/)

然后，在仓库根目录创建CNAME文件，没有后缀，一定要大写，里面只有一行，就是你的域名

最后，找一个DNS解析服务提供方，例如[DNSPod](https://www.dnspod.cn/)，建立域名与`username.github.io`之间的联系，方法是在域名解析中添加两条记录

主机记录 | 记录类型 | 记录值
----- | ----- | -----
@ | CNAME | username.github.io
www | CNAME | username.github.io

等十几分钟就生效了

<h1>更换博客主题</h1>

<h1>添加站点图标</h1>

只需要在根目录添加一个名为`favicon.ico`的文件

<h1>添加搜索功能</h1>

<h1>添加评论功能</h1>
