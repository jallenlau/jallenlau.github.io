# Ubuntu 常见命令


持续更新本人 Linux 学习过程中所需常见命令，已更新完结。

<!--more-->

## 基础指令

1. ls

```
#ls //列出当前路径下的全部文件夹名称
#ls <path> //列出指定路径下的全部文件(夹)名称
#ls root //列出相对路径root下的全部文件夹
#ls /root //列出绝对路径root下的全部文件夹
#ls -l <path> //以详细列表的形式列出路径下的所有文件夹
#ls -a <path> //显示隐藏文件(夹)
#ls -lh
```

2. cd & pwd

```
#pwd // Print Working Directory 打印当前工作路径
#cd <path> // Change Directory 切换当前工作目录
#cd ~ //切换到当前用户的家目录
    //#cd ~/apple
```

3. mkdir (Make Directory)

```
#mkdir <path> //创建目录
    //#mkdir newfolder
    //#mkdir /root/newfolder
#mkdir -p <path> //创建多层不存在目录
    //#mkdir -p /root/newfolder/a/b/c/d
#mkdir path1 path2 path3... //创建多个目录
```

4. touch

```
#touch <path> //创建文件
    //#touch fold1.txt fold2.txt...
```

5. cp (Copy)

```
#cp <copy path> <paste path> //可以对新文件重命名
#cp -r <copy folder> <paste folder> //复制文件夹，"- r" 表示递归复制
```

6. mv (Move)

```
#mv <move path> <paste path>
```

7. rm (Remove)

```
#rm -f <path> //force remove
#rm -r <path> //删除文件夹
    //rm -rf <path>
#rm -f linux* //删除具有公共特性的文件，*为通配符
```

8. vim

```
#vim <fold> //文件存在与否均可
            //Shift+: 按下 q 后回车即可退出
```

9. 储存重定向

```
#正常执行的指令 >/>> 文件的路径 //文件不存在则自动创建
    //#ls -la > ls.txt 覆盖
    //#ls -la >> ls.txt 追加
```

10. cat

```
#cat <path> //直接打开文件
#cat <path1> <path2> ... <pathN> > <path> //合并文件
```

## 进阶指令

1. df

```
#df -h //查看磁盘空间
```

2. free

```
#free -m/h //查看内存使用情况，-m 表示以 MB 为单位查看
```

swap 用于临时内存
shared 用于共享内存

3. head

```
#head -n abc.log //查看文件前 n 行，如果不指定，默认为10行
```

4. tail

```
#tail -n abc.log //查看文件末 n 行，如果不指定，默认为10行
#tail -f <path> //查看文件动态变化
```

一般用于查看系统日志

5. less

```
#less <path> //查看文件，以较少的内容进行输出，按下辅助功能键（数字+回车、空格+上下方向键）查看更多
```

6. wc

```
#wc -lwc //统计文件内容信息（包含行数、单词数、字节数）
    //-l 行数
    //-w 单词数
    //-c 字节数
```

7. date

```
#date //表示操作时间日期（读取、设置）
#date +%F
#date "+%Y-%m-%d" //输出形式：2019-07-02
#date "+%F %T"
#date "+%Y-%m-%d %H:%M:%S" //输出形式：2019-07-02 08:41:20
#date -d "-1 day" "+%Y-%m-%d %H:%M:%S"
#date -d "-1 year" "+%Y-%m-%d %H:%M:%S" //获取之前的时间
#date -d "+1 day" "+%Y-%m-%d %H:%M:%S" //获取之后的时间
```

%F 表示完整的年月日  
%T 表示完整的时分秒  
%Y 表示四位年份  
%m 表示两位月份（带前导0）  
%d 表示日期（带前导0）  
%H 表示小时（带前导0）  
%M 表示分钟（带前导0）  
%S 表示秒数（带前导0）  

8. cal

```
#cal
#cal -1 //直接输出当前月份日历
#cal -3 //输出上月+本月+下月日历
```

9. clear/ctrl+L

```
#clear/ctrl+L //清除(隐藏)终端中已经存在的信息
```

10. 管道  
    一般用于“过滤”、“特殊”、“拓展处理”。  
    不能单独使用，主要是辅助作用。

```
#ls /|grep y //过滤（查询出根目录下包含 “y” 的文档名称）
     针对以上命令说明：  
     ① 以管道作为分界线，前面的命令有个输出，后面需要先输入，再过滤最后输出。  
     ② grep 指令主要用于过滤。  
#ls /|wc -l //统计根目录文档总个数
```

## 高级指令

1. host name  
   操作主机名（读取、设置）

```
#hostname
#hostname -f //输出当前主机名中的 FQDN （全限定域名）
```

2. id  
   查看用户基本信息（包含用户id，用户组id，附加组id...），该指令如果不指定用户则默认当前用户。

```
#id
#id username //指定用户的信息
    验证上述信息是否正确？
    验证用户信息：#cat /etc/passwd
    验证用户组信息：#cat /etc/group
```

3. whoami  
   显示当前登录用户名，一般用于 shell 脚本，用于获取当前用户名，方便记录日志。

```
#whoami
```

4. ps -ef  
   查看服务器进程信息     
   “ -e ” 等价于 “ -A ” ，表示列出全部的进程  
   “ -f ” 显示全部列

```
jallen@JALLENLAU:~$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 07:44 ?        00:00:00 /init ro
root         6     1  0 07:44 tty1     00:00:00 /init ro
jallen       7     6  0 07:44 tty1     00:00:00 -bash
jallen      30     7  0 09:01 tty1     00:00:00 ps -ef
```

列的含义：  
UID：该进程执行的用户id  
PID：进程id  
PPID：该进程的父级进程id，如果一个程序的父级进程找不到，改进程称之为僵尸进程  
C：CPU的占用率  
STIME：进行的启动时间  
TTY：终端设备，发起该进程的设备识别符号
TIME：进程的执行时间
CMD：该进程的名称或者对应的路径  

```
#ps -ef|grep name //在 ps 结果中搜索
```

5. top  
   查看服务器进程占用资源

```
jallen@JALLENLAU:~$ top
top - 10:35:23 up  2:51,  0 users,  load average: 0.52, 0.58, 0.59
Tasks:   4 total,   1 running,   3 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.1 us,  3.7 sy,  0.0 ni, 90.9 id,  0.0 wa,  0.3 hi,  0.0 si,
KiB Mem :  8273208 total,  3175048 free,  4868808 used,   229352 buff/cac
KiB Swap: 15497464 total, 14828848 free,   668616 used.  3270668 avail Me
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+
    1 root      20   0    8892      0      0 S   0.0  0.0   0:00.10
    6 root      20   0    8904      0      0 S   0.0  0.0   0:00.01
    7 jallen    20   0   16928   1216   1128 S   0.0  0.0   0:00.26
  484 jallen    20   0   17644   1948   1436 R   0.0  0.0   0:00.03
```

- 表头含义：  
  PID：进程id  
  USER：该进程对应的用户id  
  PR：优先级  
  VIRT：虚拟内存  
  RES：常驻内存  
  SHR：共享内存    
  S：运行的状态（S代表睡眠，R代表运行）  
  %CPU：表示 CPU 占用百分比  
  %MEM：表示内存占用百分比  
  TIME+：执行的时间  
  COMMAND：进程的名称和路径  
- 计算一个进程实际使用的内存 = 常驻内存 - 共享内存
- 在运行 top 的时候,可以按下方便快捷键:
  M:表示将结果按内存从高到低进行排序  
  P:表示将结果按照 CPU 使用率从高到低进行降序排序

6. du -sh   
   查看目录真实大小  
   “ -s ”只显示汇总的大小  
   “ -h ”表示以较高可读性进行显示  

```
#du -sh <path>
```

7. find  
   用于查找

```
#find <path> option name
```

option:  
    -name //按照文档名称搜索（支持模糊搜索）  
    -type //按照文档类型搜索（“-”表示文件，在用find时用f替换），“d”表示文件夹

8. service  
   用于控制一些软件服务的启动/停止/重启

```
#service name start/stop/restart
```

9. kill

```
#kill 进程PID //配合 ps 一起使用
#killall 进程名称
```

10. ifconfig

```
#ifconfig //获取网卡信息
```

11. reboot  
    重启计算机

```
#reboot
#reboot -w //模拟重启（只写开机与关机的日志信息）
```

12. shutdown  
    关机

```
#shutdown
#shutdown -h now/15:25
```

13. uptime  
    输出计算机的持续在线时间

```
#uptime
```

14. uname  
    获取计算机操作系统相关信息

```
#uname //获取操作系统的类型
#uname -a //获取全部的系统信息（类型、全部主机名、内核版本、发布时间、开源计划）
```

15. netstat -tnlp  
    查看网络连接状态

```
#netstat -tnlp
```

选项说明：  
    -t：表示只列出 tcp 协议的链接  
    -n：表示将地址从字母组合转化为 ip 地址，将协议转化成端口号显示  
    -l：表示过滤出 stat（状态）列中其值为 LISTEN（监听）的连接  
    -p：表示发起连接的进程的 PID 的进程名称  

16. man（Manual）  
    手册（包含Linux中全部命令手册）

```
#man cp/rm/wc...
```

## 替换源

1. 输入指令。

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak //备份
sudo vim  /etc/apt/sources.list //打开list列表
```

2. 替换阿里源。

```
deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
```

3. 按 ESC 退出，并输入`:wq`保存。

4. 输入指令更新源。

```
sudo apt update
sudo apt upgrade
```

## 安装

1. 更新软件库  

```
sudo apt-get update
```

2. 安装软件

```
sudo apt-get install <package>
```

3. 通过关键词搜索软件库

```
sudo apt search <key>
```

## 卸载

1. 删除软件及其配置文件。

```
apt-get purge / apt-get --purge remove <package>
```

2. 删除依赖包,保留配置文件。

```
apt-get autoremove <package>
```

3. 删除软件，不删除依赖包，保留配置文件。

```
apt-get remove <package>
```

4. apt的底层包是dpkg，而dpkg安装Package时，会将*.deb 放在 /var/cache/apt/archives/ 中，apt-get autoclean 只会删除 /var/cache/apt/archives/ 已经过期的deb。

```
apt-get autoclean
```

## 以最高权限开启文件管理

```
sudo nautilus
```
