---
abbrlink: ''
categories:
- - 部署
date: '2024-04-11T10:59:07.289692+08:00'
tags:
- nginx
- onlyoffice
title: nginx与onlyoffice
updated: '2025-07-23T08:36:57.666+08:00'
---
> 背景：客户需要在浏览器里直接浏览word，对于一个使用java的项目来说难以实现。但是如果你知道onlyoffice的话一切都将迎刃而解（噩梦开端）。

我不准备介绍`onlyoffice`怎么用，因为我也不会用，我要介绍的是`onlyoffice`与`nginx`共同使用时的一个特殊情况，希望你永远也用不到。

<!-- more -->

## 网络环境

首先我要先介绍一下客户的网络环境：
有这样的几个服务器：
A 配置https、证书的服务器，这台服务器我们接触不到，所以以下配置将不涉及
B 负载均衡服务器，监听80端口，将请求代理到C/D上
C、D 部署前端同时代理E/F
E、F 部署后端

由于一些原因我在E上使用docker部署了onlyoffice 端口是4321，现在我们要配置代理到onlyoffice

## 配置nginx

```conf
location /onlyoffice/ {
    proxy_pass http://E:4321/;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection upgrade;
    proxy_set_header X-Forwarded-Host 域名/onlyoffice;
    proxy_set_header X-Forwarded-Proto https;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```
