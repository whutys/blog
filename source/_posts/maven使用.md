---
title: maven使用
type: categories
copyright: true
date: 2019-01-10 19:29:57
categories: [软件安装使用]
tags: maven
---
## 安装
maven官网 maven.apache.org
国内使用阿里仓库

修改settings.xml，加入
```
<mirror>
      <id>alimaven</id>
      <mirrorOf>central</mirrorOf>
      <name>aliyun maven</name>
      <!--<url>http://maven.aliyun.com/nexus/content/repositories/central/</url>-->
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
</mirror>
```

依赖查询 https://mvnrepository.com/