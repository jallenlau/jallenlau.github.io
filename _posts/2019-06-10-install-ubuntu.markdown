---
layout: post
title:  "安装 Ubuntu"
date:   2019-06-10 22:11:03
tags: Linux
color: rgb(255,90,90)
cover: 'https://github.com/jallenlau/picture/blob/master/post-images/install_ubuntu.png?raw=true'
subtitle: 'UEFI启动模式安装Ubuntu双系统'
---
## 准备
- 下载 [Ubuntu](https://www.ubuntu.com/)
- 制作启动盘，下载 [Rufus](https://rufus.ie/)  
    启动安装页面 Partiton scheme 选择 UEFI，Target system 保持默认，其余不变并开始制作。
- 将欲安装磁盘分配足够的空余空间，至少100GB
- 进入电源管理，关闭**快速启动**
- 重启电脑进入 BIOS 并确保 **Boot mode** 为 **UEFI**
- 在 BIOS 内关闭 **Secure Boot**

## 安装
### 第一步  
U盘插入电脑，开机选取U盘作为第一启动。
### 第二步  
选择 **Install Ubuntu**，过程不要联网。
### 第三步  
**安装类型**菜单选择**其他选项**![安装类型](https://github.com/jallenlau/picture/blob/master/ubuntu/3.png?raw=true)
### 第四步  
#### 1.安装分区
此步骤最为关键，需要将预先设置好的空闲空间分配为四个子空间。
#### (1)分配启动引导空间 biosgrub
选择**主分区**、**空间起始位置**，用于**保留BIOS启动区域**，大小至少500MB。
![biosgrub](https://github.com/jallenlau/picture/blob/master/ubuntu/1.png?raw=true)
>如果想加快开机引导速度，却想将 Ubuntu 安装到机械硬盘内,可以在固态硬盘内留有足以用来制作引导区域的空间，并将引导空间选择为此部分空间。

#### (2)分配交换空间 swap
此部分为虚拟内存，可小幅度提高系统运行性能。  
选择**逻辑分区**、**空间起始位置**，用于**交换空间**，大小同物理内存即可。
![swap](https://github.com/jallenlau/picture/blob/master/ubuntu/4.png?raw=true)

#### (3)分配根目录空间 /
根目录即为系统盘，主要放操作系统。  
选择**逻辑分区**、**空间起始位置**，用于 **Ext4日志文件系统**、挂载点选择 **/**，大小尽量大。![根目录](https://github.com/jallenlau/picture/blob/master/ubuntu/2.png?raw=true)

#### (4)分配 /home 目录文件
此部分为自行操作空间。  
选择**逻辑分区**、**空间起始位置**，用于 **Ext4日志文件系统**、挂载点选择 **/home**，分配所有剩余空间。
![home](https://github.com/jallenlau/picture/blob/master/ubuntu/5.png?raw=true)

#### 2.选择引导器（关键!!!）
选择刚刚第一步建立引导的磁盘部分，注意盘符名称。  
![bios](https://github.com/jallenlau/picture/blob/master/ubuntu/6.png?raw=true)

### 第五步
安装并设置用户名密码。

### 第六步
安装完点击立即重启，如果重启过程卡死，长按电源键强制关机，拔掉U盘后重新开机。  
开机立刻进入 BIOS 设置开机启动顺序为 Ubuntu。  
至此安装完成，如下页面第一项为进入 Ubuntu 系统，第三项为进入 Windows 系统。
![boot](https://github.com/jallenlau/picture/blob/master/ubuntu/7.png?raw=true)

## 开机可能遇到的问题
### 画面自动旋转
开机后快捷键 **Ctrl+alt+T**，打开 Terminal 终端，输入：
{% highlight ruby %}
xrandr -o normal
{% endhighlight %}

然后点击屏幕右上角快捷设置，锁定屏幕。
