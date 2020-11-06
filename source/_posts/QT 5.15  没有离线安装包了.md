---
title: 'QT 5.15 Windows 离线预编译安装包'
date: 2020-06-19
category: Experience
tags: 
- C++
- QT
- Windows
---
是的, 官方没有, 但可以有
<!--more-->

### 关于为何没有...

可以看看[这个链接](https://mirrors.cloud.tencent.com/qt/official_releases/qt/5.15/5.15.0/OFFLINE_REAMDE.txt)里的内容. 其实重点就是两个, 一个是不给开源用户提供LTS支持, 另一个就是不提供了线下安装包. 

其实这个问题在知乎也有讨论过, 个人认为首先没有更换许可证, 其次, 对于开源用户来说, 大多数是尝鲜或者开发开源产品用的, 基本上迭代起来都比较自由. 对于商业公司可能对LTS的支持更加迫切一些, 所以问题不大. 

但, 不给离线安装包这个很痛苦, 并不在于这个规矩本身, 而是你官方没有给离线安装包, 那同步的镜像源就没有, 于是你从官网那个垃圾服务器上下载论G的内容是很痛苦的一件事情, 特别是由于众所周知的原因, 墙内很多东西根本用不了. 

而且, 其实这么长时间以来, QT从来就没有给过windows上64位的离线安装包, 只有32位的. 我也不知道都2020年了为啥还有只支持32位的东西. 

### 那怎么办

"有条件就上, 没条件就创造条件也可以上".

自己编译一个. 而且还能编译成x64的.

其实这个东西我是踩了很久的坑. 既然你是在Windows上, 那当然最好是用MSVC来编译啦. 其实按照QT的传统艺能应该是用MinGW来编译, 但是...由于一些我不知道的原因, 我用MinGW编译总是会报一些编译错误, 比如说某个数组声明不对啦什么的. 希望有能人可以告诉我到底是怎么回事. 总之, 我这次用Visual Studio 2019 Community编译了x86和x64两个版本. 如果你不想关心我是怎么编译的, 那么你可以直接从下面两个链接下载. 

[QT 5.15.0 Opensource Windows MSVC2019 x64](https://data-vankyle-1257862518.cos.ap-shanghai.myqcloud.com/software/qt/5.15/qt-opensource-windows-x64-5.15.0.zip) 大小 486.21MB

[QT 5.15.0 Opensource Windows MSVC2019 x86](https://data-vankyle-1257862518.cos.ap-shanghai.myqcloud.com/software/qt/5.15/qt-opensource-windows-x64-5.15.0.zip)  大小 395.69MB



### 编译的辛酸史

首先, 我承认我对大型项目的编译一无所知...

QT自己有一个qmake, 对它没有用万能且好用的CMake而是自己搞了一个QMake. 这个QMake会在最开始你configure 的时候先被编译出来, 然后它再调用这个QMake跑一遍, 相当于构造好了调用MSVC的脚本, 然后再用MSVC来编译. 

其次, 这个QT编译过程中产生的中间文件非常大, 我最开始的时候为了保证自己本机的开发环境不被搞乱, 我特意开了一个虚拟机来配环境, 配好环境之后开始编译, 结果没过多久虚拟机的硬盘就爆了....害得我第二天起来还得扩容再编译一轮. 

再有就是, 怎么才能让它乖乖编译64位的问题. 

你装完Visual Studio的MSVC这一套东西之后, 他会给你一套命令行工具, 就是这几个家伙：

![Visual_studio_cli_tools](https://data-vankyle-1257862518.cos.ap-shanghai.myqcloud.com/image/vankyle/Visual_studio_cli_tools.png)

 

我最开始觉得, 都2020年了, 谁还用CMD是吧, 当然是用Powershell啦. 

结果我发现我还是too young too simple, 它给你的这个powershell, 默认给的是32位的环境. 所以你configure的时候, 全是32位的设置. 

为了这件事我苦恼了很久. 最后是抱着非常不屑的心理,, 用那个x64 Native Tools 的CMD, 结果...竟然成功配置成了64位....

于是, 就这样编译成功了...

最后, 这种大型工程, 源文件都是各种零碎的小文件, 不管是解压还是移动, 都非常痛苦.. 你可想而知, 我这个过程多么艰辛了. 如果你那两个编译好了的包觉得开心, 就点个打赏吧, 谢谢啦. 