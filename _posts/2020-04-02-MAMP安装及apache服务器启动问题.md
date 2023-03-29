
---
title: "MAMP安装及apache服务器启动问题"

excerpt_separator: "`<!--more-->`"

categories:

  - Blog

tags:

  - Windows

  - MAMP
---

> 看解决方案直接拉到底部总结

今天装MAMP，本来以为是很简单的事，结果还是出了点小问题。问题分成好几个阶段，都能查到解决方法，在这里汇总一下。

##安装流程

###下载

在官网 `https://www.mamp.info/en/downloads/`下载，根据系统选版本，没什么好说的。

###安装

按照安装程序一路默认即可。

###启动

默认会在桌面创建两个图标，MAMP和MAMPPRO，点击前一个启动就好了，正常的启动界面应该是这样的：

![avatar](https://img2020.cnblogs.com/blog/958944/202004/958944-20200402115511048-2006777504.png)

注意右上角两个服务器的灯都要亮，然后stop server的灯也亮就行了。点击中间的open website page或直接在浏览器输入 `http://localhost/MAMP/`，就会跳转到以下页面。

![avatar](https://img2020.cnblogs.com/blog/958944/202004/958944-20200402115431667-512907423.png)

##问题解决

本来以为这样开开心心吃着火锅唱着歌就装好了，可是事情没那么简单。装完之后启动，apache服务器的灯闪了一下就灭了。stackoverflow启动！很快就找到了解决方案。`https://stackoverflow.com/questions/58296601/apache-server-will-not-start-on-mamp`

简单来说，就是在MAMP界面，MAMP->preferences->PHP，把PHP版本调低到7.2.14，然后重启。

做到这里还没什么问题，重启之后，发现不单单是apache闪灭，sql干脆不亮了。继续查，看到博客 `https://stackoverflow.com/questions/58296601/apache-server-will-not-start-on-mamp`提供了解决方案。就是打开 `MAMP\conf\apache\httpd.conf`，查找 `LoadModule perl_module modules/mod_perl.so`（用关键词 `mod_perl.so`就能查到），然后前面加#注释，保存，重启MAMP即可。

到此就能正常看到前面所说的页面了。

##有效搜索

因为用语言描述在搜索引擎上查效果比较一般（语文没学好），比较有效的方法是打开问题日志 `MAMP\logs\apache_error.log`，把里面的warn贴进搜索栏，效果不错，当然直接从问题日志看懂问题然后解决就更好了。

##总结

###问题一

现象：apache服务器闪退，sql正常。
问题日志出现：

```
[warn] Init: Session Cache is not configured [hint: SSLSessionCache]
[warn] pid file C:/MAMP/bin/apache/logs/httpd.pid overwritten -- Unclean shutdown of previous Apache run?
[notice] Digest: generating secret for digest authentication ...
[notice] Digest: done
```

解决方法：

MAMP->preferences..->PHP->版本改为7.2.14，重启。

###问题二

现象：apache服务器闪退，sql不启动。
问题日志出现：

```
[warn] Init: Session Cache is not configured [hint: SSLSessionCache]
[warn] pid file D:/MAMP/bin/apache/logs/httpd.pid overwritten -- Unclean shutdown of previous Apache run?
[notice] Digest: generating secret for digest authentication ...
[notice] Digest: done
[notice] Apache/2.2.31 (Win32) DAV/2 mod_ssl/2.2.31 OpenSSL/1.0.2h mod_fcgid/2.3.9 mod_wsgi/3.4 Python/2.7.6 PHP/7.2.14 mod_perl/2.0.8 Perl/v5.16.3 configured -- resuming normal operations
[notice] Server built: May  6 2016 10:19:53
[crit] (22)Invalid argument: Parent: Failed to create the child process.
[crit] (OS 6)句柄无效。  : master_main: create child process failed. Exiting.
```

解决方法：

打开 `MAMP\conf\apache\httpd.conf`，注释 `LoadModule perl_module modules/mod_perl.so`，保存，重启。
