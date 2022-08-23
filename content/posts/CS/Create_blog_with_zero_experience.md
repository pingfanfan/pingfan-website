---
title: "Create_blog_with_zero_experience"
date: 2022-08-22T17:19:48+01:00
draft: false
---

![fff](https://raw.githubusercontent.com/jzxywpf/pictures/main/tencent/2022-08-13-12-34-19.png)


写这篇文章的原因是在网上看了很多的教程，踩了不少的坑，更多的白费了很多功夫，也没招到一篇从头到尾完整有效的个人建站方法。

有些教程年代久远，有些教程极为繁琐，有些教程压根跑不通。

为了方便自己，做个记录，也方便大家，在这个人人都可以发声的时代，又感觉人人的喉咙都被扼住了。

虽然大家在各个媒体平台都有自己的账号，但是给自己留一份自己的自留地，貌似也不会是什么坏事。

这也是我建个人博客的最主要理由，因为有些东西因为这样的或者那样的原因，无法在公域平台发布，那么自己的博客网站，总可以容纳的下。

# 建立个人博客的流程

这是一套非常简单的方法，我希望可以让每一个人都可以照着这套方法建立自己的博客。

总共分为两个版本：

第一个版本为通用版本，利用云服务器的host功能，一个月仅需要花费一杯咖啡的钱。

第二个版本为github版本，利用github的免费host功能，不需要花一分钱就可以拥有自己的博客。

# 总体流程图


# 前置准备

## 准备 hugo 环境

我们用hugo来写个人博客

windows：https://www.gohugo.org/doc/tutorials/installing-on-windows/

mac os：'brew install hugo' 

## 学会在命令行中创建blog （注意每一步命令输入后按「回车键」）

windows：在搜索栏中输入cmd或者命令行

mac：找到Terminal

## 使用hugo创建一个blog项目

1. hugo new site 功能来创建一个新的blog，pingfan-blog这个名字可以根据自己的需要改

hugo new site pingfan-blog

2. cd pingfan-blog 进入刚刚创建好的博客地址中

cd pingfan-blog

3. 给博客加个皮肤，一次复制+粘贴三行代码到命令行中

第一行：把当前目录进行初始化

git init  

第二行：下载ananke主题，并存放在themes文件夹中

git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke  

第三行：把主题改为annake

echo 'theme = "ananke"' >> config.toml

4. 写第一篇blog

hugo new + aaa/bbb.md， aaa指代的是某一个文件夹，如果你想写美食和电影两种，那就是[美食/第一篇美食.md]，或者[电影/第一篇电影.md]，尽量都用字母，其次一定要加.md

hugo new life/first_day.md

5. 运行下博客看是否可行

hugo server

出现以下界面后，打开任意浏览器，输入http://localhost:1313 即可查看。

浏览器中出现如下界面说明你成功了

6. 生成静态文件，准备进一步托管

hugo -D

你可以去自己的文件目录中看到，public文件夹里面已经多了很多文件出来。


# 静态网站托管服务

## 使用云服务进行托管

1. 首先你得有一个云服务空间，这里我使用的是腾讯云的cloudbase

2. 创建好后得到了一个**环境ID**，待会儿要用到

3. 在本地安装Node.js

网址为：https://nodejs.org/en/  windows和mac按类型下载，下载完成后安装即可。

在命令行中输入以下验证是否安装成功

npm -v

出现类似于6.14.13就表示成功了。

4. 打开命令行，输入以下命令安装 cloudbase cli

npm install -g @cloudbase/cli

5. 登录云开发

tcb login

6. 在弹出的页面中单击**确认授权**进行授权：

7. 执行以下命令，把public文件夹部署到云服务器上（把EnvID换成刚刚的**环境ID**）

cloudbase hosting deploy ./public  -e EnvID

8. 登录云开发控制台，进入静态网站托管页面，可以找到默认的域名，单击域名，就可以看到你的博客已经部署成功了。







## 使用github进行托管
准备一个github 仓库



1. 在命令行中进行git 初始化

git init

2.  检查是否有改变

git status

3. git add .

4. git commit -m "msg"

5. git submodule add https://github.com/josephhutch/aether themes/aether 

6. git branch -M main

7. git remote add origin https://.....git

8. git push -u origin main

9. 新建一个文件，在pingfan-blog目录下，名称为.github,然后在.github文件夹下新建一个文件夹workflows，在workflows文件夹下新建一个文件叫gh-pages.yml

总的路径为pingfan-blog/.github/workflows/gh-pages.yml

在gh-pages.yml输入以下内容后保存。

name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public



10. 因为我们新建了文件，所以我们要把所有的文件都上传到github中。

再走一遍

git status 
git add .
git commit -m "add yml file"
git push

11. 成功的话，我们会发现所有的内容都上传到github了

12. 找到刚刚的github仓库，点击Actions，就可以看到我们的网站部署成功了。

13. 最后一步，修改hugo的baseURL。

在github的仓库中找到Settings->Pages，找到为https://******.github.io/pingfan-blog 

复制粘贴，打开config.toml，然后替换到原先的。

14. 再走一遍

15. 打开github，点开pages，点击sourse，选择gh-pages，结束。

以后再写东西都重新走一遍git流程就好了。




