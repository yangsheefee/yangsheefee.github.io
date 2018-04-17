---
layout: post
title:  "搭建基于Jekyll与GitHub的博客平台"
date:   2018-04-17 01:19:28 +0800
categories: tips
description: "搭建基于Jekyll与GitHub的博客平台"
keywords: jekyll, github
---
<h1>一、什么是GitHub Pages</h1>

[Github Pages](https://pages.github.com/)是GitHub官方提供的用于个人博客或项目介绍的网站工具
>Websites for you and your projects.

用GitHub Pages搭建个人博客也是非常之容易，下面先简单介绍一下。

首先，得有个GitHub账号，这毫无疑问，创建一个名为`username.github.io`（username换成你GitHub的ID）的repository，Description、README、gitignore、license这些都可以不要，重点是这个仓库的名称。

然后，进入该仓库，点击`Create new file`按钮，添加文件`index.html`，内容只有一行
```
Hello,GitHub Pages!
```

浏览器访问`username.github.io`这个域名，就可以看到`Hello,GitHub Pages!`，`username.github.io`成了一个网站，这就是GitHub Pages，这就是你的博客！

接下来介绍的内容只是为了丰富这个站点，使用其他辅助工具如[Jekyll](https://jekyllrb.com/)更好的在该站点发表文章，至于为什么要用Jekyll？因为GitHub Pages官方用这个。除此之外，[hexo](https://hexo.io/)也是不错的选择。

<h1>二、为GitHub Pages绑定独立域名</h1>

可能你对这个站点域名`username.github.io`不满意，没关系，官方提供了绑定独立域名的功能，设置起来也很简单。当然，如果你不在意域名，请跳过该标题。

首先，有一个可用的域名，如果没有，请注册一个，国内域名注册服务商可以选择阿里巴巴的[万网](https://wanwang.aliyun.com/)

然后，在`username.github.io`仓库根目录创建CNAME文件，注意：没有后缀、一定要大写，文件内容只有一行，就是你的域名。

最后，找一个DNS解析服务提供方，例如[DNSPod](https://www.dnspod.cn/)（免费、快速、可靠），将你的域名添加进来，注意不要带www，只要域名，然后在域名解析中添加两条CNAME记录

主机记录 | 记录类型 | 记录值
----- | ----- | -----
@ | CNAME | username.github.io
www | CNAME | username.github.io

等十几分钟就生效了，可以用新的域名访问原先的GitHub Pages了。

也有人说先用ping的方式拿到`username.github.io`的IP地址，然后添加A记录，但GitHub官方给`username.github.io`分配的IP可能会变，这种方式不可靠！

<h1>三、Jekyll简介</h1>

[Jekyll官网](https://jekyllrb.com/)有一条非常醒目的介绍

>Transform your plain text into static websites and blogs.

你可以将Jekyll理解成一个工具，用于将使用Markdown语法（或Textile语法）编写的文件和其他复杂样式组成的内容解析为仅仅有html、javascript、css等文件组成的静态网站，没有数据库，没有其他多余的东西，只有你写的内容。

<h1>四、Jekyll环境</h1>

Jekyll运行在`Ruby`环境，因此首先需要安装`Ruby`，从[Ruby官网](https://rubyinstaller.org/downloads/)下载最新版本的安装包如`rubyinstaller-devkit-2.5.1-1-x64.exe`，双击安装
![2](/assets/images/2018/04/17/2018-04-17_131210.png)

注意安装目录没有空格，其他默认，到最后一步`ridk install`那里，取消勾选（实际上勾选了也没影响），然后点击`Finish`，这样`Ruby`就安装好了。

从[git官网](https://git-scm.com/)下载git客户端，双击安装，一路默认直到完成，打开`Git Bash`，接下来使用`Git Bash`代替`CMD`命令行来操作，之后的GitHub操作也是用`Git Bash`。

使用`Ruby`的`gem`命令安装`jekyll`
```
$ gem install jekyll
Successfully installed public_suffix-3.0.2
...
Done installing documentation for public_suffix, addressable, colorator, http_parser.rb, eventmachine, em-websocket, concurrent-ruby, i18n, rb-fsevent, ffi, rb-inotify, sass-listen, sass, jekyll-sass-converter, ruby_dep, listen, jekyll-watch, kramdown, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, jekyll after 18 seconds
25 gems installed
```
安装管理`jekyll`插件的`bundle`
```
$ gem install bundle
Successfully installed bundler-1.16.1
Successfully installed bundle-0.0.1
Parsing documentation for bundler-1.16.1
Installing ri documentation for bundler-1.16.1
Parsing documentation for bundle-0.0.1
Installing ri documentation for bundle-0.0.1
Done installing documentation for bundler, bundle after 3 seconds
2 gems installed
```

<h1>五、Jekyll使用</h1>

打开Git Bash，运行以下命令，在指定目录创建一个全新的基于Jekyll的博客目录
```
$ cd /c/Programmer/Ruby/Jekyll/

$ jekyll new jekyllpg
Running bundle install in C:/Programmer/Ruby/Jekyll/jekyllpg...
  Bundler: Fetching gem metadata from https://rubygems.org/............
  ...
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in C:/Programmer/Ruby/Jekyll/jekyllpg.
```
创建的目录结构如下
```
John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll/jekyllpg
$ ls -a -l
total 20
drwxr-xr-x 1 John 197121    0 4月  17 13:17 ./
drwxr-xr-x 1 John 197121    0 4月  17 13:20 ../
-rw-r--r-- 1 John 197121   35 4月  17 13:17 .gitignore
-rw-r--r-- 1 John 197121 1652 4月  17 13:17 _config.yml
drwxr-xr-x 1 John 197121    0 4月  17 13:17 _posts/
-rw-r--r-- 1 John 197121  398 4月  17 13:17 404.html
-rw-r--r-- 1 John 197121  539 4月  17 13:17 about.md
-rw-r--r-- 1 John 197121 1069 4月  17 13:17 Gemfile
-rw-r--r-- 1 John 197121 1877 4月  17 13:17 Gemfile.lock
-rw-r--r-- 1 John 197121  213 4月  17 13:17 index.md
```
* _posts 存放博客文章
* _config.yml 是Jekyll解析用的配置文件
* Gemfile 记录当前目录使用的gem插件
* index.md 用于生产index.html主页
* 404.html 404页面

这个博客可以直接在本地运行了
```
John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll/jekyllpg
$ bundle exec jekyll s
Configuration file: C:/Programmer/Ruby/Jekyll/jekyllpg/_config.yml
            Source: C:/Programmer/Ruby/Jekyll/jekyllpg
       Destination: C:/Programmer/Ruby/Jekyll/jekyllpg/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.423 seconds.
 Auto-regeneration: enabled for 'C:/Programmer/Ruby/Jekyll/jekyllpg'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```
在Generating的过程中，会生成一个_site目录，里面就是真正的网站内容，html、js、css等文件，这就是Jekyll解析的过程，此时，浏览器访问效果如下
![1](/assets/images/2018/04/17/2018-04-17_133217.png)
这个博客就在本地生成了，有固定的样式、目录等等。

<h1>六、发布到GitHub Pages</h1>

虽然本地运行的有模有样了，但，GitHub上那个仓库还是只有一个`index.html`呢！

在此之前，让我们先设置git客户端，将其与远程GitHub关联并授权。

打开Git Bash，运行
```
ssh-keygen -t rsa -C "yourname@xxx.com"
```
回车，输入`yes`，再回车，将在`C:\Users\John\.ssh\id_rsa.pub`文件生成ssh密钥，打开该文件，复制所有内容

登录github，打开“Settings”，点击左侧“SSH and GPG keys”菜单，然后点击右侧上方“New SSH key”按钮，“Title”随意输入名称，“Key”处粘贴刚才复制的密钥，注意最后不要留空格或换行，保存配置

打开git bash，输入以下内容验证ssh连接
```
ssh -T git@github.com
```
第一次需要输入`yes`然后回车才能看到连接成功的信息，以后就不需要了，然后，配置全局的用户名、邮箱信息，作为提交人信息
```
git config --global user.name "yangsheefee"
git config --global user.email "yangsheefee@gmail.com"
```
OK，Git客户端配置完成。

在本地创建一个目录（文件夹），就叫`GitHubPages`吧！进入该目录，将GitHub仓库内容pull下来，包括那个index.html文件
```
John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll/GitHubPages
$ git init
Initialized empty Git repository in C:/Programmer/Ruby/Jekyll/GitHubPages/.git/

John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll/GitHubPages (master)
$ git remote add origin git@github.com:yangsheefee/yangsheefee.github.io.git

John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll/GitHubPages (master)
$ git pull origin master
remote: Counting objects: 56, done.
remote: Compressing objects: 100% (37/37), done.
remote: Total 56 (delta 13), reused 47 (delta 7), pack-reused 0
Unpacking objects: 100% (56/56), done.
From github.com:yangsheefee/yangsheefee.github.io
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
```
将本地博客目录，就是成功运行了的那个目录，拷贝过来，执行add、commit与push操作
```
git add ./*
git commit -m "comment"
git push -u origin master
```
这样就将本地文件上传到GitHub Pages那个仓库了，访问`username.github.io`域名，就能看到新内容啦！

<h1>七、自定义网站图标</h1>

在`username.github.io`仓库的根目录添加一个名为`favicon.ico`的文件，如果没有ico图标，可以上传一张图片到[比特虫](http://www.bitbug.net/)在线做一个，刷新下页面就能看到图标了！

<h1>八、更换Jekyll主题</h1>

Jekyll更换主题不是特别简单，但也并不是很复杂，只是没有文档说明，让人莫名其妙。

当你看到一个漂亮的Jekyll主题，把它下载到本地，解压，要做的最重要的事是安装这个主题需要的插件，不然本地是运行不了的，把博客的内容就是包含_posts等文件的那个目录的内容拷贝过来，然后进入到这个主题的根目录
```
John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll/jekyllui (master)
$ bundle install
Fetching gem metadata from https://rubygems.org/............
Fetching gem metadata from https://rubygems.org/..
Resolving dependencies...
Using concurrent-ruby 1.0.5
...
Bundle complete! 1 Gemfile dependency, 85 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
Post-install message from nokogiri:
Nokogiri is built with the packaged libraries: libxml2-2.9.7, libxslt-1.1.32, zlib-1.2.11, libiconv-1.15.
Post-install message from html-pipeline:
-------------------------------------------------
Thank you for installing html-pipeline!
You must bundle Filter gem dependencies.
See html-pipeline README.md for more details.
https://github.com/jch/html-pipeline#dependencies
-------------------------------------------------
```
然后试着运行
```
bundle exec jekyll s
```
如果没报错，就行了。

另外，Jekyll可以生成空白主题（就是平铺的那种，啥样式都没），可以用来设计一个全新的主题
```
John@DESKTOP-IIQH3FK MINGW64 /c/Programmer/Ruby/Jekyll
$ jekyll new-theme jekyllui
             create C:/Programmer/Ruby/Jekyll/jekyllui/assets
             create C:/Programmer/Ruby/Jekyll/jekyllui/_layouts
             create C:/Programmer/Ruby/Jekyll/jekyllui/_includes
             create C:/Programmer/Ruby/Jekyll/jekyllui/_sass
             create C:/Programmer/Ruby/Jekyll/jekyllui/_layouts/page.html
             create C:/Programmer/Ruby/Jekyll/jekyllui/_layouts/post.html
             create C:/Programmer/Ruby/Jekyll/jekyllui/_layouts/default.html
             create C:/Programmer/Ruby/Jekyll/jekyllui/Gemfile
             create C:/Programmer/Ruby/Jekyll/jekyllui/jekyllui.gemspec
             create C:/Programmer/Ruby/Jekyll/jekyllui/README.md
             create C:/Programmer/Ruby/Jekyll/jekyllui/LICENSE.txt
         initialize C:/Programmer/Ruby/Jekyll/jekyllui/.git
             create C:/Programmer/Ruby/Jekyll/jekyllui/.gitignore
Your new Jekyll theme, jekyllui, is ready for you in C:/Programmer/Ruby/Jekyll/jekyllui!
For help getting started, read C:/Programmer/Ruby/Jekyll/jekyllui/README.md.
```
把它拷贝到博客目录，修改Gemfile文件
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```
然后执行
```
bundle install
bundle exec jekyll s
```
就可以本地运行了