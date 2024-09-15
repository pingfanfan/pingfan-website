---
title: "如何零基础零费用的在30分钟内创建一个专属于你的个人博客"
date: 2022-08-22T17:19:48+01:00
draft: false
author: pingfan
tags: ["Blog", "Hugo","Cloud"]
categories: ["Blog"]
---

<!-- ![fff](https://raw.githubusercontent.com/jzxywpf/pictures/main/tencent/2022-08-13-12-34-19.png) -->


写这篇文章的原因是在网上看了很多的教程，踩了不少的坑，更多的白费了很多功夫，也没找到一篇从头到尾完整有效的个人建站方法。

有些教程年代久远，有些教程极为繁琐，有些教程压根跑不通。

为了方便自己，做个记录，也方便大家，在这个人人都可以发声的时代，又感觉人人的喉咙都被扼住了。

虽然大家在各个媒体平台都有自己的账号，但是给自己留一份自己的自留地，貌似也不会是什么坏事。

这也是我建个人博客的最主要理由，因为有些东西因为这样的或者那样的原因，无法在公域平台发布，那么自己的博客网站，总可以容纳的下。

# 建立个人博客的两个方法

这是一套非常简单的方法，我希望可以让每一个人都可以照着这套方法建立自己的博客。

总共分为两个版本：

第一个版本为通用版本，利用云服务器的host功能，一个月仅需要花费一杯咖啡的钱。

第二个版本为github版本，利用github pages的免费host和自动部署功能，不需要花一分钱就可以拥有自己的博客。


<!-- 视频版本：
{{< bilibili id=BV1514y1s7o7 >}} -->


## 前置准备

### Mac 和 linux

需要：homebrew，git包管理，Node.js, vscode(推荐)

&nbsp;

homebrew安装：直接命令行输入
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
&nbsp;

git包管理：直接命令行输入
```bash
brew install git
```
&nbsp;

Node.js: 下载安装包后按照默认设置安装

[Node.js下载链接](https://nodejs.org/en/download/)


### Windows

需要：git包管理，hugo预编译文件，Node.js, vscode(推荐)

&nbsp;

git包管理：点击下面链接下载后安装

[git包管理下载链接](https://github.com/git-for-windows/git/releases/download/v2.37.2.windows.2/Git-2.37.2.2-64-bit.exe)

&nbsp;

Node.js: 下载安装包后按照默认设置安装

[Node.js下载链接](https://nodejs.org/en/download/)

## 准备 hugo 环境

我们用hugo来写个人博客，它是一个非常快捷和友好的博客框架。

### mac 安装方法：命令行种输入

```bash
brew install hugo
```
### Windows安装方法

比mac要麻烦点，但是安装方法很详细。

[windows版本的安装方法](https://www.gohugo.org/doc/tutorials/installing-on-windows/)


## 学会在命令行中创建blog 

{{< admonition title = "注意！" open = true >}} 
  每一步命令输入后按「回车键」 
{{< /admonition >}}

windows：在搜索栏中输入cmd或者命令行

mac：找到Terminal


{{< admonition type=tip title="正文正式开始" open=true >}}
使用hugo创建一个blog项目
{{< /admonition >}}


### 创建一个新的blog

使用命令`hugo new site`来创建一个博客，pingfan-blog这个名字可以根据自己的需要改

```bash
hugo new site pingfan-blog
```
### 进入刚刚创建好的博客文件夹中

在命令行中使用`cd`命令
```bash
cd pingfan-blog
```

### 给博客加个皮肤，一次复制+粘贴三行代码到命令行中

第一行：把当前目录进行**github仓库**的初始化
```bash
git init  
```

第二行：下载anatole主题，并存放在themes文件夹中
```bash
git submodule add https://github.com/lxndrblz/anatole.git themes/anatole  
```

第三行：把主题改为anatole

```bash
echo theme = "anatole" >> config.toml
```
{{< admonition type = tip title = "这步看不懂的话可以打开文件修改" >}} 
  不会的话可以在文件中打开config.toml文件，手动添加 
{{< /admonition >}}



### 写第一篇blog

`hugo new` + aaa/bbb.md， aaa指代的是某一个文件夹，如果你想写美食和电影两种，那就是[美食/第一篇美食.md]，或者[电影/第一篇电影.md]，尽量都用字母，其次一定要加.md
```bash
hugo new life/first_day.md
```
### 运行下博客看是否可行
```bash
hugo server
```
出现以下界面后，打开任意浏览器，输入http://localhost:1313 即可查看。

![hugo server成功](https://raw.githubusercontent.com/jzxywpf/pictures/main/zero-experience/1662237136915.jpg)

{{< admonition type = question title = "上述网址打不开" >}} 
  一般是因为1313端口被占用了，可以用它生成的别的网址；或者用`kill -9 $(lsof -ti:1313)`在命令行把1313端口重新释放出来
{{< /admonition >}}

浏览器中出现如下界面说明你成功了

{{< figure src="https://raw.githubusercontent.com/jzxywpf/pictures/main/zero-experience/blog-preview.png" title="博客预览图" >}}

<!-- ![网站预览图](https://raw.githubusercontent.com/jzxywpf/pictures/main/zero-experience/blog-preview.png) -->

### 生成静态文件，准备进一步托管
```bash
hugo -D
```
你可以去自己的文件目录中看到，public文件夹里面已经多了很多文件出来。


## 静态网站托管服务

使用云服务进行托管，这一步针对是不能访问github的同学，那么你必须得用一款云服务器进行托管。

### 1. 首先你得有一个云服务空间，这里我使用的是腾讯云的cloudbase

这里我使用的是腾讯云的cloudbase，可以通过下面这个链接，选择新用户体验券后可以免费体验一个月。

[腾讯云cloudbase免费试用一个月链接](https://curl.qcloud.com/ywYsIFMs)

添加成功后点击【控制台->云产品->cloudbase】，点开可以看到如下内容。


{{< figure src="https://pic4.zhimg.com/80/v2-e19943a4ac2bfae28ffd8e1f272cf985_720w.png?source=d16d100b" title="cloudbase云产品" >}}

### 2. 创建好后得到了一个**环境ID**，待会儿要用到

{{< figure src="https://pica.zhimg.com/80/v2-f768a5cd959a106df3281e315f52f964_720w.png?source=d16d100b" title="环境ID" >}}

### 3. 在本地安装Node.js

网址为：https://nodejs.org/en/  windows和mac按类型下载，下载完成后安装即可。

在命令行中输入以下验证是否安装成功

```bash
npm -v
```

出现类似于6.14.13就表示成功了。

### 4. 打开命令行，输入以下命令安装 cloudbase cli
```bash
npm install -g @cloudbase/cli
```
### 5. 登录云开发
```bash
tcb login
```
### 6. 在弹出的页面中单击**确认授权**进行授权

{{< figure src = "https://pic2.zhimg.com/80/v2-bdfc3508a5a012a987c8ea8a77fd8015_720w.png" >}}

### 7. 执行以下命令，把public文件夹部署到云服务器上（把EnvID换成刚刚的**环境ID**）
```bash
cloudbase hosting deploy ./public  -e EnvID
```
### 8.登录云开发控制台

进入静态网站托管页面，可以找到默认的域名，单击域名，就可以看到你的博客已经部署成功了。


{{< figure src="https://pica.zhimg.com/80/v2-08aa7b7b349d2c99e90193367312a180_720w.png?source=d16d100b" title="腾讯云控制台" >}}


下面就是自动生成的域名


{{< figure src="https://pic1.zhimg.com/80/v2-ce0768eca6594f551b366d8a82a129d9_720w.png?source=d16d100b" title="自动生成的域名" >}}


出现如下界面表明创建成功了

{{< figure src="https://pic1.zhimg.com/80/v2-a1be93cb8f24f4604de820a1a77193dc_720w.png?source=d16d100b" title="成功了！" >}}


## 使用Github进行托管

这个方法是给可以访问github的同学准备的，首先你需要新建一个github仓库，名字无所谓。

然后在命令后中进行操作

### 1.在 命令行中进行git初始化
这步我们已经做过了，当然了，再做一次也没关系
```bash
git init
```
### 2. 检查是否有改变
```bash
git status
```
### 3. 提交到暂存区 
```bash
git add .
```
### 4. 交到版本库
```bash
git commit -m "msg"
```
### 5. 创建分支

```bash
git branch -M main
git remote add origin https://.....git
```
<!-- git submodule add https://github.com/josephhutch/aether themes/aether  -->


### 6. 推送到远程仓库
```bash
git push -u origin main
```

### 7. 添加gh-pages.yml文件

新建一个文件，在pingfan-blog目录下，名称为**.github**,然后在.github文件夹下新建一个文件夹**workflows**，在workflows文件夹下新建一个文件叫**gh-pages.yml**

总的路径为***pingfan-blog/.github/workflows/gh-pages.yml***

在gh-pages.yml输入以下内容后保存。

```yaml
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
```


### 8. 重新把修改过的文件上传到github上

再走一遍
```bash
git status 
git add .
git commit -m "add yml file"
git push
```
### 9. 成功的话，我们会发现所有的内容都上传到github了

### 10. 找到刚刚的github仓库，点击Actions，就可以看到我们的网站部署成功了

{{< figure src= "https://pic1.zhimg.com/80/v2-14b67e4a795309a717df6d0d8caf20a4_720w.png?source=d16d100b" title="博客由github自动部署了" >}}

### 11. 修改branch为gh-pages，位置在settings->Pages那里


{{< figure src ="https://pic1.zhimg.com/80/v2-2a00d39f27c447842115820e092df084_720w.png?source=d16d100b"  >}}
### 11. 最后一步，修改hugo的baseURL

在github的仓库中找到Settings->Pages，找到为https://******.github.io/pingfan-blog 

{{< figure src = "https://pic3.zhimg.com/80/v2-ab3c0e5a5b7da0e9d0cd8d90bc55497a_720w.png?source=d16d100b" >}}
复制粘贴，打开config.toml，然后替换掉原先的。
{{< figure src = "https://pica.zhimg.com/80/v2-6fa10f8b021e5d9c7ec7af3ac52aa5d7_720w.png?source=d16d100b">}}
### 12. 再走一遍

```bash
git status 
git add .
git commit -m "revise config"
git push
```

### 13. 打开github，点开pages，点击sourse，选择gh-pages，结束

我这个是换成了我自己购买的域名，所以会显示的不一样，你也可以买一个自己喜欢的域名，而不是默认的域名。
{{< figure src = "https://picx.zhimg.com/80/v2-4d3a3c89c06778c80ff39fac9bc2fc5c_720w.png" >}}

这是我的[域名](https://www.pingfan.me)。


如果有问题，可以加这个群，有空我会看的。
群号：339309252
或者扫这个：[QQ群](https://raw.githubusercontent.com/jzxywpf/pictures/main/zero-experience/IMG_3980.JPG)




