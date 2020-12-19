---
layout: post
title:  "Quantumult X 京东脚本设置 "
date:   2020-12-19 22:36:00
tags: 代理软件
color: rgb(135,206,235)
cover: 'https://github.com/jallenlau/picture/blob/master/OpenWRT-bug.jpg?raw=true'
---

> Quantumult X 京东签到脚本设置

## 溯源
由于软路由 LEDE/OpenWrt 系统的问题日渐显现，改刷 OpenWrt。  
在此记录安装步骤。

## 准备
### 工具软件
- Quantumult X（外服 App Store 下载）
- [lxk0301 京豆签到脚本（长按复制链接）](https://raw.githubusercontent.com/lxk0301/jd_scripts/master/QuantumultX/lxk0301_gallery.json)
- [NobyDa 京东 Cookies 获取脚本](https://github.com/NobyDa/Script/blob/master/JD-DailyBonus/JD_DailyBonus.js)


> 选用  
> Scriptable（用来显示京豆收益图，国服即可下载）  
> [Boxjs 重写脚本（选用）](https://raw.githubusercontent.com/whyour/hundun/master/quanx/whyour.boxjs.json)  
> [Boxjs 文档](https://chavyleung.gitbook.io/boxjs/)  
>

## 步骤
### 配置 Quantumult X
1. 打开 Quantumult X，点击主界面右下角按钮。
![1](https://github.com/jallenlau/picture/blob/master/quan/1.PNG)


2. 下载好 physdiskwrite 工具、OpenWrt 镜像安装包，并全部拷贝至启动盘根目录。
3. 将软路由连接显示器、键鼠、U 盘。
4. 设置 U 盘启动，进入 PE 系统，并在分区管理工具内删除软路由固态硬盘**所有分区**并保存（不要设置新的分区，保持整个磁盘空闲状态）。
5. 打开 cmd 命令，输入 PE 启动盘所在盘符号（以下是范例）：
```
U:
```
6. 输入以下代码（XXX 替换为 OpenWrt 的安装包全名）：
```
physdiskwrite -u XXXX.img
```
7. 输入软路由的磁盘数字（一般为 0）并确认安装：
```
0 #之后按回车键
y #之后按回车键（确认安装）
```
8. 安装完毕后拔掉 U 盘并重启软路由，同时设置软路由硬盘启动。
> - 等待屏幕不再滚动代码后，按回车键  
> - 输入：```vi /etc/config/network```  
> - 自行更改 LAN 口 IP 地址和 WAN、LAN 的分配网口（涉及 Linux 基础，此处不再赘述，不懂可以略过）
9. 连接 LAN 口到计算机，浏览器地址栏输入更改后的 IP，如果略过了上方引言步骤，此处 IP 地址只能输入 ```192.168.1.1```，初始密码是：```password```。
10. 自行设置软路由的网络。

## 安装 Clash（此处以 OpenClash 作为范例）
1. 打开 PuTTY，输入软路由的 IP，选择 SSH 模式，进入。
2. 安装依赖：
```
cd /tmp
opkg update
opkg install luci
opkg install luci-base
opkg install iptables
opkg install dnsmasq-full
opkg install coreutils
opkg install coreutils-nohup
opkg install bash
opkg install curl
opkg install jsonfilter
opkg install ca-certificates
opkg install ipset
opkg install ip-full
opkg install iptables-mod-tproxy
opkg install kmod-tun  #TUN模式
opkg install luci-compat
```
3. 打开 WinSCP，文件协议选择 SCP，输入软路由的 IP，输入用户名密码，进入。
4. 找到 OpenClash 的 ipk 安装包，右键上传到软路由的 tmp 文件夹内。
5. 回到命令行，输入（xxx 替换为安装包全名）：
```
opkg install xxx.ipk
```
6. 回到软路由页面，刷新，看见**服务**选项卡出现 OpenClash 表示安装成功。

## 总结
1. Luci for Clash 安装方法类似，不再赘述。
2. Clash 安装后具体用法请参考具体配置说明：[OpenClash wiki](https://github.com/vernesong/OpenClash/wiki)。

## 附录
- [lhie1 Rules 项目地址](https://github.com/lhie1/Rules/tree/master)
- [Clash Config Builder](https://fndroid.github.io/clash-config-builder/)
- [Clash Config Builder wiki](https://github.com/Fndroid/clash-config-builder/blob/master/README.md)
- [Netflix 完美策略组](https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Media/Netflix.list)
