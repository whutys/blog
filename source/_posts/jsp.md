---
title: jsp
type: categories
copyright: true
date: 2019-01-10 19:47:45
categories: [java,javaweb]
tags: [jsp]
---

###  9大内置对象

out、request、response、session、pageContext、application、config、page、exception

#### out：Javax.servlet.jsp.JspWriter

作用域：page。

#### request：Javax.servlet.http.HttpServletRequest

作用域：request。请求结束，生命周期 结束。

```java
getParameter(key); //获取提交表单的数据
getParameterValues(key); //获取提交表单的一组数据
request.getRequestDispatcher("list.jsp").forward(request,response); //转发(通过代码的方式进行转发)
request.setAttribute(key,object); //设置请求对象的属性
request.gettAttribute(key); //获取请求对象的属性
request.setCharacterEncoding("UTF-8"); //对请求数据重新编码
```

#### resonpse：Javax.servlet.http. HttpServletResponse

作用域：page

```java
response.sendRedirect("页面");//页面跳转。注意，之前的forward是转发，这里是跳转，注意区分。
response.setCharacterEncoding("gbk");//设置响应编码
```

#### session：Javax.servlet.http.HttpSession

作用域：session。表示一个会话，用来保存用户信息，以便跟踪每个用户的状态。是指在一段时间内客户端和服务器之间的一连串的相关的交互过程。

```java
session.getid();//取得session的id号.id由tomcat自动分配。
session.isnew();//判断session时候是新建的
session.setAttribute(key,object);//往当前会话中设置一个属性
session.getAttribute(key);//获取当前会话中的一个属性
session.removeAttribute(key);//删除当前会话中的属性
session.setMaxInactiveInterval(1000*60*30);//设置当前会话失效时间(ms) 。Tomcat默认的会话时间为30分钟。
session.invalidate();//初始化当前会话对象(一般在推出的时候使用，可以删除当前会话的数据)
```

#### pageContext：javax.servlet.jsp.PageContext

作用域：page。JSP的页面上下文。

#### application：javax.servlet.ServletContext

作用域：application。从servlet配置对象获得的servlet上下文，生命周期最长。服务器启动的时候就会创建application对象。从服务器存在到服务器终止，都一直存在，且只保留一个对象，所有用户共享一个application。

#### config：javax.servlet.ServletConfig

作用域：page。本JSP的 ServletConfig配置对象

#### page：java.1ang.Object

作用域：page。实现处理本页当前请求的类的实例（javax.servlet.jsp.HttpJspPage），转换后的Servlet类本身。

#### exception：java.lang.Exception

作用域：page。本JSP页面的异常对象

