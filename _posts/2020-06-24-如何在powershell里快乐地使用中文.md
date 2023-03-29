

---
title: "如何在powershell里快乐地使用中文"

excerpt_separator: "`<!--more-->`"

categories:

  - Blog

tags:

  - Windows

  - powershell
---

最近在jekyll上写博客，上传的时候总是要加头部有点烦。于是今天用powershell写了一个脚本，实现给md文件加yaml头部，结果发现powershell对中文着实不友好，本来一个简单的事情折腾了大半天。在这里总结一下。

## 控制台输出中文

作为在windows上使用的脚本，powershell很不幸也是默认GBK，更为不幸的是，使用 `chcp 65001`并没有用，作为一个想要让更多人能用的脚本，又不能通过改本地配置解决。最后不得不把脚本的编码改成GBK，打不过加入总可以吧。

## 读入文件

我在本地写文章的编码是UTF8，powershell使用GBK，读入直接变成乱码。这个要解决还是比较容易，直接在指令后面追加编码选项即可。

```powershell
$doc = Get-Content  $file".md" -Encoding utf8
```

## 输出文件

拼接头部的时候唯一的问题就是中文提示信息的输出，这个问题在前面已经解决过了。生成头部之后把它和原本的文章拼接在一起。直接使用字符串拼接会把文章内部的换行吃掉，使用echo就没有这个问题。

```powershell
$res = $(echo $head $doc)
```

然后输出，输出花了很长的时间解决。首先，powershell的默认输出是UTF16LE。一开始，我想魔模仿读入文件，在输出的时候加入编码选项，但加上 `encoding UTF8`得到的是带DOM的UTF8，其特点是在开头会有一个指示大小端的特殊字符 \ufeff，这对YAML头来说是不能接受的（事实上，我开头多了一个空行也不行），StackOverflow上的意见有两种，一种是使用 `encoding UTF8NoDom`选项，但这个选项只有powershell6以上支持。另一种是使用.NET的输出：

```powershell
[System.IO.File]::WriteAllLines($name, $res)
```

第一个参数是写入的文件路径，第二个是内容。输出的格式默认是纯UTF8。

解决了上述问题之后，就能愉快地在powershell里使用中文了！
