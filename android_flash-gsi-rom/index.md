# 安卓手机刷入 GSI 镜像教程


从理论上来说，刷入某个 GSI，你的手机就会摇身一变，从一个系统切换到了另一个系统。

<!--more-->

## 一、gsi 镜像包介绍
GSI 的全称是 Generic System Image，翻译过来就是「通用系统镜像」，这个概念来源于 Project Treble。 自从 Android 8 引入 Project Treble 后，手机的系统文件和底层的厂商硬件驱动开始分离存放，更新系统时只需要更新系统文件即可。此项举措意在方便厂商加快 Android 大版本更新的步伐，自然也同样方便了第三方 ROM 的开发和更新，成为了社区开发的一大福音。从理论上来说，刷入某个 GSI，你的手机就会摇身一变，从一个系统切换到了另一个系统。
## 二、gsi 镜像通刷包的特点
优点是在机器还没有适配第三方 ROM 的时候，可以提前体验到类原生系统，体验原生系统的流畅简洁以及丰富的自定义。但同样存在不小的问题，由于此类镜像包没有针对具体机型进行优化，所以会存在部分问题，例如小米手机的四角弧度过大，gsi 镜像包刷入后状态栏会有不匹配，显示不完全的可能性以及相机无法拍照，即使可以拍照，相片质量也堪忧。
## 三、gsi镜像包的刷入选择
gsi通刷包有很多种选择，也是由不同的国外大神负责维护，下面贴上几乎所有 gsi 通刷包（包括官方和非官方）的集合链接，请各位自行选择，选择包的种类请见下一章节。

[点此跳转GitHub](https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-%28GSI%29-list)
## 四、gsi镜像包类名的选择（两类）
### 出厂安卓版本是8.0及以下的手机
#### 第一步  
需要下载一个软件 Treble Check 检测，附上谷歌商店和酷安链接。

   [Treble Check（点击跳转Google play store）](https://play.google.com/store/apps/details?id=com.kevintresuelo.treble)

   [Treble Check（点击跳转酷安应用市场）](https://www.coolapk.com/apk/com.kevintresuelo.treble)
#### 第二步  
打开软件查看检测结果，只有当 **Project Treble** 通过检测才表明此手机可以刷 gsi 镜像包。接着看第二项 **Seamless System Updates**，如果显示 **A/B** 即表明你应该选择的通刷包后缀名为 *A/B* 或者 *AB* 。若检测结果显示 **A only**，即表明你应该选择的通刷包后缀名为 *A* 或者 *A only*。
#### 第三步  
上网查找你所使用手机的内核名称，例如小米 9 SE 为 **arm64**

### 出厂版本是安卓9.0版本的手机（第二步关键）
#### 第一步  
同上第一步，需要检测 **Project Treble** 是否支持
#### 第二步  
此处注意！凡是出厂版本为 9.0 的手机，无论 **Seamless System Updates** 检测结果如何，通刷包的版本一律选择 **A/B** 或 **AB**。
#### 第三步  
同上第三步。

## 五、刷机步骤
### 自行完成
自行刷入第三方 rec  
自行下载好 gsi 解压后得到 img 镜像包

### 刷机前注意
使用官方稳定ROM作为底包，不要使用开发版和任何官改版。

### 开始刷机
#### 方法一：Rec 刷入
##### 第一步  
手机备份好重要资料后，重启至第三方 recovery TWRP, 并在**高级**中选择**取消强制加密**并选中两项后确认。
##### 第二步  
主页面选择**清除**，滑动下方滑块进行**双清**即可，不要自作多情，双清足够。
##### 第三步  
返回主页面，选择**安装**后，点击右下方**刷入镜像**，找到拷贝到手机里的**img**镜像包，选择后刷入**System镜像**分区内，等待结束后再次**双清**即可使用。

#### 方法二：fastboot 刷入    
>**此方法仅对小米手机有效**
##### 第一步
- 网络下载符合所使用机型的 vbmeta.img, 并将其拷贝到 platform-tools 文件夹内  
- 下载 [GSI](https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-%28GSI%29-list) 包  (choose A/B one)

##### 第二步  
adb依次输入以下命令
{% highlight ruby %}
fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img
fastboot flash system <gsi-img>
fastboot -w
fastboot reboot
{% endhighlight %}

## 六、修复 GSI 可能存在的基础问题
### 修复自动亮度失效
1. 下载 [framework-res__auto_generated_rro.apk](https://drive.google.com/open?id=1DF-v-gwG1rQT-SbAZQYlTwFZFcOPKI9U)
2.  用re管理器将其复制到 vendor/overlay 文件夹
3. 修改 overlay 文件夹权限为 `rwxr-xr-x`
3. 手机打开 Termux 输入以下命令
{% highlight ruby %}
mount -o remount -w /vendor
chcon u:object_r:vendor_overlay_file:s0 /vendor/overlay;chcon u:object_r:vendor_overlay_file:s0 /vendor/overlay/framework-res__auto_generated_rro.apk
{% endhighlight %}

### 修复扬声器失真
1. 手机下载 Root Explorer
2. 删除两个文件夹
>/system/vendor/lib/soundfx  
>/system/vendor/lib64/soundfx
3. 改变 vendor 文件夹的权限为  `rw-r--r--`
4. 重启手机

### 修复屏幕状态栏圆角
adb 输入以下命令(最后的数字根据自己喜好任意修改):  
{% highlight ruby %}
adb shell settings put secure sysui_rounded_content_padding 20
{% endhighlight %}

## 七、系统的使用
完成以上步骤即可完成刷机工作，如过程中遇到问题，可以去负责维护相关镜像系统的GitHub反馈Issue。

