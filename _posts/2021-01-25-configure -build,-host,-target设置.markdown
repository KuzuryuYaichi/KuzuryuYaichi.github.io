---
layout: post
title:  "configure -build,-host,-target设置"
date:   2021-01-25 10:30:11 +0800
categories: Linux
---

### 释义

- build: 执行代码编译的主机，正常的话就是你的主机系统。这个参数一般由config.guess来猜。自己指定也可以。

- host: 编译出来的二进制程序所执行的主机，因为绝大多数是如果本机编译，本机执行。所以这个值就等于build。只有交叉编译的时候（也就是本机编译，其他系统机器执行）才会build和host不同。用host指定运行主机。

- target: 这个选项只有在建立交叉编译环境的时候用到，正常编译和交叉编译都不会用到。他用build主机上的编译器，编译一个新的编译器（binutils, gcc,gdb等），这个新的编译器将来编译出来的其他程序将运行在target指定的系统上。

### 编译gcc

#### Sample1

命令：`./configure --build=powerpc-linux --host=powerpc-linux　--target=powerpc-linux' `

说明：利用powerpc-linux的编译器(--build)对gcc进行编译，编译出来的gcc运行在powerpc-linux(--host)，这个gcc用来编译能够在powerpc-linux(--target)运行的代码。

作用：当然没有人会用这个选项来编译gcc。

#### Sample2

命令：`./configure --build=i386-linux --host=powerpc-linux --target=powerpc-linux`

说明：利用i386-linux(--build)的编译器对gcc进行编译，编译出来的gcc运行在powerpc-linux(--host)，这个gcc用来编译能够在powerpc-linux(--target)运行的代码。

作用：这个选项可以用来为其他的机器编译它的编译器。

#### Sample3

命令：`./configure --build=i386-linux --host=i386-linux --target=powerpc-linux`

说明：利用i386-linux(--build)的编译器对gcc进行编译，编译出来的gcc运行在i386-linux(--host)，这个gcc用来编译能够在powerpc-linux(--target)运行的代码。

作用：这个选项用来在i386主机上建立一个powerpc-linux的交叉编译环境。

#### Sample4

命令：`./configure --build=powerpc-linux --host=i386-linux --target=powerpc-linux`

说明：利用powerpc-linux(--build)的编译器对gcc进行编译，编译出来的gcc运行在i386-linux(--host)，这个gcc用来编译能够在powerpc-linux(--target)运行的代码。

作用：这个选项可以用来在i386主机上建立一个powrpc-linux的交叉编译环境，但是交叉编译环境在powerpc-linux 编译出来，安装到i386-linux主机上，估计没有多少人会这么用吧。
