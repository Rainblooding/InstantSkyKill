---
abbrlink: ''
categories:
- - Linux
date: '2024-07-28T15:39:38.479407+08:00'
tags:
- shell
title: 初识shell
updated: '2024-07-28T16:02:23.231+08:00'
---
## 什么是shell

shell是系统提供的的文本交互界面。shell通过分析用户输入的文本，选择合适的内部函数或是其他可执行文件执行。例如下面这个命令：

```bash
free -h
```

<!-- more -->

通过空格shell可以把这个文本分为多个部分，在上面的这个文本中可以分为两个部分。第一个部分是`free`

它是命令名，第二个部分是`-h`它是一个选项。大部分的命令都可以分为这样的两个部分命令名，选项/参数。

有了命令名，shell下一步就要执行该命令名对应的动作。这就像戏剧舞台上，演员按照脚本演戏。shell命令可以分为如下三类。

- shell内建函数
- 可执行文件
- 别名

shell的内建函数是保存在shell内部的脚本。可执行文件是保存在shell之外的脚本。shell必须在系统中找到对应命令名的可执行文件，才能正确执行。可以通过绝对路径告诉shell可执行文件所在的位置，或是shell搜索一些特殊的位置，也就是默认路径，如/bin。

我们可以通过`which`命令确定命令名对应的是哪个可执行文件：

```bash
which date
```

别名就是给某个命令起的一个简称，之后shell就可以它通过这个简称调用对应的命令。在shell中可以通过`alias`来定义别名：

```bash
alias freak="free -h"
```

shell会记住我们定义的别名，以后在shell中输入命令`freak`时，都将等价于输入`free -h`

在shell中可以通过type来了解命令的类型：

```bash
root@VM3466752C090B1FC:~# type pwd
pwd is a shell builtin
root@VM3466752C090B1FC:~# type date
date is /usr/bin/date
root@VM3466752C090B1FC:~# type freak
freak is aliased to `free -h'

```
