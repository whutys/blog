---
title: CATIA VBA
type: categories
copyright: true
date: 2019-01-25 21:57:57
categories: [CATIA,VBA]
tags: [CATIA,VBA,二次开发]
---

### VBA intersection之注册表操作

注册表句柄键：HKEY_CURRENT_USER\Software\VB and VBA Program Settings

SaveSetting将一个值存储到注册表里

```
SaveSetting "工程主题","主键名","键名","键值"
```

appname 必要。字符串表达式，包含应用程序或工程的名称，对这些应用程序或工程使用设置 
section 必要。字符串表达式，包含区域名称，在该区域保存注册表项设置。 
key 必要。字符串表达式，包含将要保存的注册表项设置的名称。 
setting 必要。表达式，包含 key 的设置值。 

GetSetting获取的注册表的键值

```
GetSetting "工程主题","主键名","键名","默认键值" '默认键值,当获取为空,或不成功时返回默认值
```

appname 必要。字符串表达式，包含应用程序或工程的名称，要求这些应用程序或工程有注册表项设置。 
section 必要。字符串表达式，包含区域名称，要求该区域有注册表项设置。 
key 必要。字符串表达式，返回注册表项设置的名称。 
default 可选。表达式，如果注册表项设置中没有设置值，则返回缺省值。如果省略，则 default 取值为长度为零的字符串 ("")。

### 去CATVBA密码，同VBA

使用文本编辑器（如notepad++）打开vba文件

搜索DBP字段，修改为DBx，如有多个都修改，最后保存（若提示占用，先移除CATIA宏）

CATIA加载宏文件，提示出错一路回车，打开宏加密面板，修改密码为自己的密码，记住保存

DPx改回DPB

使用自己修改的密码打开宏编辑