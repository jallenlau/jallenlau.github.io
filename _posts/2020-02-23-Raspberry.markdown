---
layout: post
title:  "树莓派 4B 完美实现音乐无损串流"
date:   2020-02-23 17:00:00
tags: 树莓派
color: rgb(255,90,90)
cover: 'https://github.com/jallenlau/picture/blob/master/MVIMG_20200223_151557.jpg?raw=true'
---
>利用树莓派低功耗、低噪音、免关机的特性，针对有聆听无损音乐且鄙夷繁杂操作等需求的用户打造一台方便的无损音乐串流器。

## 溯源
利用树莓派低功耗、低噪音、免关机的特性，针对有聆听无损音乐且鄙夷繁杂操作等需求的用户打造一台方便的无损音乐串流器。

## 功能简介
利用国外的 volumio 固件进行功能实现，可以将音频直接通过 USB 接口数字传输到 DAC 解码设备，不经过系统的二次 SRC 处理，保证了音频文件的原位深、源采样率。
并支持本地存储、局域网读取、NAS读取，通过插件支持 Spotify 无缝串流、One Drive 云盘读取私人音乐库、Tidal 及 Qobuz 无损音乐串流（付费功能）、无损电台播放等等功能。

## 所需设备及固件
- [Etcher](https://www.balena.io/etcher/) 镜像烧录工具
- [Volumio](https://volumio.org/) 下载适配 Raspberry 固件
- Micro-SD 16GB 内存卡
- 读卡器
- 树莓派 4B（具备无线网卡款）
- xDuoo XD-05 DAC 解码耳放（自选）

## 步骤
- 烧录前将卡格式化为 FAT32 格式，利用 Etcher 将 Volumio 固件烧录到 Micro-SD 卡内。
- 将卡插入树莓派，开机。
- 输入用户名：volumio ，密码：volumio
- 打开电脑搜索名称为 Volumio 的 WiFi ，输入密码：volumio2 连接。
- 依次按照提示操作，并连接无线网络。
- 用同一无线网下的设备登录 [http://volumio.local]() ,即可享受聆听。
- 若选择连接有线网络，则保证在同一网段的情况下，登录树莓派所在 IP 地址。
