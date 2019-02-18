---
title: springboot
type: categories
copyright: true
date: 2019-01-10 19:49:07
categories: [java,javaweb]
tags: springboot
---



LoggerFactory is not a Logback LoggerContext but Logback is on the classpath….

spring-boot-starter-web下

```xml
<exclusions>
      <exclusion>
         <groupId>ch.qos.logback</groupId>
          <artifactId>logback-classic</artifactId>
      </exclusion>
</exclusions>

```

IntelliJ IDEA启动spring boot项目出现Failed to start component [StandardEngine[Tomcat].StandardHost[localhost].TomcatEmbeddedContext[]]

进入Project Structure，修改左侧Project、Modules，把其中的Project SDK修改为自己定义的jdk1.8