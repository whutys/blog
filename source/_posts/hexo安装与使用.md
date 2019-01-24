---
title: hexo安装与使用
type: categories
copyright: true
date: 2019-01-10 19:06:57
categories: 软件安装使用
tags: hexo
---
## 使用环境（Windows）
1.node.js 官网点[这里](https://nodejs.org/)

2.Git 官网点[这里](https://git-scm.com/)

## 安装Hexo
命令行 cmd 或 gitbash

国内使用cnpm，使用方式 npm install -g cnpm --registry=https://registry.npm.taobao.org

1.安装hexo-cli

cnpm install -g hexo-cli

2.创建博客文件夹，如D:\blog

3.初始化博客

在文件夹内打开命令行输入hexo init 或 hexo init [博客文件夹]

4.安装依赖

cnpm install

5.启动服务

hexo s，默认端口4000

6.渲染静态资源

hexo g

## 使用

1.安装Git依赖hexo-deployer-git

cnpm install hexo-deployer-git --save

2.配置 _config.yml

deploy:
 type: git
 repository: https://github.com/yourname/yourname.github.io.git
 branch: master

3.发布到GitHub

hexo d

4.查看 https://ys97.github.io

NexT主题6.0
https://github.com/theme-next/hexo-theme-next.git themes/next

RSS

安装hexo-generator-feed插件 npm install --save hexo-generator-feed

在站点配置文件添加

Extensions

Plugins: http://hexo.io/plugins/

plugins: hexo-generate-feed 主题配置文件 rss: /atom.xml

RSS迁移

安装hexo-migrator-rss插件 npm install --save hexo-migrator-rss

从 RSS 迁移所有文章 hexo migrate rss