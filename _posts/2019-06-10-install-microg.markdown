---
layout: post
title:  "microG安装教程"
date:   2019-06-10 21:47:55
tags: microG & GApps
color: rgb(255,90,90)
cover: 'https://microg.org/img/microg_full_colored.svg'
---
## 下载卡刷包
[点此下载](https://androidfilehost.com/?w=files&flid=198483) **NanoDroid-patcher** 和 **NanoDroid-microG** 两个卡刷包。
## 第一步  
刷入目标第三方 ROM（必须刷入不包含谷歌框架的系统包）。
## 第二步（推荐但不是必要的）  
刷入Magisk。  
>如果安装了 Magisk，NanoDroid 将会被作为模块刷入，否则将会直接安装到/system 分区。


## 第三步（若无需求可省略）  
安装 Kernel 核心。
## 第四步  
安装 **NanoDroid-patcher** 卡刷包（时间大约在5到10分钟，请耐心等待。)
## 第五步  
将下载好的 **NanoDroid-microG** 卡刷包打开，找到 **.nanodroid.setup**，以文本编辑模式打开，按照如下提示自定义按需设置：（**1是开启,0是关闭**）
>- nanodroid_microg=1  
>microg核心，必须开启  
>- nanodroid_gmscore=0  
>谷歌原版服务框架，如果开启，上面microg要关闭，正常不开启  
>- nanodroid_fdroid=1  
>开源应用商店，按自己需求开启  
>- nanodroid_apps=1  
>microg其他软件默认开启  
>- nanodroid_play=1  
>谷歌原版商店，可以开启  
>- nanodroid_overlay=0  
>- nanodroid_zelda=1  
>- nanodroid_mapsv1=1  
>地图api，默认开启  
>- nanodroid_init=1  
>- nanodroid_gsync=0  
>谷歌同步，联系人，chrome等同步，如果在使用谷歌同步要开启  
>- nanodroid_swipe=0  
>- nanodroid_forcesystem=0  
>- nanodroid_nlpbackend=1000  
>- nanodroid_nano=1  
>- nanodroid_bash=1  
>- nanodroid_utils=1  
>- nanodroid_fonts=1  
>- nanodroid_override=0     


## 第六步  
安装 **NanoDroid-microG** 卡刷包后，重启手机至系统。
## 第七步  
打开 microG 设置如下：  
>运行 Self Check 授予缺少的必要权限,并关闭电池优化  
>启用 Google device registration  
>启用 Google Cloud Messaging  
>启用 Google SafetyNet  
>在 UnifiedNlp Settings 内全部勾选
