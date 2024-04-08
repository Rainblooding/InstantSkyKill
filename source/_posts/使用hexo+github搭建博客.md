---
abbrlink: ''
categories:
- - 搭建
date: '2024-04-08T14:35:41.747760+08:00'
tags:
- hexo
title: 使用hexo搭建博客
updated: '2024-04-08T14:45:20.902+08:00'
---
## 安装hexo

### 安装前提

在安装hexo前需要先安装一下软件:

* Node.js(version>=10.13)
* Git

### 安装Hexo

所有必备的应用程序安装完成后,即可使用npm安装Hexo

```bash
npm insatll -g hexo-cli
```

## 建站

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```bash
hexo init <folder>
cd <folder>
npm install
```

新建完成后，指定文件夹的目录如下:

```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### 使用Hexo

使用hexo命令创建文章

```bash
hexo new test_my_site
```

生成并预览

```bash
hexo g
hexo s
```

打开浏览器输入地址[预览地址](http://localhost:4000)

#### Hexo常用命令

现在来介绍常用的Hexo 命令

```
npm install hexo -g #安装Hexo
npm update hexo -g #升级
hexo init #初始化博客
```

命令简写

```
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
```
