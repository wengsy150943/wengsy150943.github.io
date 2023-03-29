

---
title: "windows10下scoop的安装"

excerpt_separator: "`<!--more-->`"

categories:

  - Blog

tags:

  - Windows

  - Scoop
---



scoop是可用于windows的一款包管理工具，今天试着安装了一下，在这里记录一些遇到的问题和解决方法。
安装流程
先进入powershell，windows徽标键输入powershell或者cmd输入powershell均可
然后先输入以下代码，以保证后面的脚本有运行权限

```powershell
set-executionpolicy remotesigned -scope currentuser
```

```powershell
执行策略更改
执行策略可帮助你防止执行不信任的脚本。更改执行策略可能会产生安全风险，如 https:/go.microsoft.com/fwlink/?LinkID=135170
中的 about_Execution_Policies 帮助主题所述。是否要更改执行策略?
[Y] 是(Y)  [A] 全是(A)  [N] 否(N)  [L] 全否(L)  [S] 暂停(S)  [?] 帮助 (默认值为“N”): y
```

然后开始正式安装

```shell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

这一步可能出现超时或者连接中断的问题，对于这两个问题其实区别不大，都是属于网络的问题，在网上见到两种解决办法。

1. 开代理
   简单粗暴，可惜我没有
2. 查看这个网址 `https://get.scoop.sh`，会发现它转到 `https://raw.githubusercontent.com/lukesampson/scoop/master/bin/install.ps1`，所以可以把代码改成

```shell
iex (new-object net.webclient).downloadstring('https://raw.githubusercontent.com/lukesampson/scoop/master/bin/install.ps1')
```

或者，打开这个网址，把内容复制下来，然后本地运行。比如说创建一个txt，把内容贴进去，后缀改成$ps1$，在对于位置使用命令

```shell
iex 1.ps1
```

如果发生了中断，下一次使用命令安装的时候会显示已安装，把 `C:\Users\<user name>`下的scoop文件夹删掉就好了。
