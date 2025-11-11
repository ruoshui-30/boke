---
title: Ventory打造多系统
tags:
  - 软件工具
  - 系统工具
  - 使用教程
categories: 技术笔记
abbrlink: 3123955317
date: 2025-11-11 18:50:54
---
Ventoy安装器 VentoyVHD支持插件 WinNTSetup EasyBCD WinPE安装器 系统镜像

B站视频链接：【利用Ventoy打造最强大的启动U盘，把PE、Win To Go统统塞进去】 https://www.bilibili.com/video/BV1EZ4y18769/?share_source=copy_web&vd_source=1618c435269c756c56b9cb58bcd9eb3d

**第一步：制作VHD虚拟磁盘**

1.打开 磁盘管理->更多操作->创建VHD 创建VHDX格式的虚拟磁盘文件

2.创建完毕后进行初始化和新建分区



**第二步：安装系统到虚拟硬盘**

1.打开WinNTSetup，选择系统版本，安装位置选择虚拟磁盘盘符安装系统（弹窗中的引导代码选项选择"不更新引导代码"）

2.打开EasyBCD，将VHDX磁盘镜像添加到本机系统引导中

3.重启后选择VHDX磁盘的引导项，等待系统安装完毕后重启系统到本机（慎重重启，最好在虚拟机上进行）



**第三步：制作WinPE镜像**

打开WinPE安装器，选择"可启动的ISO"制作WinPE镜像



**第四步：安装Ventoy**

***此过程会格式化U盘，请先备份好全部数据！！！**

1.打开Ventoy安装器，选择U盘盘符，点击"安装"

2.将制作好的U盘格式化为NTFS文件系统

3.将WinPE镜像和VHDX镜像复制到U盘的根目录

4.在U盘根目录下新建一个名为"ventoy"的文件夹，将VentoyVHD支持插件复制到此目录下



**第五步：进入系统**

1.进入BIOS页面选择从U盘启动

2.在Ventoy启动界面选择想要启动的系统