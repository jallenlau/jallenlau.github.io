# microG 简介及安装


<!--more-->

## microG 介绍

越来越多的 Library 和 API 仅适用于预先安装了各种 Google 应用的手机，从而有效地将第三方应用锁定到 Google 生态系统。出于这些原因，Android 被描述为“可远观而不可亵玩”的开放式。

此时microG项目诞生了——谷歌专有核心库和应用程序的免费软件克隆。
用户获得了扩展的应用程序支持，可以减少或监控发送给 Google 的数据，旧款手机可以提高电池寿命。microG 不仅用于真实设备，还取代了测试模拟器中的 Google 工具，甚至用于虚拟移动基础设施。

## 组件

### Service Core (GmsCore)

是一个库应用程序，给需通过谷歌服务或 Google Maps Android API（v2）才可运行的应用程序所需的功能特性。

#### 概览

microG GmsCore 是 Google Play 服务框架的免费开源实现方式。它允许调用专有 Google API 的应用程序在基于 AOSP 的 Rom（如 Replicant 和 LineageOS）上运行。作为闭源 Google Apps（GAPPS）的替代品，它是在享受 Android 核心功能的同时保护隐私的强大工具。

#### 特征

>- 选择加入 Google 服务并扩展应用程序支持  
>  (Opt-in to Google Services and extend application support)  
>- 在线/离线定位服务  
>  (On-/Offline location service)  
>- 易于使用电池，内存和CPU  
>  (Easy on battery, memory and CPU)  
>- 没有多余软件  
>  (No bloatware)  
>- 适用于真实设备，测试模拟器和虚拟移动基础设施  
>  (Works on real devices, test emulators and virtual mobile infrastructure)  
>- 免费且开源（Apache 2.0许可）  
>  (Free and open source (Apache 2.0 licensed))  

#### 系统要求

需要伪装签名，使 GmsCore 可以假装官方 Play 服务使其存在于需要调用 Google API 的应用程序。  

>##### 签名伪装
>
>您需要一个支持签名伪装的 Rom。一些自定义 Rom 需要安装补丁并且在手机内完成部分操作设置以支持。  
>
>- CarbonROM  
>  MicroG will ask for Signature Spoofing authorization
>- OmniROM 5  
>  Must be enabled at the bottom of the developer settings first.
>- OmniROM 6/7  
>  Must be enabled in Settings>Apps>Advanced(gear icon)>Additional permissions>Spoof signature.
>- MarshRom  
>  Must be enabled in Settings>Apps>Advanced(gear icon)>Additional permissions>Spoof signature.
>- AospExtended  
>  Must be enabled in Settings>Apps>Advanced(gear icon)>App Permissions>Spoof package signature.
>- [LineageOS bundled with microG](https://lineage.microg.org/)
>- [其他自定义Rom的支持列表](https://forum.xda-developers.com/showpost.php?p=71042083)  
>
>如果安装了Xposed Framework，以下模块可以开启签名伪装：[FakeGApps](https://repo.xposed.info/module/com.thermatk.android.xf.fakegapps)    
>
>还可以通过 [NanoDroid-patcher](https://github.com/Nanolx/NanoDroid) 修补自定义 Rom，无需任何计算机操作,它将自动修补每次更新的 Rom。
>
>如果你已Root，但没有使用Xposed，你可以尝试使用 [Needle by moosd](https://github.com/moosd/Needle)（或 [fork Tingle by ale5000](https://github.com/ale5000-git/tingle)）或 [Haystack by Lanchon](https://github.com/Lanchon/haystack) 修补你已经安装的 Rom。Haystack可以选择添加一个简单的UI来控制伪装，它类似于 OmniROM 5 的伪装方式。请注意，所有3个修补程序都要求修补的是 Rom 不是 odexed。  
>
>**注意：microG GmsCore无法安装在拥有Google服务的设备上。**  
>
>[原文详情](https://github.com/microg/android_packages_apps_GmsCore/wiki/Signature-Spoofing)

#### 模块

GmsCore 包括统一网络位置提供程序模块（UnifiedNlp），用于处理对 Google 网络位置提供程序的应用程序调用。它依赖于必须单独安装的位置和地址查找后端。  

[参阅](https://github.com/microg/android_packages_apps_UnifiedNlp/blob/master/README.md)

对于完整的 microG 设置，可以安装PlayStore替换应用程序以及服务框架代理（GsfProxy）模块，以提供Google的推送消息服务。另请参见[安装](https://github.com/microg/android_packages_apps_GmsCore/wiki/Installation)。

### Services Framework Proxy (GsfProxy)

是一个辅助实用程序，允许为 Google Cloud to Device Messaging（C2DM）开发的应用程序使用 Gms Core 内附带的 Google Cloud Messaging Service。  

**同上GmsCore**

### Unified Network Location Provider (UnifiedNlp)

是一个库，可为使用 Google 网络位置的应用提供基于 Wi-Fi 和移动数据的地理定位。它包含在 GmsCore 中，但也可以在大多数 Android 系统上独立运行。

[详情](https://github.com/microg/android_packages_apps_UnifiedNlp/blob/master/README.md)

### Maps API (mapsv1)

是一个系统库，提供与现已弃用的 Google Maps API（v1）相同的功能。  

[详情](https://github.com/microg/android_frameworks_mapsv1)

## 下载

提供了从 microG 项目下载 APK 文件索引。对于非APK组件，请参阅相应的文档。

### F-Droid存储库

下载和更新 microG 项目组件的最佳方法是使用 F-Droid 存储库。它目前为 GmsCore 提供稳定的夜间更新以及 GsfProxy 和 FakeStore 发布。

[点此跳转下载界面](https://microg.org/download.html)

## 安装

### 下载卡刷包

[点此下载](https://androidfilehost.com/?w=files&flid=198483) **NanoDroid-patcher** 和 **NanoDroid-microG** 两个卡刷包。

### 第一步  

刷入目标第三方 ROM（必须刷入不包含谷歌框架的系统包）。

### 第二步（推荐但不必要）  

刷入Magisk。  

>如果安装了 Magisk，NanoDroid 将会被作为模块刷入，否则将会直接安装到/system 分区。


### 第三步（无需求可省略）  

安装 Kernel 核心。

### 第四步  

安装 **NanoDroid-patcher** 卡刷包（时间大约在5到10分钟，请耐心等待。)

### 第五步  

将下载好的 **NanoDroid-microG** 卡刷包打开，找到 **.nanodroid.setup**，以文本编辑模式打开，按照如下提示自定义按需设置：（**1是开启,0是关闭**）

>- nanodroid_microg=1  
>  microg核心，必须开启  
>- nanodroid_gmscore=0  
>  谷歌原版服务框架，如果开启，上面microg要关闭，正常不开启  
>- nanodroid_fdroid=1  
>  开源应用商店，按自己需求开启  
>- nanodroid_apps=1  
>  microg其他软件默认开启  
>- nanodroid_play=1  
>  谷歌原版商店，可以开启  
>- nanodroid_overlay=0  
>- nanodroid_zelda=1  
>- nanodroid_mapsv1=1  
>  地图api，默认开启  
>- nanodroid_init=1  
>- nanodroid_gsync=0  
>  谷歌同步，联系人，chrome等同步，如果在使用谷歌同步要开启  
>- nanodroid_swipe=0  
>- nanodroid_forcesystem=0  
>- nanodroid_nlpbackend=1000  
>- nanodroid_nano=1  
>- nanodroid_bash=1  
>- nanodroid_utils=1  
>- nanodroid_fonts=1  
>- nanodroid_override=0     


### 第六步  

安装 **NanoDroid-microG** 卡刷包后，重启手机至系统。

### 第七步  

打开 microG 设置如下：  

>运行 Self Check 授予缺少的必要权限,并关闭电池优化  
>启用 Google device registration  
>启用 Google Cloud Messaging  
>启用 Google SafetyNet  
>在 UnifiedNlp Settings 内全部勾选
