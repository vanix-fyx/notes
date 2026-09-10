# 1 Linux命令

## 1.1 目录/文件操作命令

### pwd ：打印当前所在路径

| 命令  | 选项  | 参数  |
| :-: | :-: | :-: |
| pwd |  \  |  \  |
### cd ：改变路径、切换路径

| 命令  | 选项  |  参数  |
| :-: | :-: | :--: |
| cd  |  \  | [目录] |
### mkdir ：创建目录

| 命令  | 选项 |  参数  |
| :---: | :--: | :----: |
| mkdir |  -p  | [目录] |

```
-p : parents,创建目录及子目录
example:
mkdir dir0
mkdir dir1/dir2
```

### rmdir ：删除目录

| 命令  | 选项 |  参数  |
| :---: | :--: | :----: |
| rmdir |  \   | [目录] |

### ls ：列出列表内容

| 命令 |    选项    |  参数  |
| :--: | :--------: | :----: |
|  ls  | -l  -a  -h | [目录] |

```
-l : long,显示文件更完整信息
-a : all,显示当前目录下文件及隐藏文件
-h : human-readable,大小以K/M/G等可读方式列出来
example:
ls -l	ls -a	ls -la	ls -lh
```

### cp : 复制

| 命令 |    选项    |            参数             |
| :--: | :--------: | :-------------------------: |
|  cp  | -r  -f  -d | [文件/文件夹] [文件/文件夹] |

```
-r： recursive，递归地，即复制所有文件
-f： force，强制覆盖
-d：如果源文件为链接文件，也只是把它作为链接文件复制过去，而不是复制
实际文件
example
复制目录时，常用如下命令：
cp -rfd dir_a dir_b
```

### rm : 删除文件或目录

| 命令 |  选项  |    参数     |
| :--: | :----: | :---------: |
|  rm  | -r  -f | 文件/文件夹 |

```
-r： recursive，递归地，即删除所有文件
-f： force，强制删除
```

### mv : 移动文件或目录，也可以用于重命名

| 命令 | 选项 | 参数                            |
| ---- | ---- | ------------------------------- |
| mv   | -f   | [文件/文件夹] [目标路径/新名字] |

```bash
-f : force，强制覆盖

作用:
1. 移动文件
2. 移动文件夹
3. 重命名文件
4. 重命名文件夹
example:

1. 把文件移动到指定目录
mv file.txt dir

2. 把文件夹移动到指定目录
mv dir1 dir2

说明:
如果dir2已经存在，表示把dir1移动到dir2目录里面
移动后路径为:
dir2/dir1

3. 重命名文件
mv old.txt new.txt

4. 重命名文件夹
mv old_dir new_dir

说明:
如果new_dir不存在，表示把old_dir重命名为new_dir
注意:
mv移动目录时不需要加 -r
cp复制目录时才需要加 -r

example:
mv dir1 dir2        移动目录
cp -r dir1 dir2     复制目录
```

### cat : 串联文件的内容并打印出来

| 命令 | 选项 | 参数 |
| :--: | :--: | :--: |
| cat  |  \   | 文件 |

```
example:
cat file1.txt file2.txt		串联文件并一次全部打印在标准输出中
```

### touch : 修改文件的时间，如果文件不存在泽创建空文件

| 命令  | 选项 |  参数  |
| :---: | :--: | :----: |
| touch |  \   | 文件名 |

## 1.2 改变文件的权限和属性

### chgrp : 改变文件所属用户组

| 命令  | 选项 |        参数         |
| :---: | :--: | :-----------------: |
| chgrp |  -R  | [用户组] [文件/目录] |

```
-R : recursive，递归地，即连同目录下的所有文件一起修改
example:
chgrp users file.txt
chgrp -R users dir
```

### chown : 改变文件的所有者

|  命令   | 选项  |        参数        |
| :---: | :-: | :--------------: |
| chown | -R  | [用户/用户组] [文件/目录] |

```
-R : recursive，递归地，即连同目录下的所有文件一起修改
example:
chown book file.txt
chown book:book file.txt
chown -R book:book dir
```

### chmod : 改变文件的权限

| 命令  | 选项 |       参数        |
| :---: | :--: | :---------------: |
| chmod |  -R  | [权限] [文件/目录] |

```
-R : recursive，递归地，即连同目录下的所有文件一起修改

权限说明:
r : read，可读，数字为4
w : write，可写，数字为2
x : execute，可执行，数字为1

u : user，文件所有者
g : group，文件所属用户组
o : others，其他用户
a : all，所有用户

example:
chmod 755 file.sh
chmod u+x file.sh
chmod g-w file.txt
chmod -R 755 dir
```

## 1.3 查找/搜索命令

### find : 在指定目录下查找文件

| 命令 |       选项        |        参数        |
| :--: | :---------------: | :----------------: |
| find | -name -type -size | [目录] [查找条件] |

```
-name : 按文件名查找
-type : 按文件类型查找，f表示普通文件，d表示目录
-size : 按文件大小查找

example:
find . -name "file.txt"
find . -name "*.c"
find /home -type d -name "dir"
find . -type f -size +10M
```

### grep : 在文件中查找指定字符串

| 命令 |    选项     |       参数        |
| :--: | :---------: | :---------------: |
| grep | -n -r -i -v | [字符串] [文件名] |

```
-n : number，显示匹配内容所在的行号
-r : recursive，递归查找目录下的所有文件
-i : ignore-case，忽略大小写
-v : invert-match，显示不匹配的行

example:
grep "main" file.c
grep -n "main" file.c
grep -r "hello" .
grep -rn "printf" ./src
```

## 1.4 压缩/解压缩命令

### gzip : 压缩/解压.gz文件

| 命令 | 选项 |    参数    |
| :--: | :--: | :--------: |
| gzip |  -d  | [文件名] |

```
-d : decompress，解压缩

说明:
gzip只能压缩文件，不能直接压缩目录
压缩后原文件会变成.gz文件

example:
gzip file.txt
gzip -d file.txt.gz
```

### bzip2 : 压缩/解压.bz2文件

| 命令  | 选项 |    参数    |
| :---: | :--: | :--------: |
| bzip2 |  -d  | [文件名] |

```
-d : decompress，解压缩

说明:
bzip2只能压缩文件，不能直接压缩目录
压缩后原文件会变成.bz2文件

example:
bzip2 file.txt
bzip2 -d file.txt.bz2
```

### tar : 打包/解包文件

| 命令 |      选项       |        参数         |
| :--: | :-------------: | :-----------------: |
| tar  | -c -x -v -f -z -j -J | [压缩包] [文件/目录] |

```
-c : create，创建新的打包文件
-x : extract，解包
-v : verbose，显示过程
-f : file，指定文件名，f后面一般紧跟文件名
-z : 使用gzip，对应.tar.gz
-j : 使用bzip2，对应.tar.bz2
-J ：使用 xz，对应 .tar.xz

注意：
1. tar 的选项区分大小写，-j 和 -J 的作用不同
2. tar 选项前面的“-”可以省略
   tar -xJf file.tar.xz
   tar xJf file.tar.xz
   上面两条命令作用相同
3. 建议自己使用时统一加“-”，方便阅读和记忆

example:
tar -cvf dir.tar dir
tar -xvf dir.tar
tar -czvf dir.tar.gz dir
tar -xzvf dir.tar.gz
tar -cjvf dir.tar.bz2 dir
tar -xjvf dir.tar.bz2
```

## 1.5 vim 编辑器

### 1.5.1 vim : 打开或新建文件

| 命令 | 选项 | 参数   |
| ---- | ---- | ------ |
| vim  | \    | [文件] |

```bash
作用:
使用 vim 打开文件
如果文件不存在，则新建文件

说明:
vim 是 vi 的增强版，日常 Linux 开发中更常用
vim 兼容 vi，大部分 vi 命令在 vim 中也能使用

example:
vim file.txt
vim main.c
```

### 1.5.2 vim 的三种模式

| 模式     | 说明                                            |
| -------- | ----------------------------------------------- |
| 命令模式 | vim 打开后默认进入，用来移动、复制、删除、粘贴等 |
| 编辑模式 | 用来输入和修改文字                              |
| 底行模式 | 用来保存、退出、查找、显示行号等                |

```bash
说明:
命令模式 -> 编辑模式:
按 i、a、o 等按键

编辑模式 -> 命令模式:
按 Esc

命令模式 -> 底行模式:
按 :
```

### 1.5.3 进入编辑模式

| 命令 | 说明                         |
| ---- | ---------------------------- |
| i    | 在光标前开始插入             |
| a    | 在光标后开始插入             |
| o    | 在当前行下一行新建一行并插入 |
| I    | 在当前行行首开始插入         |
| A    | 在当前行行尾开始插入         |
| O    | 在当前行上一行新建一行并插入 |

```bash
常用:
i   在光标前编辑
a   在光标后编辑
o   新开下一行编辑

退出编辑模式:
Esc
```

### 1.5.4 命令模式下移动光标

| 命令       | 说明              |
| -------- | --------------- |
| h        | 光标向左移动          |
| j        | 光标向下移动          |
| k        | 光标向上移动          |
| l        | 光标向右移动          |
| 0        | 移动到当前行行首        |
| $        | 移动到当前行行尾        |
| gg       | 移动到文件第一行        |
| G        | 移动到文件最后一行       |
| nG       | 移动到第 n 行，例如 10G |
| Ctrl + f | 向下翻一页           |
| Ctrl + b | 向上翻一页           |

```bash
example:
gg      跳到文件开头
G       跳到文件结尾
10G     跳到第10行
0       跳到当前行开头
$       跳到当前行结尾
```

### 1.5.5 复制、删除、粘贴、撤销

| 命令     | 说明                   |
| -------- | ---------------------- |
| yy       | 复制当前行             |
| nyy      | 复制 n 行，例如 3yy    |
| dd       | 删除当前行             |
| ndd      | 删除 n 行，例如 3dd    |
| x        | 删除光标所在字符       |
| p        | 粘贴到光标所在位置之后 |
| P        | 粘贴到光标所在位置之前 |
| u        | 撤销上一步操作         |
| Ctrl + r | 取消撤销               |

```bash
example:
yy      复制当前行
3yy     复制当前行开始的3行
dd      删除当前行
3dd     删除当前行开始的3行
x       删除一个字符
p       粘贴
u       撤销
```

### 1.5.6 查找命令

| 命令    | 说明           |
| ------- | -------------- |
| /字符串 | 向下查找字符串 |
| ?字符串 | 向上查找字符串 |
| n       | 查找下一个     |
| N       | 查找上一个     |

```bash
example:
/hello
n
N

说明:
输入 /hello 后，按回车开始查找 hello
n 表示继续查找下一个
N 表示查找上一个
```

### 1.5.7 底行模式命令

| 命令      | 说明                    |
| --------- | ----------------------- |
| :w        | 保存                    |
| :q        | 退出                    |
| :wq       | 保存并退出              |
| :q!       | 不保存，强制退出        |
| :set nu   | 显示行号                |
| :set nonu | 取消显示行号            |
| :n        | 跳转到第 n 行，例如 :10 |

```bash
example:
:w
:q
:wq
:q!
:set nu
:set nonu
:10
```


## 1.6 其他命令

### exit : 退出当前终端、shell或登录用户

| 命令 | 选项 | 参数 |
| ---- | ---- | ---- |
| exit | \    | \    |

```bash
作用:
退出当前所在的shell环境

常见使用场景:
1. 在普通终端中执行exit，可以关闭当前终端会话
2. 使用su切换用户后，执行exit可以退回到原来的用户
3. 使用adb shell进入开发板后，执行exit可以退出开发板，回到虚拟机终端
4. 使用ssh远程登录设备后，执行exit可以退出远程登录
```

### hostname -I : 打印本机IP地址

| 命令     | 选项 | 参数 |
| -------- | ---- | ---- |
| hostname | -I   | \    |

```bash
-I : 打印本机所有IP地址

example:
hostname -I
说明:
hostname -I 可以直接打印当前机器的IP地址
如果是在虚拟机中执行，打印的是虚拟机的IP地址
如果是在开发板中执行，打印的是开发板的IP地址

注意:
这里是大写的 I，不是小写的 l
```

### ifconfig : 查看网络信息和IP地址

| 命令     | 选项 | 参数 |
| -------- | ---- | ---- |
| ifconfig | \    | \    |

```bash
作用:
查看当前机器的网卡信息和IP地址

example:
ifconfig
说明:
ifconfig显示的信息比较多
其中 inet 后面的地址就是IP地址

常见网卡:
eth0 : 有线网卡
wlan0 : 无线网卡
lo : 本地回环网卡，不是外部网络IP

example:
eth0      Link encap:Ethernet
          inet addr:192.168.1.100

这里的192.168.1.100就是IP地址
```

### echo : 打印内容或向文件写入内容

| 命令 | 选项  | 参数     |
| ---- | ----- | -------- |
| echo | -n -e | [字符串] |

```bash
作用:
把内容打印到终端
也可以配合重定向，把内容写入文件
常用选项:

-n:
输出后不换行

-e:
识别转义字符，例如 \n、\t
example:
echo hello
echo -n hello
echo -e "hello\nworld"
配合重定向使用:

>  :
覆盖写入文件

>> :
追加写入文件
example:
echo hello > file.txt
echo world >> file.txt
说明:
echo hello > file.txt
表示把 hello 写入 file.txt
如果 file.txt 原来有内容，会被清空后重新写入

echo world >> file.txt
表示把 world 追加到 file.txt 末尾
不会清空原文件内容
开发板中常见用法:

echo 0 > /sys/class/graphics/fb0/blank
echo 1 > /sys/class/graphics/fb0/blank
说明:
这种写法是向系统文件写入指定值
常用于控制开发板上的某些设备或内核接口
```

------

### umask : 查看或设置默认权限掩码

| 命令  | 选项 | 参数       |
| ----- | ---- | ---------- |
| umask | \    | [权限掩码] |

```bash
作用:
umask 用来控制新建文件或目录的默认权限
查看当前 umask:
umask
example:
umask
常见输出:
0022
说明:
umask 表示需要从默认权限中去掉哪些权限

普通文件默认最大权限:
666

目录默认最大权限:
777
常见情况:

umask 为 022 时:

新建文件权限:
666 - 022 = 644

新建目录权限:
777 - 022 = 755
权限含义:

644:
文件所有者可读可写
同组用户只读
其他用户只读

755:
目录所有者可读可写可执行
同组用户可读可执行
其他用户可读可执行
临时设置 umask:
umask 022
umask 002
umask 000
说明:
umask 022:
常见默认值，新建文件一般是 644，新建目录一般是 755

umask 002:
同组用户也可以写，常用于多人协作目录

umask 000:
不去掉任何权限，新建文件和目录权限较开放
注意:
umask 只影响新创建的文件或目录
不会修改已经存在的文件或目录权限

如果要修改已有文件权限，使用 chmod
简单记忆:

chmod:
修改已有文件权限

umask:
决定以后新建文件或目录的默认权限
```

### hexdump : 以十六进制显示文件内容

| 命令    | 选项 | 参数     |
| ------- | ---- | -------- |
| hexdump | -C   | [文件名] |

```bash
作用:
以十六进制方式查看文件内容
常用于查看二进制文件、字符编码、文件真实内容等
常用命令:
hexdump -C file.txt
说明:
-C:
以比较直观的格式显示文件内容

左边:
文件偏移地址

中间:
十六进制数据

右边:
对应的 ASCII 字符
不可显示字符会用 . 表示
example:
hexdump -C test.txt
```

------

### xxd : 以十六进制显示文件内容

| 命令 | 选项 | 参数     |
| ---- | ---- | -------- |
| xxd  | \    | [文件名] |

```bash
作用:
以十六进制方式查看文件内容
显示效果和 hexdump -C 类似
example:
xxd test.txt
简单记忆:
hexdump -C file.txt
xxd file.txt

这两个都可以把文件内容按十六进制显示出来
```

### ps : 查看当前系统中的进程

| 命令 | 选项    | 参数 |
| ---- | ------- | ---- |
| ps   | -ef aux | \    |

```bash
作用:
查看当前系统中正在运行的进程
常用命令:

ps
查看当前终端相关的进程

ps -ef
查看系统中所有进程，常用于 Linux

ps aux
查看系统中所有进程，显示信息更详细

ps | grep 进程名
查找指定进程
example:
ps
ps -ef
ps aux
ps | grep adbd
ps -ef | grep ssh
常见字段说明:

PID:进程号

PPID:父进程号

USER:运行该进程的用户

CMD:启动该进程的命令

%CPU:CPU 占用率

%MEM:内存占用率

常见用法:
1. 查看 adbd 是否正在运行
ps | grep adbd

2. 查看 ssh 相关进程
ps -ef | grep ssh

3. 找到进程号后结束进程
kill 进程号
说明:
进程就是正在运行的程序
比如 shell、adbd、ssh、应用程序等，都可以看作进程
```

### stty：查看或设置终端窗口大小

```bash
stty size
作用：
查看当前终端窗口的行数和列数。

输出格式：
行数 列数
stty rows 35 cols 51
作用：
把当前终端设置为 35 行、51 列。

说明：
rows 表示行数。
cols 表示列数。

该设置只对当前终端生效，关闭终端后通常会失效。
```

## 1.7 adb实现板子与虚拟机交互的命令

### adb : Android Debug Bridge，用于虚拟机和开发板交互

| 命令 | 选项 | 参数 |
| ---- | ---- | ---- |
| adb  | \    | \    |

```
adb : Android Debug Bridge，安卓调试桥
作用 : 让虚拟机和开发板之间进行连接、进入shell、传输文件等操作

说明:
使用adb之前，需要保证开发板已经启动，并且开发板中运行了adbd服务
虚拟机中需要能识别到开发板，一般通过USB线或网络连接
```

### adb devices : 查看已经连接的设备

| 命令 | 选项    | 参数 |
| ---- | ------- | ---- |
| adb  | devices | \    |

```
作用:
查看虚拟机是否已经识别到开发板

example:
adb devices

可能出现的结果:
List of devices attached
1234567890abcdef    device

说明:
device : 表示设备连接正常
offline : 表示设备连接异常，可以重新插拔USB线或重启adb服务
没有设备 : 表示虚拟机没有识别到开发板
```

### adb shell : 进入开发板命令行

| 命令 | 选项  | 参数 |
| ---- | ----- | ---- |
| adb  | shell | \    |

```
作用:
从虚拟机进入开发板的Linux命令行环境

example:
adb shell

退出开发板shell:
exit
```

### adb push : 从虚拟机发送文件到开发板

| 命令 | 选项 | 参数                          |
| ---- | ---- | ----------------------------- |
| adb  | push | [虚拟机中的文件] [开发板路径] |

```
作用:
把虚拟机中的文件或目录复制到开发板中

example:
adb push hello /tmp
adb push file.txt /root
adb push dir /tmp

说明:
前面的路径是虚拟机中的路径
后面的路径是开发板中的路径
```

### adb pull : 从开发板拉取文件到虚拟机

| 命令 | 选项 | 参数                          |
| ---- | ---- | ----------------------------- |
| adb  | pull | [开发板中的文件] [虚拟机路径] |

```
作用:
把开发板中的文件或目录复制到虚拟机中

example:
adb pull /tmp/hello .
adb pull /root/file.txt ~/work
adb pull /tmp/dir ./

说明:
前面的路径是开发板中的路径
后面的路径是虚拟机中的路径
```

### adb reboot : 重启开发板

| 命令 | 选项   | 参数 |
| ---- | ------ | ---- |
| adb  | reboot | \    |

```
作用:
通过虚拟机命令重启开发板

example:
adb reboot
```

### adb root : 以root权限重启adbd服务

| 命令 | 选项 | 参数 |
| ---- | ---- | ---- |
| adb  | root | \    |

```
作用:
让开发板上的adbd服务以root权限运行

example:
adb root

说明:
有些开发板支持adb root，有些系统不支持
如果提示adbd cannot run as root，说明当前系统不支持该命令
```

### adb remount : 重新挂载系统分区为可写

| 命令 | 选项    | 参数 |
| ---- | ------- | ---- |
| adb  | remount | \    |

```
作用:
把开发板的系统分区重新挂载为可读写，方便修改系统文件

example:
adb root
adb remount

说明:
通常需要先执行adb root，再执行adb remount
有些开发板或系统不支持该命令
```

### adb start-server/kill-server : 启动或关闭adb服务

| 命令 | 选项                     | 参数 |
| ---- | ------------------------ | ---- |
| adb  | start-server/kill-server | \    |

```
作用:
启动或关闭虚拟机中的adb服务

example:
adb start-server
adb kill-server
adb start-server
adb devices

说明:
当adb devices看不到设备，或者设备显示offline时，可以尝试重启adb服务
```

### adb connect/disconnect : 通过网络连接或断开开发板

| 命令 | 选项               | 参数           |
| ---- | ------------------ | -------------- |
| adb  | connect/disconnect | [开发板IP地址] |

```
作用:
通过网络连接开发板，而不是通过USB连接

example:
adb connect 192.168.1.100
adb disconnect 192.168.1.100

说明:
开发板和虚拟机需要在同一个网络中
开发板需要支持网络adb连接
```

### adb常用操作流程

```
1. 查看是否连接到开发板
adb devices

2. 进入开发板命令行
adb shell

3. 从虚拟机发送文件到开发板
adb push hello /tmp

4. 从开发板拉取文件到虚拟机
adb pull /tmp/hello .

5. 重启开发板
adb reboot
```
## 1.8 Linux驱动相关命令

### insmod

加载指定的 `.ko` 内核模块。

```bash
insmod 模块文件
```

例如：

```bash
insmod hello_drv.ko
```

---

### rmmod

卸载已经加载的内核模块。

```bash
rmmod 模块名
```

例如：

```bash
rmmod hello_drv
```

模块名通常不写 `.ko` 后缀。

---

### lsmod

查看当前已经加载到内核中的模块。

```bash
lsmod
```

可以用来确认驱动模块是否已经加载成功。

---

### dmesg

查看 Linux 内核日志，驱动中 printk 输出的信息可以通过该命令查看。

```bash
dmesg
```

实时查看新产生的内核日志：

```bash
dmesg -w
```

---

### mknod

手动创建设备节点。

```bash
mknod 设备节点 类型 主设备号 次设备号
```

例如：

```bash
mknod /dev/hello c 240 0
```

其中：

```text
/dev/hello  → 设备节点
c           → 字符设备
240         → 主设备号
0           → 次设备号
```

---

### cat /proc/devices

查看当前系统已经注册的字符设备和块设备及其主设备号。

```bash
cat /proc/devices
```

例如可能看到：

```text
Character devices:
240 hello
```

表示名称为 hello 的字符设备使用主设备号 240。

---

### ls /dev

查看 `/dev` 目录下已经存在的设备节点。

```bash
ls /dev
```

也可以直接查看指定设备：

```bash
ls -l /dev/hello
```

---

### uname -r

查看当前正在运行的 Linux 内核版本。

```bash
uname -r
```

例如：

```text
4.9.88
```

编译内核模块时，需要特别注意目标开发板的内核版本和内核源码是否匹配。

---

### modprobe

按模块名加载内核模块，并自动处理模块之间的依赖关系。

```bash
modprobe 模块名
```

卸载：

```bash
modprobe -r 模块名
```

与 insmod 不同，modprobe 通常从系统的模块目录中查找模块，而不是直接指定 `.ko` 文件路径。

---

### modinfo

查看内核模块的信息。

```bash
modinfo 模块文件
```

例如：

```bash
modinfo hello_drv.ko
```

可以查看模块名称、许可证、依赖等信息。

---

常用驱动调试流程：

```bash
# 加载驱动
insmod hello_drv.ko

# 确认模块是否已经加载
lsmod

# 查看内核打印
dmesg

# 查看设备节点
ls -l /dev/hello

# 卸载驱动
rmmod hello_drv
```
# 2 环境配置

## 2.1 编译环境

在进行嵌入式 Linux 开发时，需要先配置好编译环境。

编译环境主要包括两部分：

```text
1. gcc 编译环境：用于编译能在 Ubuntu 虚拟机上运行的程序
2. ARM 交叉编译环境：用于编译能在 ARM 开发板上运行的程序
```

------

### 2.1.1 gcc 编译

`gcc` 是 Linux 下常用的 C 语言编译器，用来把 `.c` 源文件编译成可执行程序。

例如有一个源文件：

```bash
hello.c
```

使用 gcc 编译：

```bash
gcc hello.c -o hello
```

含义：

```text
gcc       使用 gcc 编译器
hello.c   要编译的 C 源文件
-o        指定输出文件名
hello     生成的可执行程序名
```

运行程序：

```bash
./hello
```

如果不使用 `-o` 指定输出文件名：

```bash
gcc hello.c
```

默认会生成：

```bash
a.out
```

运行方式：

```bash
./a.out
```

总结：

```text
gcc 编译出来的程序，是给 Ubuntu 虚拟机运行的。
```

------

### 2.1.2 ARM 交叉编译

开发板使用的是 ARM 架构，而 Ubuntu 虚拟机一般是 x86 架构。

如果想在 Ubuntu 虚拟机中编译出能在 ARM 开发板上运行的程序，就需要使用 ARM 交叉编译器。

交叉编译可以理解为：

```text
在 Ubuntu 虚拟机上编译
生成给 ARM 开发板运行的程序
```

韦东山 i.MX6ULL 开发环境中常用的交叉编译器是：

```bash
arm-buildroot-linux-gnueabihf-gcc
```

使用方法：

```bash
arm-buildroot-linux-gnueabihf-gcc hello.c -o hello
```

含义：

```text
arm-buildroot-linux-gnueabihf-gcc   ARM 交叉编译器
hello.c                             要编译的 C 源文件
-o hello                            生成名为 hello 的可执行程序
```

编译完成后，生成的 `hello` 不是给 Ubuntu 虚拟机运行的，而是给 ARM 开发板运行的。

可以通过 adb 发送到开发板：

```bash
adb push hello /root
```

进入开发板：

```bash
adb shell
```

在开发板中运行：

```bash
cd /root
./hello
```

------

### 2.1.3 配置 ARM 交叉编译环境

为了让系统能够找到 ARM 交叉编译器，需要配置环境变量。

执行：

```bash
export ARCH=arm
```

含义：

```text
指定目标平台架构是 ARM
```

执行：

```bash
export CROSS_COMPILE=arm-buildroot-linux-gnueabihf-
```

含义：

```text
指定交叉编译器前缀
```

注意：最后的 `-` 不能漏掉。

例如内核或驱动编译时，会自动把：

```bash
$(CROSS_COMPILE)gcc
```

组合成：

```bash
arm-buildroot-linux-gnueabihf-gcc
```

继续执行：

```bash
export PATH=$PATH:/home/book/100ask_imx6ull-sdk/ToolChain/arm-buildroot-linux-gnueabihf_sdk-buildroot/bin
```

含义：

```text
把交叉编译器所在目录加入 PATH 环境变量
```

加入之后，在任意目录都可以直接使用：

```bash
arm-buildroot-linux-gnueabihf-gcc
```

------

### 2.1.4 检查交叉编译器是否配置成功

查看交叉编译器版本：

```bash
arm-buildroot-linux-gnueabihf-gcc -v
```

如果能看到版本信息，说明交叉编译器可以正常使用。

查看交叉编译器路径：

```bash
which arm-buildroot-linux-gnueabihf-gcc
```

如果输出类似：

```bash
/home/book/100ask_imx6ull-sdk/ToolChain/arm-buildroot-linux-gnueabihf_sdk-buildroot/bin/arm-buildroot-linux-gnueabihf-gcc
```

说明系统已经能找到这个交叉编译器。

------

### 2.1.5 gcc 编译和 ARM 编译对比

| 编译方式 | 编译器                              | 运行位置      |
| -------- | ----------------------------------- | ------------- |
| 普通编译 | `gcc`                               | Ubuntu 虚拟机 |
| 交叉编译 | `arm-buildroot-linux-gnueabihf-gcc` | ARM 开发板    |

普通 gcc 编译：

```bash
gcc hello.c -o hello
```

生成的 `hello` 是给 Ubuntu 虚拟机运行的。

ARM 交叉编译：

```bash
arm-buildroot-linux-gnueabihf-gcc hello.c -o hello
```

生成的 `hello` 是给 ARM 开发板运行的。

可以使用 `file` 命令查看程序属于哪种架构：

```bash
file hello
```

如果是 Ubuntu 程序，可能显示：

```text
ELF 64-bit LSB executable, x86-64
```

如果是开发板程序，可能显示：

```text
ELF 32-bit LSB executable, ARM
```

------

### 2.1.6 常用编译流程

在 Ubuntu 虚拟机中交叉编译：

```bash
arm-buildroot-linux-gnueabihf-gcc hello.c -o hello
```

把程序发送到开发板：

```bash
adb push hello /root
```

进入开发板：

```bash
adb shell
```

在开发板中运行：

```bash
cd /root
./hello
```

如果程序无法运行，可能需要添加执行权限：

```bash
chmod +x hello
./hello
```

------

一句话总结：

```text
gcc 是给 Ubuntu 虚拟机编译程序用的；
arm-buildroot-linux-gnueabihf-gcc 是给 ARM 开发板编译程序用的；
-o 用来指定生成的可执行文件名。
```

# 3 编译

## 3.0 编译器预定义内容
### `__FILE__`、`__LINE__`

```c
/* 不需要包含头文件，由编译器直接提供 */

__FILE__    /* 当前源文件的文件名字符串 */
__LINE__    /* 当前代码所在的行号 */
```

`__FILE__` 表示当前源文件名，结果是字符串。

`__LINE__` 表示当前代码所在的源文件行号，结果是整数。

常用于记录代码所在位置，方便调试。

```c
static const char *source_file = __FILE__;
static int source_line = __LINE__;

/*
 * 假设这段代码位于 hello_drv.c 第 20 行附近：
 *
 * source_file -> "hello_drv.c"
 * source_line -> 对应的源代码行号
 */
```

```c
 printk("%s line %d\n", __FILE__, __LINE__);
```
### `__FUNCTION__`

```c
/* 不需要包含头文件，由 GCC 编译器提供 */

__FUNCTION__
```

`__FUNCTION__` 表示当前所在函数的函数名。

它在 GCC 中是编译器提供的预定义标识符，**不是预处理宏**。


```c
static const char *get_function_name(void)
{
    return __FUNCTION__;
}

/*
 * 调用 get_function_name() 时，
 * 返回的字符串为 "get_function_name"。
 */
```

```c

printk("%s\n", __FUNCTION__);
```

在 hello_drv_read 函数中使用时，得到的字符串为：

```text
hello_drv_read
```

标准 C 中功能对应的标识符是 **func**。
## 3.1 编译的基本概念

```bash
编译:
把人能看懂的C语言代码，转换成机器能运行的可执行程序

源文件:
.c文件，例如 hello.c

头文件:
.h文件，例如 stdio.h

目标文件:
.o文件，是编译过程中生成的中间文件

可执行文件:
最终可以运行的程序，例如 hello
说明:
C语言源文件不能直接运行，需要经过编译器编译后才能运行

在Linux虚拟机中，常用gcc编译程序
在开发板中，如果CPU架构是ARM，一般需要使用ARM交叉编译器编译程序
```

## 3.2 编译流程

C语言从源文件到可执行文件，一般经过四个步骤：

```bash
1. 预处理
2. 编译
3. 汇编
4. 链接
```

| 步骤   | 作用                               | 生成文件   |
| ------ | ---------------------------------- | ---------- |
| 预处理 | 处理头文件、宏定义等               | .i文件     |
| 编译   | 把C代码转换成汇编代码              | .s文件     |
| 汇编   | 把汇编代码转换成目标文件           | .o文件     |
| 链接   | 把目标文件和库文件链接成可执行程序 | 可执行文件 |

```bash
完整流程:
hello.c  ->  hello.i  ->  hello.s  ->  hello.o  ->  hello
源文件       预处理文件    汇编文件     目标文件     可执行文件
```

## 3.3 gcc选项

#### 常用选项

| 选项          | 作用                   |
| ----------- | -------------------- |
| -o          | 指定输出文件名              |
| -E          | 只进行预处理               |
| -S          | 只进行预处理和编译，生成汇编文件     |
| -c          | 只编译生成目标文件，不链接        |
| -Wall       | 显示更多警告信息             |
| -Werror     | 将警告当成错误处理            |
| -g          | 生成调试信息，方便gdb调试       |
| -I   （大写的i） | 指定头文件路径              |
| -L          | 指定库文件路径              |
| -l   （小写的L） | 指定链接的库               |
| -D          | 定义宏                  |
| -O          | 优化程序                 |
| -v          | verbose，显示编译过程中的详细信息 |

#### **字符编码相关选项**

| 选项                     | 作用                                             |
| ------------------------ | ------------------------------------------------ |
| `-finput-charset=GB2312` | 指定 C 源文件使用 GB2312 编码                    |
| `-finput-charset=UTF-8`  | 指定 C 源文件使用 UTF-8 编码                     |
| `-fexec-charset=GB2312`  | 指定可执行程序中普通字符和字符串使用 GB2312 编码 |
| `-fexec-charset=UTF-8`   | 指定可执行程序中普通字符和字符串使用 UTF-8 编码  |

```bash
说明:

-finput-charset:
指定 gcc 按什么编码读取源代码文件

-fexec-charset:
指定源代码中的普通字符和字符串，编译后使用什么编码
```

输入和输出编码不同时，可以组合使用：

```bash
gcc -finput-charset=GB2312 -fexec-charset=UTF-8 main.c -o app
说明:
上面的命令表示:

源文件使用 GB2312 编码
编译后，程序中的普通字符和字符串转换为 UTF-8 编码
简单记忆:

input:
gcc 如何读取源文件

exec:
字符和字符串编译后使用什么编码
```

### `-M` 相关选项

主要用于生成头文件依赖关系，常配合 Makefile 使用。

| 选项   | 作用                                                 |
| ------ | ---------------------------------------------------- |
| `-M`   | 生成依赖关系，包含系统头文件                         |
| `-MM`  | 生成依赖关系，不包含系统头文件                       |
| `-MD`  | 编译源文件，同时生成 `.d` 依赖文件，包含系统头文件   |
| `-MMD` | 编译源文件，同时生成 `.d` 依赖文件，不包含系统头文件 |
| `-MF`  | 指定生成的依赖文件名                                 |
| `-MT`  | 指定依赖规则中的目标名                               |
| `-MP`  | 为头文件生成伪目标，防止头文件删除后 make 报错       |

```bash
example:
gcc -M main.c
作用:
输出 main.c 依赖了哪些头文件
包含系统头文件

example:
gcc -MM main.c
作用:
输出 main.c 依赖了哪些用户自己的头文件
不包含系统头文件

example:
gcc -MMD -c main.c -o main.o
作用:
编译 main.c 生成 main.o
同时生成 main.d 依赖文件
main.d 中记录 main.o 依赖哪些头文件

example:
gcc -MMD -MP -c main.c -o main.o
说明:
这是 Makefile 中比较常用的写法

example:
gcc -c c.c -o c.o -MD -MF c.d
作用：
把 c.c 编译成 c.o，同时生成依赖文件 c.d，c.d 中记录 c.c 依赖了哪些头文件。

-MMD:
生成用户头文件依赖，不包含系统头文件

-MP:
给头文件生成伪目标，避免删除头文件后 make 报错
简单记忆:

-M   只生成依赖，包含系统头文件
-MM  只生成依赖，不包含系统头文件

-MD   编译 + 生成依赖，包含系统头文件
-MMD  编译 + 生成依赖，不包含系统头文件

-MF   指定 .d 文件名
-MT   指定依赖目标名
-MP   防止头文件删除后 make 报错
```

### -I 头文件路径

| 命令 | 选项 | 参数         |
| ---- | ---- | ------------ |
| gcc  | -I   | [头文件目录] |

```bash
-I : include，指定头文件所在目录

example:
gcc main.c add.c -I ./include -o app

说明:
-I 后面接的是头文件所在的目录，不是具体的头文件名

例如:
-I ./include
表示告诉gcc去当前目录下的include目录中查找头文件

注意:
-I 只能解决找不到.h头文件的问题
如果函数的实现写在.c文件中，编译时仍然需要把对应的.c文件一起编译
```

### -L -l 库文件路径

| 命令 | 选项  | 参数                |
| ---- | ----- | ------------------- |
| gcc  | -L -l | [库文件目录] [库名] |

```bash
example:
gcc main.c -L ./lib -ladd -o app
说明:
使用 gcc 编译 main.c，并且到 ./lib 目录下查找 add 库，把 main.c 和这个库链接起来，最后生成可执行程序 app。
如果不使用 -L 指定库文件目录，gcc只会去系统默认库目录中查找库文件。

-L : 指定库文件所在目录
-l : 指定链接哪个库

-ladd 表示链接 libadd.so 或 libadd.a

-ladd 的理解:

-l 是 gcc 的选项，表示链接指定的库
add 是库名

-ladd 可以理解成:
-l add

但是 gcc 实际查找库文件时，不是直接找 add 这个文件，而是会自动在库名前面加 lib，在后面匹配 .so 或 .a

所以:-ladd  表示链接 libadd.so 或者 libadd.a

也就是说:
-lxxx 表示链接 libxxx.so 或 libxxx.a

example:
-ladd      表示链接 libadd.so 或 libadd.a
-lmath     表示链接 libmath.so 或 libmath.a
-lhello    表示链接 libhello.so 或 libhello.a

注意:
写命令时不要写成 -llibadd
因为 gcc 会自动补 lib

正确写法:
-ladd

错误写法:
-llibadd
```

## 3.4 gcc和ARM交叉编译器

```bash
普通gcc:
编译出来的程序，一般在虚拟机或电脑上运行

ARM交叉编译器:
编译出来的程序，在ARM开发板上运行
```

| 编译器                              | 编译器运行位置 | 生成程序运行位置                 | 什么时候用                           |
| ----------------------------------- | -------------- | -------------------------------- | ------------------------------------ |
| `gcc`                               | Ubuntu/电脑    | Ubuntu/电脑（通常是 x86-64）     | 编译虚拟机本机程序                   |
| `arm-linux-gcc`                     | Ubuntu/电脑    | ARM 开发板                       | 老教程里的泛称或某套旧工具链         |
| `arm-linux-gnueabihf-gcc`           | Ubuntu/电脑    | ARM Linux 开发板                 | 通用 ARM hard-float Linux 程序       |
| `arm-buildroot-linux-gnueabihf-gcc` | Ubuntu/电脑    | 使用对应 Buildroot 系统的 ARM 板 | 韦东山 SDK、配套根文件系统，优先使用 |

```bash
说明:
交叉编译:
在一个平台上编译出另一个平台运行的程序

例如:
在x86虚拟机中，编译出ARM开发板可以运行的程序
```

### 查看默认头文件和库搜索路径

```bash
echo 'main(){}' | arm-buildroot-linux-gnueabihf-gcc -E -v -
作用:
查看 ARM 交叉编译器在编译时默认搜索的头文件目录、库目录以及编译器相关配置信息。

常用于:
确认交叉编译器去哪些目录查找系统头文件和库文件。

下面是执行后找到的库目录：
#include "..." search starts here:
#include <...> search starts here:
  /home/book/100ask_imx6ull-sdk/ToolChain/arm-buildroot-linux-gnueabihf_sdk-buildroot/bin/../lib/gcc/arm-buildroot-linux-gnueabihf/7.5.0/include
  
 /home/book/100ask_imx6ull-sdk/ToolChain/arm-buildroot-linux-gnueabihf_sdk-buildroot/bin/../lib/gcc/arm-buildroot-linux-gnueabihf/7.5.0/include-fixed
 
 /home/book/100ask_imx6ull-sdk/ToolChain/arm-buildroot-linux-gnueabihf_sdk-buildroot/bin/../lib/gcc/arm-buildroot-linux-gnueabihf/7.5.0/../../../../arm-buildroot-linux-gnueabihf/include
 
 /home/book/100ask_imx6ull-sdk/ToolChain/arm-buildroot-linux-gnueabihf_sdk-buildroot/arm-buildroot-linux-gnueabihf/sysroot/usr/include
```

### 交叉编译程序的万能命令

```bash
./configure --host=arm-buildroot-linux-gnueabihf --prefix=$PWD/tmp
make
make install
作用:
使用 ARM 交叉编译工具链配置并编译源码，
最后把编译结果安装到当前目录下的 tmp 文件夹中。

适用条件:
源码目录中存在 configure 文件。
交叉编译器前缀为:
arm-buildroot-linux-gnueabihf-

执行完成后，tmp 目录中一般会生成:
bin      可执行程序
lib      库文件
include  头文件
```

## 3.5 查看程序类型

| 命令 | 选项 | 参数     |
| ---- | ---- | -------- |
| file | \    | [文件名] |

```bash
example:
file hello
说明:
file命令可以查看程序是给什么平台运行的

如果是虚拟机运行的程序，可能显示x86、x86-64
如果是开发板运行的程序，可能显示ARM
```
## 3.6 常用编译命令总结

```bash
1. 编译单个C文件
gcc hello.c -o hello

2. 运行程序
./hello

3. 只生成目标文件
gcc -c hello.c -o hello.o

4. 多文件编译
gcc main.c add.c -o app

5. 显示更多警告
gcc -Wall hello.c -o hello

6. 生成调试信息
gcc -g hello.c -o hello

7. 指定头文件路径
gcc main.c -I ./include -o app

8. 指定库文件路径
gcc main.c -L ./lib -ladd -o app

9. ARM交叉编译
arm-linux-gcc hello.c -o hello

10. 查看程序类型
file hello
```

# 4 Makefile

## 4.1 Makefile 是什么

```bash
Makefile:
用来保存编译规则的文件

make:
执行Makefile中的编译规则
作用:
工程文件较多时，不需要每次手动输入很长的gcc命令
只需要写好Makefile，然后执行make即可编译
```

## 4.2 Makefile 基本格式

```makefile
目标: 依赖文件
	命令
说明:
目标: 最终要生成的文件

依赖文件: 生成目标需要用到的文件

命令: 真正执行的编译命令

注意: 命令前面必须是Tab键，不能是空格
```

## 4.3 最简单的 Makefile

假设有一个 `hello.c` 文件：

```makefile
hello: hello.c
	gcc hello.c -o hello
	
执行编译:
make

运行程序:
./hello

说明:
hello 是目标
hello.c 是依赖文件
gcc hello.c -o hello 是编译命令
```

## 4.4 多文件编译

假设有：

```bash
main.c
add.c
add.h
```

Makefile 可以写成：

```makefile
app: main.c add.c
	gcc main.c add.c -o app
执行:
make

生成:
app
```

## 4.5 先生成 .o 文件再链接

```makefile
app: main.o add.o
	gcc main.o add.o -o app

main.o: main.c add.h
	gcc -c main.c -o main.o

add.o: add.c add.h
	gcc -c add.c -o add.o
说明:
main.c 先编译成 main.o
add.c 先编译成 add.o
最后 main.o 和 add.o 链接生成 app

好处:
如果只修改了 add.c，重新 make 时一般只会重新编译 add.c
```

## 4.6 变量与写法总结

### 4.6.1 常用变量

| 变量     | 含义               | 示例                  |
| -------- | ------------------ | --------------------- |
| `CC`     | 编译器             | `CC = gcc`            |
| `TARGET` | 最终生成的程序名   | `TARGET = app`        |
| `OBJS`   | 所有 `.o` 目标文件 | `OBJS = main.o add.o` |
| `CFLAGS` | 编译选项           | `CFLAGS = -Wall -g`   |

### 4.6.2 使用变量

| 写法        | 含义                   |
| ----------- | ---------------------- |
| `$(CC)`     | 使用 `CC` 变量的值     |
| `$(TARGET)` | 使用 `TARGET` 变量的值 |
| `$(OBJS)`   | 使用 `OBJS` 变量的值   |
| `$(CFLAGS)` | 使用 `CFLAGS` 变量的值 |

### 4.6.3 自动变量

| 自动变量 | 含义           |
| -------- | -------------- |
| `$@`     | 目标文件       |
| `$<`     | 第一个依赖文件 |
| `$^`     | 所有依赖文件   |

### 4.6.4 通配符和模式规则

| 符号 | 含义               | 常见用法                           |
| ---- | ------------------ | ---------------------------------- |
| `*`  | 匹配任意内容       | `*.o` 表示所有 `.o` 文件           |
| `%`  | 匹配文件名的一部分 | `%.o: %.c` 表示 `.c` 生成对应 `.o` |

### 4.6.5 常用 make 命令

| 命令            | 作用                   |
| ------------- | -------------------- |
| `make`        | 执行默认目标               |
| `make clean`  | 执行 `clean` 目标，清理生成文件 |
| `make app`    | 执行 `app` 目标          |
| `make -C dir` | 进入 `dir` 目录执行 `make` |

### 4.6.6 变量赋值方式

| 写法 | 名称     | 说明                         |
| ---- | -------- | ---------------------------- |
| `=`  | 延时变量 | 使用变量时，才确定最终的值   |
| `:=` | 即时变量 | 定义变量时，立刻确定值       |
| `?=` | 条件赋值 | 如果变量之前没有定义，才赋值 |
| `+=` | 追加赋值 | 在原来变量后面追加内容       |

```makefile
A = hello
B = $(A)
A = world

all:
	echo $(B)
说明:
B 使用的是 = 延时变量
所以执行 echo $(B) 时，才去看 A 的值
此时 A 已经变成 world

输出:
world
-----------------------------------------------------------------------------------
A = hello
B := $(A)
A = world

all:
	echo $(B)
说明:
B 使用的是 := 即时变量
所以 B 在定义时就已经确定为 hello
后面 A 改成 world，不影响 B

输出:
hello
-----------------------------------------------------------------------------------
CC ?= gcc
说明:
?= 表示条件赋值
如果 CC 前面没有定义，就让 CC = gcc
如果 CC 前面已经定义了，就不修改 CC
-----------------------------------------------------------------------------------
CFLAGS = -Wall
CFLAGS += -g
说明:
+= 表示追加内容
最终 CFLAGS 的值为:
-Wall -g
```

### 4.6.7 常见错误

| 错误                     | 常见原因                   | 解决方法                           |
| ------------------------ | -------------------------- | ---------------------------------- |
| `missing separator`      | 命令前面没有使用 Tab 键    | 把空格改成 Tab 键                  |
| `No rule to make target` | 依赖文件不存在或文件名写错 | 检查文件名和路径                   |
| `undefined reference`    | 链接阶段找不到函数实现     | 检查是否少编译 `.c` 文件或少链接库 |

## 4.7 Makefile 函数

Makefile 函数用于自动获取文件、替换文件名、处理路径等。

### 4.7.1 函数基本格式

```makefile
$(函数名 参数)
```

多个参数一般用逗号隔开：

```makefile
$(函数名 参数1,参数2,参数3)
```

### 4.7.2 常用函数

#### 4.7.2.1 文件查找和文件名转换

| 函数        | 作用               | 示例                           |
| ----------- | ------------------ | ------------------------------ |
| `wildcard`  | 查找匹配的文件     | `$(wildcard *.c)`              |
| `patsubst`  | 按模式替换字符串   | `$(patsubst %.c,%.o,$(SRCS))`  |
| `addprefix` | 给每个字符串加前缀 | `$(addprefix ./src/,$(FILES))` |
| `addsuffix` | 给每个字符串加后缀 | `$(addsuffix .o,$(NAMES))`     |

#### 4.7.2.2 路径和文件名处理

| 函数       | 作用                   | 示例                     |
| ---------- | ---------------------- | ------------------------ |
| `dir`      | 取目录部分             | `$(dir ./src/main.c)`    |
| `notdir`   | 去掉目录，只保留文件名 | `$(notdir ./src/main.c)` |
| `suffix`   | 取文件后缀             | `$(suffix main.c)`       |
| `basename` | 去掉文件后缀           | `$(basename main.c)`     |
| `abspath`  | 生成绝对路径           | `$(abspath ./src)`       |
| `realpath` | 生成真实绝对路径       | `$(realpath ./src)`      |

#### 4.7.2.3 字符串处理

| 函数         | 作用               | 示例                          |
| ------------ | ------------------ | ----------------------------- |
| `subst`      | 普通字符串替换     | `$(subst old,new,$(TEXT))`    |
| `strip`      | 去掉多余空格       | `$(strip $(TEXT))`            |
| `findstring` | 查找字符串         | `$(findstring debug,$(MODE))` |
| `filter`     | 保留符合模式的内容 | `$(filter %.c,$(FILES))`      |
| `filter-out` | 去掉符合模式的内容 | `$(filter-out %.h,$(FILES))`  |
| `sort`       | 排序并去重         | `$(sort $(FILES))`            |

#### 4.7.2.4 单词处理

| 函数        | 作用           | 示例                       |
| ----------- | -------------- | -------------------------- |
| `word`      | 取第 n 个单词  | `$(word 2,$(FILES))`       |
| `firstword` | 取第一个单词   | `$(firstword $(FILES))`    |
| `lastword`  | 取最后一个单词 | `$(lastword $(FILES))`     |
| `words`     | 统计单词个数   | `$(words $(FILES))`        |
| `wordlist`  | 取一段单词     | `$(wordlist 2,4,$(FILES))` |

#### 4.7.2.5条件和循环

| 函数/语句 | 作用                 | 示例                                 |
| --------- | -------------------- | ------------------------------------ |
| `if`      | 条件判断             | `$(if 条件,成立时的值,不成立时的值)` |
| `foreach` | 循环处理每个单词     | `$(foreach f,$(FILES),$(f).o)`       |
| `shell`   | 执行 Linux 命令      | `$(shell pwd)`                       |
| `ifneq`   | 判断两个值是否不相等 | `ifneq ($(ARCH),x86)`                |

### 4.7.3 函数的使用

#### 4.7.3.1 wildcard : 查找文件

```makefile
SRCS = $(wildcard *.c)
说明:
wildcard 用来查找符合条件的文件

*.c 表示当前目录下所有 .c 文件

例如当前目录有:
main.c add.c sub.c

那么:
SRCS = main.c add.c sub.c
```

#### 4.7.3.2 patsubst : 替换文件名格式

```makefile
OBJS = $(patsubst %.c,%.o,$(SRCS))
说明:
patsubst 用来把一种格式替换成另一种格式

%.c 表示 .c 文件
%.o 表示对应的 .o 文件

如果:
SRCS = main.c add.c sub.c

那么:
OBJS = main.o add.o sub.o
```

#### 4.7.3.3 wildcard 和 patsubst 配合使用

```makefile
SRCS = $(wildcard *.c)
OBJS = $(patsubst %.c,%.o,$(SRCS))
说明:
第一行自动找到所有 .c 文件
第二行把 .c 文件转换成对应的 .o 文件

这样新增 .c 文件后，一般不需要手动修改 OBJS
```

#### 4.7.3.4 shell : 执行 Linux 命令

```makefile
PWD = $(shell pwd)
说明:
shell 函数可以在 Makefile 中执行 Linux 命令

$(shell pwd)
表示执行 pwd 命令，并把结果保存到变量 PWD 中
```

#### 4.7.3.5 addprefix : 添加前缀

```makefile
FILES = main.o add.o sub.o
OBJS = $(addprefix ./obj/,$(FILES))
结果:
OBJS = ./obj/main.o ./obj/add.o ./obj/sub.o

说明:
addprefix 用来给每个单词前面添加相同的前缀
这里是给每个 .o 文件前面加上 ./obj/
```

#### 4.7.3.6 addsuffix : 添加后缀

```makefile
NAMES = main add sub
OBJS = $(addsuffix .o,$(NAMES))
结果:
OBJS = main.o add.o sub.o

说明:
addsuffix 用来给每个单词后面添加相同的后缀
这里是给 main add sub 后面都加上 .o
```

#### 4.7.3.7 dir : 获取目录部分

```makefile
FILE = ./src/main.c
DIR = $(dir $(FILE))
结果:
DIR = ./src/

说明:
dir 用来获取文件路径中的目录部分
```

#### 4.7.3.8 notdir : 获取文件名部分

```makefile
FILE = ./src/main.c
NAME = $(notdir $(FILE))
结果:
NAME = main.c

说明:
notdir 用来去掉路径，只保留文件名
```

#### 4.7.3.9 suffix : 获取文件后缀

```makefile
FILE = main.c
SUF = $(suffix $(FILE))
结果:
SUF = .c

说明:
suffix 用来获取文件后缀
```

#### 4.7.3.10 basename : 去掉文件后缀

```makefile
FILE = main.c
BASE = $(basename $(FILE))
结果:
BASE = main

说明:
basename 用来去掉文件后缀
```

#### 4.7.3.11 subst : 普通字符串替换

```makefile
TEXT = hello_world
NEW = $(subst world,linux,$(TEXT))
结果:
NEW = hello_linux

说明:
subst 用来进行普通字符串替换
这里把 world 替换成 linux
```

#### 4.7.3.12 strip : 去掉多余空格

```makefile
TEXT =    hello     linux   
NEW = $(strip $(TEXT))
结果:
NEW = hello linux

说明:
strip 会去掉开头和结尾的空格
中间多个空格会变成一个空格
```

#### 4.7.3.13 findstring : 查找字符串

```makefile
MODE = debug
RET = $(findstring debug,$(MODE))
结果:
RET = debug

说明:
findstring 用来查找某个字符串是否存在
如果找到了，返回找到的字符串
如果没找到，返回空
```

#### 4.7.3.14 filter : 保留符合条件的内容

```makefile
FILES = main.c add.c add.h README.md
CFILES = $(filter %.c,$(FILES))
结果:
CFILES = main.c add.c

说明:
filter 用来保留符合模式的内容
这里保留所有 .c 文件
```

#### 4.7.3.15 filter-out : 去掉符合条件的内容

```makefile
FILES = main.c add.c add.h README.md
NO_H = $(filter-out %.h,$(FILES))
结果:
NO_H = main.c add.c README.md

说明:
filter-out 用来去掉符合模式的内容
这里去掉所有 .h 文件
```

#### 4.7.3.16 sort : 排序并去重

```makefile
FILES = b.c a.c b.c c.c
NEW = $(sort $(FILES))
结果:
NEW = a.c b.c c.c

说明:
sort 会对内容进行排序
同时会去掉重复内容
```

#### 4.7.3.17 word : 取第 n 个单词

```makefile
FILES = main.c add.c sub.c
A = $(word 2,$(FILES))
结果:
A = add.c

说明:
word 用来取第 n 个单词
这里取第 2 个单词
```

#### 4.7.3.18 firstword : 取第一个单词

```makefile
FILES = main.c add.c sub.c
A = $(firstword $(FILES))
结果:
A = main.c

说明:
firstword 用来取第一个单词
```

#### 4.7.3.19 lastword : 取最后一个单词

```makefile
FILES = main.c add.c sub.c
A = $(lastword $(FILES))
结果:
A = sub.c

说明:
lastword 用来取最后一个单词
```

#### 4.7.3.20 words : 统计单词个数

```makefile
FILES = main.c add.c sub.c
NUM = $(words $(FILES))
结果:
NUM = 3

说明:
words 用来统计一共有多少个单词
```

#### 4.7.3.21 wordlist : 取一段单词

```makefile
FILES = main.c add.c sub.c test.c
PART = $(wordlist 2,3,$(FILES))
结果:
PART = add.c sub.c

说明:
wordlist 用来取一段单词
这里表示从第 2 个单词取到第 3 个单词
```

#### 4.7.3.22 foreach : 循环处理

```makefile
NAMES = main add sub
OBJS = $(foreach name,$(NAMES),$(name).o)
结果:
OBJS = main.o add.o sub.o

说明:
foreach 会依次取出 NAMES 中的每个单词
然后按照指定格式生成新的内容
```

#### 4.7.3.23 if : 条件判断

```makefile
DEBUG = y
CFLAGS = $(if $(DEBUG),-g,-O2)
结果:
CFLAGS = -g

说明:
if 用来做条件判断
如果 DEBUG 有值，就使用 -g
如果 DEBUG 为空，就使用 -O2
```

#### 4.7.3.24 abspath : 获取绝对路径

```makefile
PATH1 = ./src
PATH2 = $(abspath $(PATH1))
结果:
PATH2 = 当前工程目录/src

说明:
abspath 用来把相对路径转换成绝对路径
路径是否真实存在，不是重点
```

#### 4.7.3.25 realpath : 获取真实路径

```makefile
PATH1 = ./src
PATH2 = $(realpath $(PATH1))
结果:
PATH2 = 当前工程目录/src

说明:
realpath 也会转换成绝对路径
但它更强调真实存在的路径
如果路径不存在，结果可能为空
```

#### 4.7.3.26 ifneq : 判断两个值是否不相等

```makefile
ifneq ($(变量名),值)
	命令或变量定义
endif
说明:
ifneq 表示 if not equal
如果两个值不相等，就执行 ifneq 和 endif 中间的内容
ARCH = arm

ifneq ($(ARCH),x86)
CC = arm-linux-gcc
endif
说明:
如果 ARCH 不等于 x86
就把 CC 设置为 arm-linux-gcc
简单记忆:
ifeq  : 相等时执行
ifneq : 不相等时执行
endif : 条件判断结束
```

### 4.7.4 使用函数的 Makefile 示例

```makefile
CC = gcc
TARGET = app
SRCS = $(wildcard *.c)
OBJS = $(patsubst %.c,%.o,$(SRCS))

$(TARGET): $(OBJS)
	$(CC) $^ -o $@

%.o: %.c
	$(CC) -c $< -o $@

.PHONY: clean

clean:
	rm -f $(TARGET) $(OBJS)
说明:
SRCS 自动获取当前目录下所有 .c 文件
OBJS 自动把 .c 文件转换成 .o 文件
$(TARGET) 最后由所有 .o 文件链接生成
```

## 4.8 clean 清理生成文件

```makefile
clean:
	rm -f app *.o
执行:
make clean
说明:
clean 是一个清理动作
rm -f app *.o 表示删除 app 和所有 .o 文件

-f : force，强制删除
*.o : 所有 .o 文件
```

## 4.9 .PHONY 伪目标

```makefile
.PHONY: clean

clean:
	rm -f app *.o
说明:
.PHONY 表示 clean 是伪目标
clean 不是要生成的文件，而是一个动作名字

写了 .PHONY 后，即使当前目录下有 clean 这个文件，
make clean 也会正常执行清理命令
```

## 4.10 常用 Makefile 模板

```makefile
CC = gcc
TARGET = app
OBJS = main.o add.o
CFLAGS = -Wall -g

$(TARGET): $(OBJS)
	$(CC) $^ -o $@

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

.PHONY: clean

clean:
	rm -f $(TARGET) $(OBJS)
说明:
$(TARGET): $(OBJS)
表示 app 依赖 main.o add.o

$(CC) $^ -o $@
等价于 gcc main.o add.o -o app

%.o: %.c
表示 .c 文件可以生成对应的 .o 文件

clean:
清理生成文件
```

## 4.11 ARM 交叉编译 Makefile

```makefile
CC = arm-linux-gcc
TARGET = app
OBJS = main.o add.o
CFLAGS = -Wall -g

$(TARGET): $(OBJS)
	$(CC) $^ -o $@

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

.PHONY: clean

clean:
	rm -f $(TARGET) $(OBJS)
说明:
如果程序要放到 ARM 开发板上运行，需要把 gcc 换成 ARM 交叉编译器

具体使用哪个交叉编译器，要看开发板提供的工具链名字
```

# 5 文件 IO

## 5.1 文件 IO 基本概念

Linux 中常见文件操作接口分为两类：

| 类型         | 使用对象          | 特点                             |
| ------------ | ----------------- | -------------------------------- |
| 系统调用接口 | 文件描述符 `fd`   | 直接调用内核接口，常用于底层开发 |
| 标准 IO 接口 | 文件指针 `FILE *` | C 库封装，带缓冲，使用更方便     |

```bash
简单记忆:

系统调用接口:
open / read / write / lseek / fsync / close
操作 fd

标准 IO 接口:
fopen / fread / fwrite / fseek / fflush / fclose
操作 FILE *
```

### 5.1.1 文件描述符 fd

```bash
fd:
file descriptor，文件描述符
本质上是一个整数，用来表示一个已经打开的文件
```

常见文件描述符：

| fd   | 含义            |
| ---- | --------------- |
| `0`  | 标准输入 stdin  |
| `1`  | 标准输出 stdout |
| `2`  | 标准错误 stderr |

------

## 5.2 系统调用接口

系统调用接口操作的是 **文件描述符 fd**。

```bash
系统调用接口常用函数:
open / read / write / dup / dup2 / dup3 / lseek / fsync / close
```

------

### open

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int open(const char *pathname, int flags);
int open(const char *pathname, int flags, mode_t mode);
作用:
打开或创建一个文件

参数:
pathname:文件路径，或者文件名

flags:表示打开文件时采用的操作方式

mode:创建文件时的权限,只有 flags 中使用 O_CREAT 时，mode 参数才需要写

返回值:
成功 返回文件描述符 fd
失败 返回 -1
常用 flags:

O_RDONLY:只读方式打开

O_WRONLY:只写方式打开

O_RDWR:读写方式打开

O_APPEND:追加写入,如果原来文件里有内容，这次写入会写在文件末尾

O_CREAT:如果文件不存在，则创建这个文件,使用 O_CREAT 时，open 通常需要第三个参数 mode；如果文件已存在则不会改变它的权限

O_EXCL:一般和 O_CREAT 一起使用,如果文件已经存在，则 open 失败并返回 -1,常用来防止覆盖已有文件

O_TRUNC:如果文件已经存在，并且以写方式打开,则把文件原来的内容清空，文件长度变为 0

O_NOCTTY:如果 pathname 指向终端设备,不把这个设备作为进程的控制终端

O_NONBLOCK:非阻塞方式打开文件或设备,常用于 FIFO、设备文件、串口等

O_DSYNC:等待数据写入完成,但不一定等待文件属性更新完成

O_SYNC:等待数据和文件属性都写入完成

O_RSYNC:读操作也要等待相关写操作完成
    
int fd;
fd = open("test.txt", O_RDWR | O_CREAT | O_TRUNC, 0644);
说明:
O_RDWR:以读写方式打开

O_CREAT:文件不存在则创建

O_TRUNC:文件存在则清空原内容

0644:
创建文件时的权限
```

```bash
mode:
创建文件时的权限
只有使用 O_CREAT 创建文件时才需要
```

| 权限数字 | 含义            |
| -------- | --------------- |
| 4        | read，可读      |
| 2        | write，可写     |
| 1        | execute，可执行 |

```bash
常用 mode:

0644:
文件所有者可读可写
同组用户只读
其他用户只读

0666:
所有用户可读可写

0755:
文件所有者可读可写可执行
同组用户可读可执行
其他用户可读可执行
注意:
0644 前面的 0 表示八进制
不要写成 644
```

------

### read

```c
#include <unistd.h>

ssize_t read(int fd, void *buf, size_t count);
作用:从文件中读取数据

参数:
fd:文件描述符

buf:缓冲区，用来保存读取到的数据

count:最多读取的字节数

返回值:
> 0  实际读取到的字节数
= 0  读到文件末尾
-1   读取失败
    
char buf[100];
int ret;
ret = read(fd, buf, sizeof(buf));
说明:
read 不一定每次都能读到 count 个字节
实际读到多少，要看返回值 ret
```

------

### write

```c
#include <unistd.h>

ssize_t write(int fd, const void *buf, size_t count);
作用:向文件中写入数据

参数:
fd:文件描述符

buf:要写入的数据

count:要写入的字节数

返回值:
>= 0 实际写入的字节数
-1   写入失败

write(fd, "hello\n", 6);
说明:
write 的返回值表示实际写入了多少字节
实际写入字节数可能小于 count
所以严谨写法需要检查返回值
```

------

### dup / dup2 / dup3

```c
#include <unistd.h>

int dup(int oldfd);
int dup2(int oldfd, int newfd);
#define _GNU_SOURCE
#include <fcntl.h>
#include <unistd.h>

int dup3(int oldfd, int newfd, int flags);
作用:
复制文件描述符

oldfd:
被复制的旧文件描述符

newfd:
指定新的文件描述符

flags:
dup3 的额外标志，常用 O_CLOEXEC

返回值:
成功 返回新的文件描述符
失败 返回 -1
说明:
dup:
复制 oldfd，系统自动分配一个新的 fd

dup2:
把 oldfd 复制到指定的 newfd
如果 newfd 已经打开，会先关闭 newfd

dup3:
类似 dup2
但可以设置 flags，例如 O_CLOEXEC
常见用途:
重定向标准输入
重定向标准输出
重定向标准错误
dup2(fd, 1);
说明:
把标准输出 stdout 重定向到 fd 对应的文件
后面 printf 的内容可能会写入文件
```

------

### lseek

```c
#include <sys/types.h>
#include <unistd.h>

off_t lseek(int fd, off_t offset, int whence);
作用:
移动文件的读写位置

参数:
fd:
文件描述符

offset:
偏移量

whence:
偏移参考位置

返回值:
成功 返回新的文件位置
失败 返回 -1
whence 常用取值:

SEEK_SET:
从文件开头开始偏移

SEEK_CUR:
从当前位置开始偏移

SEEK_END:
从文件末尾开始偏移
lseek(fd, 0, SEEK_SET);
说明:
把文件位置移动到文件开头
lseek(fd, 0, SEEK_END);
说明:
把文件位置移动到文件末尾
lseek(fd, 10, SEEK_SET);
说明:
把文件位置移动到距离文件开头 10 字节的位置
```

------

### fsync

```c
#include <unistd.h>

int fsync(int fd);
作用:
把文件数据同步到存储设备

参数:
fd:
文件描述符

返回值:
成功 返回 0
失败 返回 -1
说明:
write 写文件时，数据可能先放在内存缓冲区中
fsync 可以尽量把数据真正同步到磁盘、Flash、SD 卡等设备中

常见使用场景:
写完重要文件后
断电前
重启开发板前
```

------

### close

```c
#include <unistd.h>

int close(int fd);
作用:
关闭已经打开的文件

参数:
fd:
文件描述符

返回值:
成功 返回 0
失败 返回 -1
说明:
open 打开文件后，使用完成要 close
否则可能造成文件描述符泄漏
```

------

### 系统调用接口示例

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

int main(void)
{
    int fd;
    char buf[100];

    fd = open("test.txt", O_RDWR | O_CREAT | O_TRUNC, 0644);
    if (fd < 0)
        return -1;

    write(fd, "hello\n", 6);

    lseek(fd, 0, SEEK_SET);

    read(fd, buf, sizeof(buf));

    fsync(fd);

    close(fd);

    return 0;
}
说明:
open:
打开或创建文件

write:
写入数据

lseek:
移动文件位置

read:
读取数据

fsync:
同步数据到存储设备

close:
关闭文件
```

------

## 5.3 标准 IO 接口

标准 IO 接口操作的是 **文件指针 FILE \***。

```bash
标准 IO 接口常用函数:
fopen / fread / fwrite / fseek / fflush / fclose
```

------

### fopen

```c
#include <stdio.h>

FILE *fopen(const char *filename, const char *mode);
作用:
打开文件

参数:
filename:
文件路径，或者文件名

mode:
打开方式

返回值:
成功 返回 FILE *
失败 返回 NULL
常用 mode:

"r":
只读方式打开文件
文件必须存在

"r+":
读写方式打开文件
文件必须存在

"w":
只写方式打开文件
如果文件不存在，则创建
如果文件已经存在，则清空原内容

"w+":
读写方式打开文件
如果文件不存在，则创建
如果文件已经存在，则清空原内容

"a":
追加写方式打开文件
如果文件不存在，则创建
写入内容会追加到文件末尾

"a+":
读和追加写方式打开文件
如果文件不存在，则创建
写入内容会追加到文件末尾
简单记忆:
r : read，读
w : write，写，会清空原文件
a : append，追加写
+ : 读写
FILE *fp;

fp = fopen("test.txt", "w+");
说明:
以读写方式打开 test.txt
如果文件不存在则创建
如果文件存在则清空原内容
```

------

### fread

```c
#include <stdio.h>

size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
作用:
从文件中读取数据

参数:
ptr:
保存读取数据的缓冲区

size:
每个数据块的大小，单位是字节

nmemb:
要读取多少个数据块

stream:
FILE 文件指针

返回值:
成功读取的数据块个数
char buf[100];
size_t ret;

ret = fread(buf, 1, sizeof(buf), fp);
说明:
size = 1
nmemb = sizeof(buf)

表示最多读取 sizeof(buf) 个字节

注意:
fread 返回值不是字节数本身
而是成功读取的数据块个数

当 size 为 1 时，返回值才可以直接理解为读取到的字节数
```

------

### fwrite

```c
#include <stdio.h>

size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
作用:
向文件中写入数据

参数:
ptr:
要写入的数据

size:
每个数据块的大小，单位是字节

nmemb:
要写入多少个数据块

stream:
FILE 文件指针

返回值:
成功写入的数据块个数
fwrite("hello\n", 1, 6, fp);
说明:
把 6 个字节写入文件

注意:
fwrite 返回值表示成功写入的数据块个数
如果返回值小于 nmemb，说明没有全部写入
```

------

### fseek

```c
#include <stdio.h>

int fseek(FILE *stream, long int offset, int whence);
作用:
移动文件读写位置

参数:
stream:
FILE 文件指针

offset:
偏移量

whence:
偏移参考位置

返回值:
成功 返回 0
失败 返回非 0
whence 常用取值:

SEEK_SET:
从文件开头开始偏移

SEEK_CUR:
从当前位置开始偏移

SEEK_END:
从文件末尾开始偏移
fseek(fp, 0, SEEK_SET);
说明:
把文件位置移动到文件开头
```

------

### fflush

```c
#include <stdio.h>

int fflush(FILE *stream);
作用:
刷新标准 IO 缓冲区

参数:
stream:
FILE 文件指针

返回值:
成功 返回 0
失败 返回 EOF
说明:
标准 IO 是带缓冲的
fwrite 或 fprintf 写入的数据，可能先留在 C 库缓冲区中
fflush 可以把缓冲区中的数据刷新出去
注意:
fflush 只是刷新 C 库缓冲区
不等于 fsync

如果要求尽量写入存储设备，需要考虑 fsync
```

------

### fclose

```c
#include <stdio.h>

int fclose(FILE *stream);
作用:
关闭文件

参数:
stream:
FILE 文件指针

返回值:
成功 返回 0
失败 返回 EOF
说明:
fclose 会先刷新缓冲区
然后关闭文件

fopen 打开文件后，使用完成要 fclose
```

------

### 标准 IO 接口示例

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char buf[100];

    fp = fopen("test.txt", "w+");
    if (fp == NULL)
        return -1;

    fwrite("hello\n", 1, 6, fp);

    fflush(fp);

    fseek(fp, 0, SEEK_SET);

    fread(buf, 1, sizeof(buf), fp);

    fclose(fp);

    return 0;
}
说明:
fopen:
打开文件

fwrite:
写入数据

fflush:
刷新缓冲区

fseek:
移动文件位置

fread:
读取数据

fclose:
关闭文件
```

### 其他函数

```c
char *fgets(char *s, int size, FILE *stream);
int fputs(const char *s, FILE *stream);
int fprintf(FILE *stream, const char *format, ...);
int fscanf(FILE *stream, const char *format, ...);
int feof(FILE *stream);
int ferror(FILE *stream);
fgets:
读取一行

fputs:
写字符串

fprintf:
格式化写入

fscanf:
格式化读取

feof:
判断文件结束

ferror:
判断错误
```

------

## 5.4 系统调用接口 vs 标准 IO

| 对比项     | 系统调用        | 标准 IO            |
| ---------- | --------------- | ------------------ |
| 操作对象   | fd              | FILE *             |
| 是否带缓冲 | 否              | 是                 |
| 常用函数   | open/read/write | fopen/fread/fwrite |
| 同步       | fsync           | fflush             |
| 使用场景   | 底层开发        | 应用开发           |

```bash
重点区别:

系统调用:
直接操作内核，效率高

标准IO:
带缓冲，更方便
```

------

## 5.5 常见错误处理

### 5.5.1 errno、perror、strerror

```
#include <errno.h>
#include <stdio.h>
#include <string.h>
errno:
保存最近一次系统调用或库函数出错的错误码

perror:
打印错误原因

strerror:
把错误码转换成错误字符串
perror("open");
说明:
perror 会打印传入的字符串 + 具体错误原因

例如:
open: No such file or directory
printf("error: %s\n", strerror(errno));
说明:
strerror(errno) 可以把 errno 转换成错误描述字符串
```

------

### 5.5.2 常见错误返回值总结

| 函数     | 失败返回值 | 说明                     |
| -------- | ---------- | ------------------------ |
| `open`   | `-1`       | 打开文件失败             |
| `read`   | `-1`       | 读取失败                 |
| `write`  | `-1`       | 写入失败                 |
| `lseek`  | `-1`       | 移动文件位置失败         |
| `fsync`  | `-1`       | 同步失败                 |
| `close`  | `-1`       | 关闭失败                 |
| `fopen`  | `NULL`     | 打开文件失败             |
| `fread`  | 小于期望值 | 可能文件结束，也可能出错 |
| `fwrite` | 小于期望值 | 没有全部写入             |
| `fseek`  | 非 `0`     | 移动文件位置失败         |
| `fflush` | `EOF`      | 刷新失败                 |
| `fclose` | `EOF`      | 关闭失败                 |

### 5.5.3 常见错误原因

| 错误原因          | 说明                             |
| ----------------- | -------------------------------- |
| 文件不存在        | 读模式打开不存在的文件           |
| 权限不足          | 没有读、写、执行权限             |
| 路径错误          | 文件路径写错                     |
| 磁盘空间不足      | 写文件失败                       |
| fd 无效           | 文件描述符已经关闭或没有正确打开 |
| FILE 指针无效     | `fopen` 失败后继续使用 `fp`      |
| 忘记 close/fclose | 文件没有正常关闭                 |
| 忘记判断返回值    | 函数失败后程序继续执行，容易出错 |

# 6 开发板操作命令

## 亮屏/息屏

| 命令 | 选项 | 参数             |
| ---- | ---- | ---------------- |
| echo | \    | [0/1] [文件路径] |

```bash
echo 0 > /sys/class/graphics/fb0/blank        亮屏
echo 1 > /sys/class/graphics/fb0/blank        息屏
说明:
echo : 向指定文件写入内容
> : 重定向，把前面的内容写入到后面的文件中

/sys/class/graphics/fb0/blank:
这是Linux系统中控制屏幕亮灭的文件

0 : 亮屏
1 : 息屏

注意:
这个命令一般是在开发板上执行，不是在虚拟机上执行
如果当前是通过adb shell进入开发板，也可以执行这个命令
```

## 查看设备节点对应的硬件  

```
cat /proc/bus/input/devices
```

##  LVGL 图形界面 停止/启动

```sh
/etc/init.d/S05lvgl stop     # 停止 LVGL 图形界面程序
/etc/init.d/S05lvgl start    # 启动 LVGL 图形界面程序

说明：
/etc/init.d/S05lvgl：
LVGL 图形界面程序的 SysV init 启动脚本。

stop：
调用脚本中的 stop() 函数，停止 lvgl_100ask_demo 程序。

start：
调用脚本中的 start() 函数，启动 lvgl_100ask_demo 程序。


在运行触摸屏测试程序前，先停止 LVGL：
/etc/init.d/S05lvgl stop
ts_test_mt

测试结束后，重新启动 LVGL 图形界面：
/etc/init.d/S05lvgl start

注意：
这些命令需要在开发板中执行。
当前开发板没有使用 systemd，因此不能使用：
systemctl stop myir
当前开发板使用 /etc/init.d/ 下的 SysV init 启动脚本管理程序。
```

## sync : 同步数据到存储设备

| 命令 | 选项 | 参数 |
| ---- | ---- | ---- |
| sync | \    | \    |

```bash
作用:
把内存中还没有写入存储设备的数据，立即同步到Flash、SD卡等存储设备中

example:
sync
说明:
Linux为了提高速度，很多文件操作会先放在内存中
执行sync后，可以减少突然断电导致文件丢失或损坏的风险

常见使用场景:
1. 修改文件后，准备重启开发板
2. 拷贝文件到开发板后，准备断电
3. 修改系统配置后，准备reboot
```

## reboot : 重启开发板

| 命令   | 选项 | 参数 |
| ------ | ---- | ---- |
| reboot | \    | \    |

```bash
作用:
重启Linux系统

example:
reboot
说明:
在开发板上执行reboot后，开发板会重新启动
如果刚刚修改过文件，建议先执行sync，再执行reboot

常用操作:
sync
reboot
```

## poweroff : 关闭开发板系统

| 命令     | 选项 | 参数 |
| -------- | ---- | ---- |
| poweroff | \    | \    |

```bash
作用:
关闭Linux系统

example:
poweroff
说明:
poweroff会让系统进入关机状态
有些开发板执行poweroff后，电源灯可能仍然亮着，这是因为板子还接着电源
如果要完全断电，需要拔掉电源线或关闭电源开关

建议:
关机前先执行sync

常用操作:
sync
poweroff
```

## dmesg : 查看内核打印信息

| 命令  | 选项 | 参数 |
| ----- | ---- | ---- |
| dmesg | \    | \    |

```bash
作用:
查看Linux内核启动和运行过程中的打印信息

example:
dmesg
dmesg | grep fb
dmesg | grep input
说明:
dmesg常用于查看硬件驱动相关信息
比如屏幕、触摸屏、USB、网卡等设备有没有被内核识别到

| : 管道，把前一个命令的输出交给后一个命令处理
grep : 搜索指定内容
```

## ifconfig : 查看开发板网络信息

| 命令     | 选项 | 参数 |
| -------- | ---- | ---- |
| ifconfig | \    | \    |

```bash
作用:
查看开发板的网卡和IP地址信息

example:
ifconfig
ifconfig eth0
说明:
eth0 : 通常表示有线网卡
lo : 本地回环网卡，不是外部网络
wlan0 : 通常表示无线网卡

常见使用场景:
1. 查看开发板IP地址
2. 判断网卡是否启动
3. 配合adb connect、ssh、nfs等网络操作使用
```

## ps : 查看正在运行的进程

| 命令 | 选项 | 参数 |
| ---- | ---- | ---- |
| ps   | \    | \    |

```bash
作用:
查看当前系统中正在运行的程序

example:
ps
ps | grep adbd
说明:
进程就是正在运行的程序
比如adbd、shell、应用程序等都可以看作进程

常见使用场景:
查看某个服务是否正在运行

example:
ps | grep adbd
```

## kill : 结束进程

| 命令 | 选项 | 参数     |
| ---- | ---- | -------- |
| kill | \    | [进程号] |

```bash
作用:
结束指定的进程

example:
kill 1234
kill -9 1234
说明:
1234 : 进程号，也叫PID
-9 : 强制结束进程

注意:
kill命令要谨慎使用
不要随便结束不认识的系统进程，否则可能导致开发板运行异常
```
# 7 Linux 应用开发

## 7.1 文件与设备控制

### 7.1.1 宏

#### fcntl相关（F_*）

##### 概括
```c
#include <fcntl.h>

#define F_DUPFD          0    /* 复制文件描述符 */
#define F_GETFD          1    /* 获取文件描述符标志 */
#define F_SETFD          2    /* 设置文件描述符标志 */
#define F_GETFL          3    /* 获取文件状态标志 */
#define F_SETFL          4    /* 设置文件状态标志 */

#define F_GETLK          5    /* 查询是否存在冲突的文件记录锁 */
#define F_SETLK          6    /* 非阻塞地设置或解除文件记录锁 */
#define F_SETLKW         7    /* 阻塞地设置或解除文件记录锁 */

#define F_SETOWN         8    /* 设置异步 I/O 信号的接收者 */
#define F_GETOWN         9    /* 获取异步 I/O 信号的接收者 */

#define F_SETSIG         10   /* 设置异步 I/O 通知使用的信号 */
#define F_GETSIG         11   /* 获取异步 I/O 通知使用的信号 */

#define F_GETLK64        12   /* 使用 struct flock64 查询文件记录锁 */
#define F_SETLK64        13   /* 使用 struct flock64 非阻塞地设置或解除文件记录锁 */
#define F_SETLKW64       14   /* 使用 struct flock64 阻塞地设置或解除文件记录锁 */

#define F_SETOWN_EX      15   /* 使用 struct f_owner_ex 设置异步 I/O 信号接收者 */
#define F_GETOWN_EX      16   /* 使用 struct f_owner_ex 获取异步 I/O 信号接收者 */

#define F_GETOWNER_UIDS  17   /* 获取异步 I/O 信号接收者相关的用户 ID */

#define F_OFD_GETLK      36   /* 查询是否存在冲突的打开文件描述锁 */
#define F_OFD_SETLK      37   /* 非阻塞地设置或解除打开文件描述锁 */
#define F_OFD_SETLKW     38   /* 阻塞地设置或解除打开文件描述锁 */
```

##### F_SETOWN

```c
/**
 * @brief  设置文件描述符异步 I/O 信号的接收者。
 *
 * @param  fd: 需要设置的文件描述符。
 *
 * @param  owner: 接收异步通知信号的进程或进程组。
 *                正数表示进程 ID；
 *                负数表示进程组 ID。
 *
 * @retval 0: 设置成功。
 *
 * @retval -1: 设置失败，并设置 errno。
 *
 * @note   F_SETOWN 是 fcntl() 的命令宏，不是函数。
 * @note   还需要通过 F_SETFL 设置 FASYNC，
 *         才能真正开启异步通知。
 */
#include <fcntl.h>

fcntl(fd, F_SETOWN, owner);
```

代码示例：

```c
fcntl(fd, F_SETOWN, getpid());

/*
 * 将当前进程设置为 fd 的异步通知信号接收者。
 *
 * 当 fd 产生异步 I/O 事件时，
 * 内核会把信号发送给当前进程。
 */
```

##### F_GETFL

```c
/**
 * @brief  获取文件描述符当前的文件状态标志。
 *
 * @param  fd: 需要获取状态标志的文件描述符。
 *
 * @retval 成功: 返回文件描述符当前的文件状态标志。
 *
 * @retval -1: 获取失败，并设置 errno。
 *
 * @note   F_GETFL 是 fcntl() 的命令宏，不是函数。
 * @note   使用 F_GETFL 时不需要第三个参数。
 */
#include <fcntl.h>

fcntl(fd, F_GETFL);
```

代码示例：

```c
int flags;

flags = fcntl(fd, F_GETFL);

/*
 * flags 保存 fd 当前的文件状态标志。
 *
 * 文件状态指的是这个已经打开的文件描述符 fd 当前采用了什么访问方式，
 * 以及启用了哪些文件状态标志
 * example:
 * O_RDONLY      只读方式
 * O_NONBLOCK    非阻塞方式
 *
 * 修改文件状态标志前先获取原有标志，
 * 可以避免原来的状态标志被覆盖。
 */
```

##### F_SETFL

```c
/**
 * @brief  设置文件描述符的文件状态标志。
 *
 * @param  fd: 需要设置状态标志的文件描述符。
 *
 * @param  flags: 需要设置的文件状态标志。
 *
 * @retval 0: 设置成功。
 *
 * @retval -1: 设置失败，并设置 errno。
 *
 * @note   F_SETFL 是 fcntl() 的命令宏，不是函数。
 */
#include <fcntl.h>

fcntl(fd, F_SETFL, flags);
```

代码示例：

```c
fcntl(fd, F_SETFL, flags | FASYNC);

/*
 * 保留 flags 中原来的文件状态标志，
 * 并为 fd 开启异步 I/O 信号通知。
 */

FASYNC
/**
 * @brief  开启文件描述符的异步 I/O 信号通知。
 *
 * @note   FASYNC 是文件状态标志，不是 fcntl() 的命令宏。
 * @note   FASYNC 需要配合 F_SETFL 使用。
 * @note   当 fd 产生异步 I/O 事件时，内核会向
 *         F_SETOWN 指定的进程发送 SIGIO。
 */
#include <fcntl.h>

#define FASYNC 00020000
```

### 7.1.2 函数
#### ioctl : 设备控制函数

```c
/**
 * @brief  向设备驱动发送控制命令，用于控制设备或获取设备状态。
 *
 * @param  fd：文件描述符。
 *         该参数由 open 函数打开设备文件后获得。
 *
 * @param  request：控制命令。
 *         该参数用于告诉驱动程序要执行什么操作。
 *
 *         @arg	framebuffer 中常用 request 可以是以下值：
 *				 FBIOGET_VSCREENINFO
 *               获取屏幕可变参数信息。
 *               第三个参数应传入 struct fb_var_screeninfo 结构体地址
 *
 * @param  ...：可变参数。
 *         该参数是否需要传入，由 request 决定。
 *         如果 request 需要向驱动传递数据，或需要从驱动获取数据，
 *         则该参数通常传入对应变量或结构体的地址。
 *		   example:
 *			static struct fb_var_screeninfo var;
 *			ioctl(fd_fb, FBIOGET_VSCREENINFO, &var)
 *
 * @retval 非负数: 调用成功。 
 * 				具体返回值由 request 决定； 
 * 				某些命令成功时返回 0， 
 * 				某些命令成功时返回数据长度或其他非负结果。 
 * 
 * @retval -1: 调用失败，并设置 errno。
 */
#include <sys/ioctl.h>
int ioctl(int fd, unsigned long request, ...);

example:
static struct fb_var_screeninfo var;
ioctl(fd_fb, FBIOGET_VSCREENINFO, &var)
```

#### fcntl：文件描述符控制函数

```c
/**
 * @brief  对已经打开的文件描述符进行控制操作，
 *         如获取或修改文件状态标志、设置异步通知接收者等。
 *
 * @param  fd: 需要控制的文件描述符。
 *
 * @param  cmd: 要执行的控制命令，如 F_GETFL、F_SETFL、F_SETOWN。
 *
 * @param  ...: 可选的第三个参数，其类型和含义由 cmd 决定。
 *
 * @retval 成功: 返回值由 cmd 决定。
 *
 * @retval -1: 调用失败，并设置 errno。
 */
#include <fcntl.h>

int fcntl(int fd, int cmd, ...);
```

代码示例：

```c
int flags;
int ret;

flags = fcntl(fd, F_GETFL);

/*
 * F_GETFL：
 * 获取 fd 当前的文件状态标志。
 *
 * 成功时返回文件状态标志；
 * 失败时返回 -1。
 */

ret = fcntl(fd, F_SETFL, flags | O_NONBLOCK | O_ASYNC);

/*
 * F_SETFL：
 * 修改 fd 的文件状态标志。
 *
 * O_NONBLOCK：
 * 将文件描述符设置为非阻塞方式。
 *
 * O_ASYNC：
 * 开启异步 I/O 信号通知。
 *
 * 成功时返回 0；
 * 失败时返回 -1。
 */
```

#### fstat：获取文件属性信息函数

```c
/**
 * @brief  通过文件描述符获取文件属性信息。
 *
 * @param  fd：文件描述符。
 *         该参数由 open 函数打开文件或设备文件后获得。
 *
 * @param  statbuf：保存文件属性信息的结构体地址。
 *         函数调用成功后，文件大小、权限、类型等信息会被保存到该结构体中。
 *
 *         常用成员：
 *
 *         @arg st_size
 *              文件大小，单位是字节。
 *
 *         @arg st_mode
 *              文件类型和权限信息。
 *
 *         @arg st_mtime
 *              文件最后修改时间。
 *
 *         @arg st_uid
 *              文件所有者用户 ID。
 *
 *         @arg st_gid
 *              文件所属用户组 ID。
 *
 * @retval 0 ：函数调用成功。
 * @retval -1：函数调用失败。
 */
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

int fstat(int fd, struct stat *statbuf);
```

## 7.2 多文件同时监视(I/O 多路复用)

### 7.2.1 宏
#### fd_set相关

##### FD_ZERO：清空集合

```c
/**
 * @brief  清空 fd_set 文件描述符集合，
 *         使集合中不包含任何文件描述符。
 *
 * @param  set: 指向需要清空的 fd_set 集合。
 *
 * @retval 无返回值。
 *
 * @note   FD_ZERO 是宏，不是函数。
 */
#include <sys/select.h>

FD_ZERO(fd_set *set);
```

代码示例：

```c
fd_set readfds;

FD_ZERO(&readfds);

/*
 * 清空 readfds 集合。
 *
 * 使用 FD_SET() 添加文件描述符之前，
 * 通常需要先调用 FD_ZERO() 清空集合。
 */
```

##### FD_SET：将fd加入集合

```c
/**
 * @brief  将指定文件描述符加入 fd_set 集合。
 *
 * @param  fd: 需要加入集合的文件描述符。
 *
 * @param  set: 指向目标 fd_set 集合。
 *
 * @retval 无返回值。
 *
 * @note   FD_SET 是宏，不是函数。
 */
#include <sys/select.h>

FD_SET(int fd, fd_set *set);
```

代码示例：

```c
fd_set readfds;

FD_ZERO(&readfds);
FD_SET(fd, &readfds);

/*
 * 将 fd 加入 readfds 集合。
 *
 * readfds 传给 select() 后，
 * 可以用于监视 fd 是否变为可读。
 */
```

##### FD_ISSET：判断是否在集合

```c
/**
 * @brief  判断指定文件描述符是否存在于 fd_set 集合中。
 *
 * @param  fd: 需要判断的文件描述符。
 *
 * @param  set: 指向需要检查的 fd_set 集合。
 *
 * @retval 非 0: fd 存在于集合中。
 *
 * @retval 0: fd 不存在于集合中。
 *
 * @note   FD_ISSET 是宏，不是函数。
 */
#include <sys/select.h>

FD_ISSET(int fd, fd_set *set);
```

代码示例：

```c
if (FD_ISSET(fd, &readfds))
{
    /*
     * fd 存在于 readfds 集合中。
     *
     * 当 readfds 经过 select() 处理后，
     * 这里表示 fd 已经处于可读状态。
     */
}
```

### 7.2.2 数据类型

#### fd_set

```c
/**
 * @brief  保存文件描述符集合，供 select() 指定需要监视的文件描述符，
 *         并接收 select() 返回的就绪文件描述符。
 *
 *         fd_set 的内部结构由系统实现决定，
 *         应使用 FD_ZERO()、FD_SET()、FD_CLR() 和 FD_ISSET() 操作。
 */
#include <sys/select.h>

fd_set set;
```

代码示例：

```c
fd_set readfds;

FD_ZERO(&readfds);
FD_SET(fd, &readfds);

/*
 * FD_ZERO()：
 * 清空 readfds 文件描述符集合。
 *
 * FD_SET()：
 * 将 fd 加入 readfds 集合。
 *
 * readfds 可以传给 select()，
 * 表示监视 fd 是否变为可读。
 *
 * select() 返回后：
 * FD_ISSET(fd, &readfds) 非 0，
 * 表示 fd 已经可以读取。
 *
 * FD_CLR(fd, &readfds)：
 * 可以将 fd 从集合中移除。
 */
```

#### struct pollfd

```c
/**
 * @brief  描述 poll() 需要监视的文件描述符及其事件。
 *
 * @member fd: 需要监视的文件描述符。
 *             fd 小于 0 时，poll() 会忽略该元素。
 *
 * @member events: 希望监视的事件。
 *                 常用值为 POLLIN、POLLOUT 等，
 *                 多个事件可以使用按位或运算组合。
 *
 * @member revents: poll() 返回时实际发生的事件。
 *                  调用前通常设置为 0。
 */
#include <poll.h>

struct pollfd {
    int   fd;
    short events;
    short revents;
};
```

代码示例：

```c
struct pollfd pfd;

pfd.fd = fd;
pfd.events = POLLIN;
pfd.revents = 0;

/*
 * fd：
 * 需要监视的文件描述符。
 *
 * POLLIN：
 * 表示等待文件中出现可读取的数据。
 *
 * revents：
 * poll() 返回后保存实际发生的事件。
 *
 * 判断结果：
 * if (pfd.revents & POLLIN)
 * 表示该文件描述符当前可以读取数据。
 */
```

#### struct timeval

```c
/**
 * @brief  保存由秒和微秒组成的时间值，可用于表示时间点或时间间隔。
 *
 * @member tv_sec: 秒数。
 *
 * @member tv_usec: 不足一秒的微秒数，通常取值范围为 0～999999。
 */
#include <sys/time.h>

struct timeval {
    time_t      tv_sec;
    suseconds_t tv_usec;
};
```

代码示例：

```c
struct timeval timeout;

timeout.tv_sec = 5;
timeout.tv_usec = 500000;

/*
 * timeout.tv_sec：
 * 表示 5 秒。
 *
 * timeout.tv_usec：
 * 表示 500000 微秒，即 0.5 秒。
 *
 * timeout 表示的总时间：
 * 5.5 秒。
 */
```

### 7.2.3 函数

#### poll： 监视文件

```c
/**
 * @brief  监视一个或多个文件描述符，等待指定事件发生。
 *		   没有数据时休眠；硬件产生数据或超时后，驱动唤醒应用
 *		   休眠指的是当前线程暂时不运行，CPU 可以去执行其他程序
 *
 * @param  fds: 指向 struct pollfd 数组。
 *              数组中的每个元素用于指定一个文件描述符、
 *              需要监视的事件以及实际发生的事件。
 *
 * @param  nfds: fds 数组中的元素个数。
 *
 * @param  timeout: 等待超时时间，单位为毫秒。
 *                  大于 0 表示最多等待指定时间；
 *                  等于 0 表示立即返回；
 *                  等于 -1 表示一直等待，直到有事件发生。
 *
 * @retval 正数: 已发生事件的文件描述符数量。
 *
 * @retval 0: 等待超时，没有事件发生。
 *
 * @retval -1: 调用失败，并设置 errno。
 */
#include <poll.h>

int poll(struct pollfd *fds, nfds_t nfds, int timeout);
```

代码示例：

```c
struct pollfd fds[1];
int ret;

fds[0].fd = fd;
fds[0].events = POLLIN;
fds[0].revents = 0;

ret = poll(fds, 1, 1000);

/*
 * fds：
 * 监视 fd 对应的文件。
 *
 * POLLIN：
 * 等待文件中出现可读取的数据。
 *
 * 1：
 * 表示 fds 数组中有 1 个元素。
 *
 * 1000：
 * 最多等待 1000 毫秒。
 *
 * ret > 0：
 * 有文件描述符发生了事件，
 * 可以通过 fds[0].revents 判断实际发生的事件。
 *
 * ret == 0：
 * 等待超时，没有事件发生。
 *
 * ret == -1：
 * 调用失败，并设置 errno。
 */
```

#### select：监视文件

```c
/**
 * @brief  等待一个或多个文件描述符变为可读、可写或发生异常。
 *
 * @param  nfds: 所有被监视文件描述符中的最大值加 1，注意：不是文件个数。
 *
 * @param  readfds: 指向可读文件描述符集合。
 *                  不监视可读事件时传入 NULL。
 *
 * @param  writefds: 指向可写文件描述符集合。
 *                   不监视可写事件时传入 NULL。
 *
 * @param  exceptfds: 指向异常文件描述符集合。
 *                    不监视异常事件时传入 NULL。
 *
 * @param  timeout: 指向超时时间。
 *                  传入 NULL 表示一直等待；
 *                  时间为 0 表示立即返回。
 *
 * @retval 正数: 已准备好的文件描述符数量。
 *
 * @retval 0: 等待超时，没有文件描述符准备好。
 *
 * @retval -1: 调用失败，并设置 errno。
 */
#include <sys/select.h>

int select(int nfds,
           fd_set *readfds,
           fd_set *writefds,
           fd_set *exceptfds,
           struct timeval *timeout);

注意：这4个指针参数每次调用 select() 前都要重新设置；select() 返回后会修改 它们的值。
```

代码示例：

```c
fd_set readfds;
struct timeval timeout;
int ret;

FD_ZERO(&readfds);
FD_SET(fd, &readfds);

timeout.tv_sec = 5;
timeout.tv_usec = 0;

ret = select(fd + 1, &readfds, NULL, NULL, &timeout);
/*
 * fd + 1：
 * 被监视的最大文件描述符加 1。
 *
 * &readfds：
 * 等待 fd 变为可读。
 *
 * NULL：
 * 不监视可写事件和异常事件。
 *
 * &timeout：
 * 最多等待 5 秒。
 *
 * ret > 0：
 * 有文件描述符已经准备好；
 * 可以使用 FD_ISSET(fd, &readfds) 判断 fd 是否可读。
 *
 * ret == 0：
 * 等待超时。
 *
 * ret == -1：
 * 调用失败，并设置 errno。
 */

/*
 * FD_ZERO()：
 * 清空 readfds 文件描述符集合。
 *
 * FD_SET()：
 * 将 fd 加入 readfds 集合。
 */
```

## 7.3 输入系统

### 7.3.1 宏
#### 输入事件类型宏（EV_*）

`EV_*` 宏用于表示 Linux 输入事件的类型。

使用：
```c
EVIOCGBIT(0, len)
```

查询输入设备支持的事件类型时，返回位图中的**位编号**与 `EV_*` 宏的数值相对应：

```c
#include <linux/input-event-codes.h>
    
#define EV_SYN          0x00    /* 同步事件 */
#define EV_KEY          0x01    /* 按键、按钮事件 */
#define EV_REL          0x02    /* 相对位移事件，如鼠标移动 */
#define EV_ABS          0x03    /* 绝对位置事件，如触摸屏坐标 */
#define EV_MSC          0x04    /* 其他杂项事件 */
#define EV_SW           0x05    /* 开关状态事件 */

#define EV_LED          0x11    /* LED 状态事件 */
#define EV_SND          0x12    /* 声音事件 */
#define EV_REP          0x14    /* 按键自动重复事件 */
#define EV_FF           0x15    /* 力反馈事件 */
#define EV_PWR          0x16    /* 电源事件 */
#define EV_FF_STATUS    0x17    /* 力反馈状态事件 */

#define EV_MAX          0x1f    /* 最大事件类型编号 */
#define EV_CNT          (EV_MAX + 1)
```
#### EVIOCGBIT

```c
/**
 * @brief  生成查询输入设备能力位图的 ioctl 控制命令。
 *
 * @param  ev: 需要查询的事件类型。
 *             传入 0 时，查询设备支持哪些 EV_* 事件类型；
 *             传入 EV_KEY、EV_REL、EV_ABS 等时，
 *             查询该事件类型下支持哪些具体事件。
 *
 * @param  len: 接收查询结果的缓冲区大小，单位为字节。
 *
 * @return 生成的 ioctl request 控制命令。
 */
#include <linux/input.h>

#define EVIOCGBIT(ev, len) \
        _IOC(_IOC_READ, 'E', 0x20 + (ev), (len))
```

代码示例：

```c
//正整数除法向上取整的通用写法：(N + 7) / 8
unsigned char evbit[((EV_MAX + 1) + 7) / 8];
int len;

len = ioctl(fd, EVIOCGBIT(0, sizeof(evbit)), evbit);
len = ioctl(fd, EVIOCGBIT(0, sizeof(evbit)), &evbit);

上面两种写法是一样的，都可以正常运行，但用evbit更规范；
返回的len是读到了数据字节数
evbit    → 数组第一个元素的起始地址
&evbit   → 整个数组的起始地址
/*
 * 0：
 * 查询设备支持哪些 EV_* 事件类型，
 * 例如 EV_KEY、EV_REL、EV_ABS。
 *
 * sizeof(evbit)：
 * 指定最多读取 sizeof(evbit) 字节的数据。
 *
 * evbit：
 * 用于保存设备支持的事件类型位图。
 * 某一位为 1，表示支持该位编号对应的事件类型。
 *
 * len：
 * 大于 0 表示成功读取的字节数；
 * -1 表示 ioctl 调用失败。
 *
 * 查询某类事件下支持的具体事件时，
 * 可以把第一个参数换成对应的事件类型：
 *
 * EVIOCGBIT(EV_KEY, sizeof(keybit))
 * EVIOCGBIT(EV_REL, sizeof(relbit))
 * EVIOCGBIT(EV_ABS, sizeof(absbit))
 */
```
#### EVIOCGABS

`EVIOCGABS(abs)` 用于生成一个 `ioctl` 请求码，用来**获取输入设备某个绝对坐标轴（ABS）的当前值和属性信息**。

常用于查询：

- `ABS_X`：X 轴
    
- `ABS_Y`：Y 轴
    
- `ABS_PRESSURE`：压力
    
- `ABS_MT_POSITION_X`：多点触摸 X 坐标
    
- `ABS_MT_POSITION_Y`：多点触摸 Y 坐标
    
- `ABS_MT_SLOT`：多点触摸槽位范围
    

查询结果保存到 `struct input_absinfo` 中。

```c
/**
 * @brief 生成“获取绝对坐标轴信息”的 ioctl 请求码。
 *
 * @param abs 要查询的绝对坐标轴类型，
 *            例如 ABS_X、ABS_Y、ABS_MT_SLOT。
 *
 * @note EVIOCGABS() 本身不会读取设备，
 *       它只是生成 ioctl() 所需要的 request 参数。
 *
 * 查询结果通常保存到 struct input_absinfo 中：
 *
 * value       当前值
 * minimum     最小值
 * maximum     最大值
 * fuzz        过滤微小抖动时使用的容差值
 * flat        中心死区范围
 * resolution  分辨率
 *
 * 必需头文件：
 * #include <linux/input.h>
 * #include <sys/ioctl.h>
 */

#include <linux/input.h>
#include <sys/ioctl.h>

#define EVIOCGABS(abs) \
        _IOR('E', 0x40 + (abs), struct input_absinfo)

/* 常用形式 */
ioctl(fd, EVIOCGABS(abs), &absinfo);
```

代码示例：

```c
struct input_absinfo slot;

/* 查询多点触摸 ABS_MT_SLOT 的信息 */
if (ioctl(fd, EVIOCGABS(ABS_MT_SLOT), &slot) == 0) {
    /* 根据槽位编号的最小值和最大值计算槽位数量 */
    int max_slots = slot.maximum - slot.minimum + 1;
}
```

这里：

`EVIOCGABS(ABS_MT_SLOT)`  
表示生成“查询 `ABS_MT_SLOT` 信息”的 `ioctl` 命令。

`&slot`  
用于接收内核返回的 `struct input_absinfo` 数据。

例如：

```text
slot.minimum = 0
slot.maximum = 4
```

则触摸槽位数量为：

`4 - 0 + 1 = 5`

因此：

**`EVIOCGABS()` 决定“查询哪个 ABS 轴”，`ioctl()` 负责真正向驱动获取数据，`struct input_absinfo` 负责保存查询结果。**

### 7.3.2 数据类型
#### struct input_id

```c
/**
 * @brief  保存输入设备的身份信息。
 *
 * @member bustype: 设备连接使用的总线类型，
 *                  例如 BUS_USB、BUS_I2C、BUS_HOST。
 *
 * @member vendor: 设备厂商编号。
 *
 * @member product: 设备产品编号。
 *
 * @member version: 当前输入设备的版本编号。
 */
#include <linux/input.h>

struct input_id {
    __u16 bustype;
    __u16 vendor;
    __u16 product;
    __u16 version;
};
```

代码示例：

```c
struct input_id id;

ioctl(fd, EVIOCGID, &id);

/*
 * ioctl() 获取成功后：
 *
 * id.bustype：
 * 保存设备的总线类型。
 *
 * id.vendor：
 * 保存设备的厂商编号。
 *
 * id.product：
 * 保存设备的产品编号。
 *
 * id.version：
 * 保存当前输入设备的版本编号。
 */
```

#### struct input_event

```c
/**
 * @brief  保存输入设备上报的一次标准输入事件。
 *
 * @member time: 事件发生的时间。
 *               tv_sec 保存秒数；
 *               tv_usec 保存微秒数。
 *
 * @member type: 事件类型，
 *               例如 EV_KEY、EV_REL、EV_ABS。
 *
 * @member code: 该事件类型下的具体事件编号，
 *               例如 KEY_A、REL_X、ABS_X。
 *
 * @member value: 事件值。
 *                具体含义由 type 和 code 决定。
 */
#include <linux/input.h>

struct input_event {
    struct timeval time;
    __u16 type;
    __u16 code;
    __s32 value;
};
```

代码示例：

```c
struct input_event event;

read(fd, &event, sizeof(event));

/*
 * read() 读取成功后：
 *
 * event.time：
 * 保存事件发生的时间。
 *
 * event.type：
 * 保存事件所属的大类。
 *
 * event.code：
 * 保存该大类下的具体事件编号。
 *
 * event.value：
 * 保存事件值。
 *
 * 例如按键事件：
 * event.type  = EV_KEY；
 * event.code  = KEY_ENTER；
 * event.value = 0 表示松开；
 * event.value = 1 表示按下；
 * event.value = 2 表示按键自动重复。
 */
```
#### struct input_absinfo

```c
/**
 * @brief 保存输入设备某个绝对坐标轴的当前值和属性信息。
 *        例如可以配合：
 *	          EVIOCGABS(ABS_X)、EVIOCGABS(ABS_Y)、EVIOCGABS(ABS_MT_SLOT) 等宏，
 *			  通过 ioctl() 获取对应绝对轴的信息。
 * value:
 *     当前值。
 *
 * minimum:
 *     该绝对轴能够取到的最小值。
 *
 * maximum:
 *     该绝对轴能够取到的最大值。
 *
 * fuzz:
 *     用于过滤输入数据微小抖动的容差值。
 *
 * flat:
 *     中心无效区域（死区）范围。
 *
 * resolution:
 *     该绝对轴的分辨率。
 *
 * 必需头文件：
 * #include <linux/input.h>
 */

#include <linux/input.h>

struct input_absinfo {
    __s32 value;         /* 当前值 */
    __s32 minimum;       /* 最小值 */
    __s32 maximum;       /* 最大值 */
    __s32 fuzz;          /* 抖动过滤容差 */
    __s32 flat;          /* 死区范围 */
    __s32 resolution;    /* 分辨率 */
};
```

代码示例：

```c
#include <linux/input.h>
#include <sys/ioctl.h>

struct input_absinfo slot;

/* 获取 ABS_MT_SLOT 的范围信息 */
if (ioctl(fd, EVIOCGABS(ABS_MT_SLOT), &slot) == 0) {
    int max_slots = slot.maximum - slot.minimum + 1;
}
```

例如：

```text
slot.minimum = 0
slot.maximum = 4
```

则：

```text
max_slots = 4 - 0 + 1 = 5
```

表示设备支持 `5` 个多点触摸槽位。
## 7.4 信号

### 7.4.1 宏
#### 信号编号宏

`SIG*` 宏用于表示进程接收到的信号类型。

使用：

```c
signal(SIGINT, handler);
```

`signal()` 的 `signum` 参数与下面的信号宏相对应：

```c
#include <signal.h>

/* ISO C99 信号 */

#define SIGINT       2    /* 终端中断，通常由 Ctrl+C 产生 */
#define SIGILL       4    /* 非法指令 */
#define SIGABRT      6    /* 异常终止，通常由 abort() 产生 */
#define SIGFPE       8    /* 算术运算异常 */
#define SIGSEGV      11   /* 非法访问内存 */
#define SIGTERM      15   /* 请求终止进程 */


/* POSIX 历史信号 */

#define SIGHUP       1    /* 终端挂断 */
#define SIGQUIT      3    /* 终端退出，通常由 Ctrl+\ 产生 */
#define SIGTRAP      5    /* 跟踪或断点陷阱 */
#define SIGKILL      9    /* 强制终止进程 */
#define SIGBUS       10   /* 总线错误 */
#define SIGSYS       12   /* 错误的系统调用 */
#define SIGPIPE      13   /* 管道断裂 */
#define SIGALRM      14   /* 定时器到期 */


/* 较新的 POSIX 信号 */

#define SIGURG       16   /* 套接字收到紧急数据 */
#define SIGSTOP      17   /* 强制暂停进程，不能被阻塞 */
#define SIGTSTP      18   /* 终端暂停，通常由 Ctrl+Z 产生 */
#define SIGCONT      19   /* 继续运行暂停的进程 */
#define SIGCHLD      20   /* 子进程终止或暂停 */
#define SIGTTIN      21   /* 后台进程尝试读取控制终端 */
#define SIGTTOU      22   /* 后台进程尝试写入控制终端 */
#define SIGPOLL      23   /* 可轮询事件发生 */
#define SIGXCPU      24   /* 超过 CPU 时间限制 */
#define SIGXFSZ      25   /* 超过文件大小限制 */
#define SIGVTALRM    26   /* 虚拟定时器到期 */
#define SIGPROF      27   /* 性能分析定时器到期 */
#define SIGUSR1      30   /* 用户自定义信号 1 */
#define SIGUSR2      31   /* 用户自定义信号 2 */


/* 现代 POSIX 系统普遍支持的非标准信号 */

#define SIGWINCH     28   /* 终端窗口大小发生改变 */


/* 为兼容旧程序保留的信号别名 */

#define SIGIO        SIGPOLL  /* I/O 操作现在可以进行 */
#define SIGIOT       SIGABRT  /* SIGABRT 的旧名称 */
#define SIGCLD       SIGCHLD  /* SIGCHLD 的旧名称 */
```

**信号编号说明**

```c
/*
 * 信号编号 0：
 * 不表示真正的信号。
 *
 * kill(pid, 0) 可用于检查进程是否存在，
 * 不会真正向目标进程发送信号。
 *
 *
 * 信号编号 7 和 29：
 * 在当前 signum-generic.h 中没有分配给信号。
 *
 *
 * SIGKILL 和 SIGSTOP：
 * 不能被 signal() 捕获；
 * 不能被忽略；
 * 不能修改其默认处理方式。
 *
 *
 * 编程时应使用 SIGINT、SIGTERM 等宏，
 * 不应直接使用数字信号编号。
 */
```

#### 信号处理方式宏

**SIG_DFL、SIG_IGN、SIG_HOLD**

这些宏可以作为 `signal()` 的 `handler` 参数，用于指定信号的处理方式。

```c
#include <signal.h>

/**
 * @brief  使用该信号的系统默认处理方式。
 *
 * @note   这是宏，不是函数。
 */
#define SIG_DFL  ((__sighandler_t)0)


/**
 * @brief  忽略该信号。
 *
 * @note   这是宏，不是函数。
 */
#define SIG_IGN  ((__sighandler_t)1)


/**
 * @brief  将信号加入信号阻塞集合，使信号暂时处于等待状态。
 *
 * @note   这是宏，不是函数。
 * @note   只有定义了 __USE_XOPEN 时才会提供。
 */
#define SIG_HOLD ((__sighandler_t)2)
```

代码示例：

```c
signal(SIGINT, SIG_DFL);

/*
 * 将 SIGINT 设置为系统默认处理方式。
 *
 * SIGINT 通常由 Ctrl+C 产生，
 * 默认处理方式通常是终止进程。
 */


signal(SIGINT, SIG_IGN);

/*
 * 忽略 SIGINT。
 *
 * 设置后，按下 Ctrl+C 时，
 * 进程不会按照默认方式终止。
 */


signal(SIGINT, SIG_HOLD);

/*
 * 将 SIGINT 加入阻塞集合，
 * 使收到的 SIGINT 暂时处于等待状态。
 *
 * SIG_HOLD 不是所有使用环境都会提供。
 */
```

**SIG_ERR**

`SIG_ERR` 不是一种信号处理方式，而是 `signal()` 调用失败时的返回值。

```c
#include <signal.h>

/**
 * @brief  表示 signal() 调用失败。
 *
 * @note   这是宏，不是函数。
 */
#define SIG_ERR ((__sighandler_t)-1)
```

代码示例：

```c
sighandler_t ret;

ret = signal(SIGINT, SIG_IGN);

if (ret == SIG_ERR)
{
    /*
     * signal() 设置失败。
     */
}
```
### 7.4.2 函数
#### signal：设置信号处理方式

```c
/**
 * @brief  为指定信号设置处理方式。
 *
 * @param  signum: 需要处理的信号编号，如 SIGINT、SIGTERM、SIGIO。
 *				   evdev输入事件使用 SINGIO
 
 *				   在 Linux 的 evdev 驱动中，
 *				   当一组输入事件以 EV_SYN/SYN_REPORT 结束时，
 *				   内核会通过异步通知机制向进程发送 SIGIO，
 *				   表示设备中已经有数据可以读取。
 *
 *
 * @param  handler: 信号处理方式，可以是：
 *                  SIG_DFL，使用系统默认处理方式；
 *                  SIG_IGN，忽略该信号；
 *                  自定义信号处理函数。
 *
 * @retval 成功: 返回该信号原来的处理函数。
 *
 * @retval 失败: 返回 SIG_ERR，并设置 errno。
 */
#include <signal.h>

typedef void (*sighandler_t)(int);

sighandler_t signal(int signum, sighandler_t handler);
```

代码示例：

```c
void signal_handler(int signum)
{
    /*
     * signum 保存实际收到的信号编号。
     */
}

signal(SIGINT, signal_handler);

fcntl(fd, F_SETOWN, getpid());
flags = fcntl(fd, F_GETFL);
fcntl(fd, F_SETFL, flags | FASYNC);

/*
 * 当进程收到 SIGINT 信号时，
 * 系统会调用 signal_handler(SIGINT)。
 *
 * SIGINT 通常可以通过 Ctrl+C 产生。
 */
```

## 7.5 进程与休眠

### 7.5.1 函数
#### getpid：获取进程ID

```c
/**
 * @brief  获取当前进程的进程 ID。
 *
 * @param  无。
 *
 * @retval 当前进程的进程 ID。
 */
#include <sys/types.h>
#include <unistd.h>

pid_t getpid(void);
```

代码示例：

```c
pid_t pid;

pid = getpid();

/*
 * pid 保存当前进程的进程 ID。
 */
```
#### sleep：线程暂停

```c
/**
 * @brief  使当前线程暂停执行指定的秒数。
 *
 * @param  seconds: 需要暂停的秒数。
 *
 * @retval 0: 已经暂停了指定的时间。
 *
 * @retval >0: sleep 被信号提前中断，返回剩余未休眠的秒数。
 */
#include <unistd.h>

unsigned int sleep(unsigned int seconds);
```

sleep 是 POSIX 提供的函数，不属于 C/C++ 标准库，在 Linux 中常用。

基本用法：

```c
sleep(3);
```

表示当前线程暂停约 3 秒，然后继续向下执行。

例如：

```c
printf("start\n");

sleep(3);

printf("end\n");
```

sleep 只会使调用它的当前线程暂停，不会让整个系统停止运行。

#### nanosleep：ns级线程暂停

```c
/**
 * @brief  使当前线程暂停指定的一段时间，可以精确到纳秒级。
 *
 * @param  req: 指向 timespec 结构体，指定需要暂停的时间。
 *
 * @param  rem: 如果休眠被信号中断，用于保存剩余未休眠的时间。
 *              不需要保存剩余时间时可以设置为 NULL。
 *
 * @retval 0: 休眠时间完成。
 *
 * @retval -1: 休眠失败或被信号中断，并设置 errno。
 */
#include <time.h>

int nanosleep(const struct timespec *req,
              struct timespec *rem);
```

req 指向的 timespec 结构体用于指定休眠时间：

```c
struct timespec {
    time_t tv_sec;    /* 秒 */
    long   tv_nsec;   /* 纳秒：0 ~ 999999999 */
};
```

例如暂停 500 ms：

```c
struct timespec req;

req.tv_sec  = 0;
req.tv_nsec = 500 * 1000 * 1000;

nanosleep(&req, NULL);
```

时间换算：

```text
1 秒  = 1000 毫秒
1 毫秒 = 1000 微秒
1 微秒 = 1000 纳秒

500 ms = 500000000 ns
```

如果 nanosleep() 在休眠过程中被信号中断，并且 rem 不为 NULL，rem 中会保存还没有休眠完的剩余时间：

```c
struct timespec req;
struct timespec rem;

req.tv_sec  = 1;
req.tv_nsec = 0;

if (nanosleep(&req, &rem) == -1)
{
    /* rem 中保存剩余休眠时间 */
}
```

## 7.6 内存
### 7.6.1 函数
#### bzero：内存置0

```c
/**
 * @brief  将指定内存区域的前 n 个字节全部设置为 0。
 *
 * @param  s: 指向需要清零的内存区域。
 *
 * @param  n: 需要清零的字节数。
 *
 * @retval 无返回值。
 */
#include <strings.h>

void bzero(void *s, size_t n);
```

基本用法：

```c
char buf[100];

bzero(buf, sizeof(buf));
```

执行后，buf 的 100 个字节都会被设置为 0。

bzero 不是 ISO C 标准库函数，它来源于 BSD，在 Linux 等系统中可以使用。

在可移植的 C 程序中，通常可以使用 memset 代替：

```c
#include <string.h>

memset(buf, 0, sizeof(buf));
```


#### mmap ：地址映射函数

```c
/**
 * @brief  将文件或设备映射到内存中。
 *
 * @param  addr：指定映射到用户空间的起始地址。
 *         一般填 NULL，表示由系统自动分配地址。
 *
 * @param  length：映射区域的大小，单位是字节。
 *
 * @param  prot：映射区域的访问权限。
 *
 *         @arg PROT_READ
 *              映射区域可读。
 *
 *         @arg PROT_WRITE
 *              映射区域可写。
 *
 *         @arg PROT_READ | PROT_WRITE
 *              映射区域可读可写，开发板 LCD framebuffer 常用这种方式。
 *
 * @param  flags：映射方式。
 *
 *         @arg MAP_SHARED
 *              共享映射，对内存的修改会影响到文件或设备。
 *
 *         @arg MAP_PRIVATE
 *              私有映射，对内存的修改不会影响到原文件。
 *
 * @param  fd：文件描述符。
 *         由 open 函数打开文件或设备后获得。
 *
 * @param  offset：映射起始位置相对于文件开头的偏移量。
 *         一般填 0，表示从文件或设备起始位置开始映射。
 *
 * @retval 成功：返回映射后的内存地址。
 * @retval 失败：返回 MAP_FAILED。
 */
#include <sys/mman.h>

void *mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);
fb_base = mmap(NULL, screen_size, PROT_READ | PROT_WRITE, MAP_SHARED, fd_fb, 0);
说明:
mmap 常用于把 LCD framebuffer 映射到应用程序中。
映射成功后，就可以像操作普通内存一样操作 LCD 显存。
```

------

#### memset：内存数据设置函数

```c
/**
 * @brief  将一段内存中的数据设置为指定值。
 *
 * @param  s：要设置的内存起始地址。
 *
 * @param  c：要设置的值。
 *         注意：memset 是按字节设置数据。
 *
 * @param  n：要设置的字节数。
 *
 * @retval 返回 s，也就是内存起始地址。
 */
#include <string.h>

void *memset(void *s, int c, size_t n);
memset(fb_base, 0x00, screen_size);
说明:
这条语句表示把 framebuffer 显存全部清 0。
在 LCD 中通常可以理解为清屏。

注意:
memset 是按字节设置。
适合清 0 或设置成 0xff。
如果要设置具体颜色，通常要逐个像素赋值。
```

------

#### munmap：取消地址映射函数

```c
/**
 * @brief  取消 mmap 建立的内存映射。
 *
 * @param  addr：映射区域的起始地址。
 *         该地址一般是 mmap 的返回值。
 *
 * @param  length：映射区域的大小，单位是字节。
 *         该大小应和 mmap 时的 length 对应。
 *
 * @retval 成功：返回 0。
 * @retval 失败：返回 -1。
 */
#include <sys/mman.h>

int munmap(void *addr, size_t length);
munmap(fb_base, screen_size);
说明:
mmap 使用完成后，需要调用 munmap 取消映射。
一般在程序退出前调用。
```

## 7.7 网络编程
### 7.7.1 宏

#### INADDR_ANY

```c
#include <netinet/in.h>

#define INADDR_ANY ((in_addr_t) 0x00000000)
```

作用：

```text
表示任意本地 IPv4 地址。

服务器绑定地址时使用 INADDR_ANY，
表示允许客户端通过本机任意网络接口的 IPv4 地址连接服务器。
```

代码示例：

```c
#include <netinet/in.h>

struct sockaddr_in server_addr = {0};

server_addr.sin_family = AF_INET;
server_addr.sin_port = htons(8888);

/* 绑定本机所有 IPv4 网络接口 */
server_addr.sin_addr.s_addr = INADDR_ANY;
```
### 7.7.2 数据类型
#### sockaddr_in

作用：

用于保存 **IPv4 网络地址信息**，主要包括地址族、端口号和 IPv4 地址。

在 IPv4 socket 编程中，`bind()`、`connect()`、`accept()` 等函数经常配合该结构体使用。

```c
#include <netinet/in.h>

struct sockaddr_in
{
    sa_family_t    sin_family;   // 地址族
    in_port_t      sin_port;     // 端口号
    struct in_addr sin_addr;     // IPv4 地址
    unsigned char  sin_zero[8];  // 填充字段
};
```

成员说明：

```text
sin_family：
地址族。
IPv4 网络编程中设置为 AF_INET。

sin_port：
端口号。
通常使用 htons() 将端口号转换为网络字节序后保存。

sin_addr：
IPv4 地址。
用于保存设备的 IPv4 地址。

sin_zero：
填充字段。
一般清零，不用于保存实际的网络地址信息。
```

代码示例：

```c
#include <netinet/in.h>
#include <arpa/inet.h>

struct sockaddr_in server_addr = {0};

server_addr.sin_family = AF_INET;
server_addr.sin_port = htons(8888);
inet_aton("192.168.1.100", &server_addr.sin_addr);

//服务器一般使用这个
server_addr.sin_addr.s_addr = INADDR_ANY;
```

#### sockaddr

作用：

用于表示一种**通用的 socket 地址结构**。

很多 socket 函数为了能够同时接收 IPv4、IPv6 等不同类型的地址，参数统一使用 `struct sockaddr *`。

实际进行 IPv4 编程时，通常先使用 `struct sockaddr_in` 保存地址，再将它的指针强制转换为 `struct sockaddr *` 传给 socket 函数。

```c
#include <sys/socket.h>

struct sockaddr
{
    sa_family_t sa_family;   // 地址族
    char        sa_data[14]; // 地址数据
};
```

成员说明：

```text
sa_family：
地址族。
用于表示地址属于哪一种协议族，例如 IPv4 使用 AF_INET。

sa_data：
保存与地址相关的数据。

实际进行 IPv4 编程时，
通常不会直接操作 sa_data，
而是使用 struct sockaddr_in 保存具体地址信息。

struct sockaddr_in 用于实际保存 IPv4 地址信息，而 struct sockaddr 是 socket 接口使用的通用地址结构。为了让 bind()、connect() 等函数能够统一接收 IPv4、IPv6 等不同类型的地址，它们的参数统一定义为 struct sockaddr *。因此使用 IPv4 时，需要将 struct sockaddr_in * 强制转换为 struct sockaddr * 后传入函数；函数再根据地址族（如 AF_INET）判断实际的地址类型。
```

代码示例：

```c
#include <sys/socket.h>
#include <netinet/in.h>

struct sockaddr_in ipv4_addr;

/* 将 IPv4 地址结构体指针转换为通用地址结构体指针 */
struct sockaddr *addr;

addr = (struct sockaddr *)&ipv4_addr;
```

#### in_addr

作用：

用于保存一个 **IPv4 地址**。

它通常作为 `struct sockaddr_in` 的 `sin_addr` 成员使用，用来存放网络通信中的 IPv4 地址。

```c
#include <netinet/in.h>

struct in_addr
{
    in_addr_t s_addr;    // IPv4 地址
};
```

成员说明：

```text
s_addr：
用于保存 IPv4 地址。

IPv4 地址以网络字节序的形式保存。
```

代码示例：

```c
#include <arpa/inet.h>

struct in_addr addr;

/* 将字符串形式的 IPv4 地址转换后保存到 addr 中 */
inet_aton("192.168.1.100", &addr);
```

#### socklen_t

```c
#include <sys/socket.h>
```

socklen_t 是用于表示 **socket 地址结构体长度** 的数据类型。

它常用于保存 sockaddr、sockaddr_in 等地址结构体的大小，并作为 accept()、recvfrom()、getsockname()、getpeername() 等函数的地址长度参数类型。

具体底层整数类型由系统实现决定，因此网络编程中应直接使用 socklen_t，而不要用 int 代替。

常见用法：

```c
struct sockaddr_in client_addr;
socklen_t addrlen;

addrlen = sizeof(client_addr);

accept(sockfd,
       (struct sockaddr *)&client_addr,
       &addrlen);
```

在 accept()、recvfrom() 等函数中，addrlen 通常具有输入和输出两种作用：

```text
调用前：保存地址结构体缓冲区的大小
调用后：保存实际返回的地址结构体长度
```

例如：

```c
socklen_t addrlen = sizeof(client_addr);

recvfrom(sockfd,
         buf,
         sizeof(buf),
         0,
         (struct sockaddr *)&client_addr,
         &addrlen);
```

### 7.7.3 函数
#### socket

```c
/**
 * @brief  创建一个 socket(套接字，可以理解为端口)，并返回对应的文件描述符。
 *
 * @param  domain: 通信地址族。
 *                 IPv4 常用 AF_INET。
 *
 * @param  type: socket 类型（可通过man socket查询）。
 *               TCP 常用 SOCK_STREAM。
 *               UDP 常用 SOCK_DGRAM
 *
 * @param  protocol: 使用的协议。
 *                   通常设置为 0，由系统根据 domain 和 type 自动选择。
 *
 * @retval >=0: 创建成功，返回 socket 文件描述符。
 *
 * @retval -1: 创建失败。
 */
#include <sys/socket.h>

int socket(int domain, int type, int protocol);
```

代码示例：

```c
int sockfd;

/* 创建一个 IPv4 TCP socket */
sockfd = socket(AF_INET, SOCK_STREAM, 0);

if (sockfd == -1)
{
    /* socket 创建失败 */
}
```

#### bind

```c
/**
 * @brief  将 socket 与本地 IP 地址和端口号绑定。
 *
 * @param  sockfd: socket() 创建的套接字文件描述符。
 *
 * @param  addr: 指向本地地址结构体的指针。
 *
 * @param  addrlen: 地址结构体的大小。
 *
 * @retval 0: 绑定成功。
 *
 * @retval -1: 绑定失败。
 */
#include <sys/socket.h>

int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```

代码示例：

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int sockfd;
struct sockaddr_in server_addr = {0};

sockfd = socket(AF_INET, SOCK_STREAM, 0);

server_addr.sin_family = AF_INET;
server_addr.sin_port = htons(8888);
server_addr.sin_addr.s_addr = INADDR_ANY;

/* 将 socket 绑定到本机的 8888 端口 */
if (bind(sockfd,
         (const struct sockaddr *)&server_addr,
         sizeof(server_addr)) == -1)
{
    /* 绑定失败 */
}
```

#### listen

```c
/**
 * @brief  将 socket 设置为监听状态，等待客户端连接。
 *
 * @param  sockfd: 已经通过 bind() 绑定地址的 socket 文件描述符。
 *
 * @param  backlog: 等待连接队列的长度限制。
 *
 * @retval 0: 设置监听成功。
 *
 * @retval -1: 设置监听失败。
 */
#include <sys/socket.h>

int listen(int sockfd, int backlog);
```

代码示例：

```c
#include <sys/socket.h>

#define BACKLOG 10

/* 开始监听客户端连接 */
if (listen(sockfd, BACKLOG) == -1)
{
    /* 设置监听失败 */
}
```

#### accept

```c
/**
 * @brief  从监听 socket 中接收一个客户端连接，
 *         并返回一个新的 socket 文件描述符用于与该客户端通信。
 *
 * @param  sockfd: 处于监听状态的 socket 文件描述符。
 *
 * @param  addr: 用于保存客户端地址信息。
 *               不需要客户端地址时可以传入 NULL。
 *
 * @param  addrlen: 输入时表示 addr 缓冲区大小，
 *                  返回时表示实际客户端地址长度。
 *
 * @retval >=0: 接收连接成功，返回新的客户端 socket 文件描述符。
 *
 * @retval -1: 接收连接失败。
 */
#include <sys/socket.h>

int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

代码示例：

```c
#include <sys/socket.h>
#include <netinet/in.h>

int client_fd;
struct sockaddr_in client_addr;
socklen_t addr_len;

addr_len = sizeof(client_addr);

/* 等待并接收客户端连接 */
client_fd = accept(sockfd,
                   (struct sockaddr *)&client_addr,
                   &addr_len);

if (client_fd == -1)
{
    /* 接收连接失败 */
}
```

#### connect

```c
/**
 * @brief  主动连接指定的服务器。
 *
 * @param  sockfd: socket() 创建的套接字文件描述符。
 *
 * @param  addr: 指向服务器地址结构体的指针，
 *               通常将 struct sockaddr_in * 转换为 struct sockaddr *。
 *
 * @param  addrlen: 地址结构体的大小。
 *
 * @retval 0: 连接成功。
 *
 * @retval -1: 连接失败。
 */
#include <sys/socket.h>

int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```

代码示例：

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int sockfd;
struct sockaddr_in server_addr = {0};

sockfd = socket(AF_INET, SOCK_STREAM, 0);

server_addr.sin_family = AF_INET;
server_addr.sin_port = htons(8888);
inet_aton("192.168.1.100", &server_addr.sin_addr);

/* 连接服务器 */
if (connect(sockfd,
            (const struct sockaddr *)&server_addr,
            sizeof(server_addr)) == -1)
{
    /* 连接失败 */
}
```

#### recv

```c
/**
 * @brief  从已经连接的 socket 中接收数据。
 *
 * @param  sockfd: socket 文件描述符。
 *
 * @param  buf: 用于保存接收数据的缓冲区。
 *
 * @param  len: 缓冲区最多可以接收的字节数。
 *
 * @param  flags: 接收控制标志。
 *                不需要特殊功能时通常设置为 0。
 *
 * @retval >0: 实际接收到的字节数。
 *
 * @retval 0: 对端已经正常关闭连接。
 *
 * @retval -1: 接收失败。
 */
#include <sys/socket.h>

ssize_t recv(int sockfd, void *buf, size_t len, int flags);
```

代码示例：

```c
#include <sys/socket.h>

char buf[1000];
ssize_t recv_len;

/* 最多接收 999 个字节，预留一个字节存放 '\0' */
recv_len = recv(client_fd, buf, sizeof(buf) - 1, 0);

if (recv_len > 0)
{
    /* 将接收到的数据作为字符串使用时补上结束符 */
    buf[recv_len] = '\0';
}
else if (recv_len == 0)
{
    /* 对端关闭连接 */
}
else
{
    /* 接收失败 */
}
```


#### send

```c
/**
 * @brief  通过已连接的 socket 发送数据。
 *
 * @param  sockfd: socket 文件描述符。
 *
 * @param  buf: 指向待发送数据的缓冲区。
 *
 * @param  len: 要发送的数据长度，单位为字节。
 *
 * @param  flags: 发送控制标志。
 *                不需要特殊功能时通常设置为 0。
 *
 * @retval >0: 实际发送的字节数。
 *
 * @retval 0: 没有发送数据。
 *
 * @retval -1: 发送失败。
 */
#include <sys/socket.h>

ssize_t send(int sockfd, const void *buf, size_t len, int flags);
```

代码示例：

```c
#include <sys/socket.h>
#include <string.h>

char buf[] = "hello";

ssize_t ret;

/* 发送字符串中的数据 */
ret = send(sockfd, buf, strlen(buf), 0);

if (ret == -1)
{
    /* 发送失败 */
}
```

#### recvfrom

```c
/**
 * @brief  从 socket 中接收数据，并获取发送方的地址信息，常用于 UDP 通信。
 *
 * @param  sockfd: socket 文件描述符。
 *
 * @param  buf: 用于保存接收数据的缓冲区。
 *
 * @param  len: 缓冲区可接收的最大数据长度。
 *
 * @param  flags: 接收标志，通常设置为 0。
 *
 * @param  src_addr: 用于保存发送方地址信息。
 *
 * @param  addrlen: 输入时表示 src_addr 缓冲区大小，
 *                  返回时保存实际的发送方地址结构大小。
 *
 * @retval >=0: 实际接收到的数据字节数。
 *
 * @retval -1: 接收失败。
 */
#include <sys/socket.h>

ssize_t recvfrom(int sockfd, void *buf, size_t len, int flags,
                 struct sockaddr *src_addr, socklen_t *addrlen);
```

代码示例：

```c
#include <sys/socket.h>
#include <netinet/in.h>

char buf[1000];
struct sockaddr_in client_addr;
socklen_t addrlen;
ssize_t ret;

addrlen = sizeof(client_addr);

ret = recvfrom(sockfd,
               buf,
               sizeof(buf) - 1,
               0,
               (struct sockaddr *)&client_addr,
               &addrlen);

if (ret >= 0)
{
    buf[ret] = '\0';
}
```

recvfrom 除了接收数据以外，还可以获得**是谁发送了这份数据**，因此 UDP 服务器通常使用它接收客户端数据。

#### sendto

```c
/**
 * @brief  通过 socket 向指定地址发送数据，常用于 UDP 通信。
 *
 * @param  sockfd: socket 文件描述符。
 *
 * @param  buf: 指向待发送数据的缓冲区。
 *
 * @param  len: 要发送的数据长度，单位为字节。
 *
 * @param  flags: 发送标志，通常设置为 0。
 *
 * @param  dest_addr: 指向目标地址结构体。
 *
 * @param  addrlen: 目标地址结构体的大小。
 *
 * @retval >=0: 实际发送的数据字节数。
 *
 * @retval -1: 发送失败。
 */
#include <sys/socket.h>

ssize_t sendto(int sockfd, const void *buf, size_t len, int flags,
               const struct sockaddr *dest_addr, socklen_t addrlen);
```

代码示例：

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <string.h>

char buf[] = "hello";
struct sockaddr_in server_addr;
ssize_t ret;

ret = sendto(sockfd,
             buf,
             strlen(buf),
             0,
             (const struct sockaddr *)&server_addr,
             sizeof(server_addr));
```

sendto 在发送数据时直接指定**目标 IP 地址和端口号**，因此 UDP 不需要像 TCP 一样先通过 connect 建立连接后再发送数据。

#### htons

```c
/**
 * @brief  将 16 位整数从主机字节序转换为网络字节序，
 *         网络编程中通常用于转换端口号。
 *
 * @param  hostshort: 主机字节序的 16 位整数。
 *
 * @retval 返回转换后的网络字节序数值。
 */
#include <arpa/inet.h>

uint16_t htons(uint16_t hostshort);
```

代码示例：

```c
#include <arpa/inet.h>

struct sockaddr_in server_addr;

/* 将端口号 8888 转换为网络字节序 */
server_addr.sin_port = htons(8888);
```

#### inet_aton

```c
/**
 * @brief  将点分十进制形式的 IPv4 地址字符串
 *         转换为网络地址，并保存到 struct in_addr 中。
 *
 * @param  cp: IPv4 地址字符串。
 *
 * @param  inp: 用于保存转换结果的 struct in_addr 地址。
 *
 * @retval 1: 转换成功。
 *
 * @retval 0: IPv4 地址格式无效。
 */
#include <arpa/inet.h>

int inet_aton(const char *cp, struct in_addr *inp);
```

代码示例：

```c
#include <arpa/inet.h>

struct in_addr addr;

if (inet_aton("192.168.1.100", &addr) == 0)
{
    /* IPv4 地址格式无效 */
}
```

#### inet_ntoa

```c
/**
 * @brief  将 struct in_addr 中保存的 IPv4 地址
 *         转换为点分十进制字符串。
 *
 * @param  in: 要转换的 IPv4 地址。
 *
 * @retval 成功: 返回 IPv4 地址字符串的指针。
 */
#include <arpa/inet.h>

char *inet_ntoa(struct in_addr in);
```

代码示例：

```c
#include <arpa/inet.h>
#include <stdio.h>

struct sockaddr_in client_addr;

/*
 * 假设 client_addr 已经由 accept() 得到客户端地址，
 * 将客户端 IPv4 地址转换为字符串。
 */
printf("client ip: %s\n",
       inet_ntoa(client_addr.sin_addr));
```

### 7.7.4 TCP网络编程流程

```text
服务器端                                   客户端

socket()                                  socket()
创建 TCP socket                           创建 TCP socket
   ↓                                         ↓
bind()                                   connect()
绑定本机 IP 和端口                        主动连接服务器的 IP 和端口
   ↓                                         │
listen()                                     │
监听客户端连接                               │
   ↓                                         │
accept() ←──────── 建立 TCP 连接 ────────────┘
接受客户端连接
   ↓
recv()  ←────────────── send()
接收客户端数据              发送数据

send()  ───────────────→ recv()
发送数据                    接收服务器数据
   ↓                                         ↓
close()                                  close()
关闭 socket                              关闭 socket
```

### 7.7.5 UDP网络编程流程
```
服务器端                                   客户端

socket()                                  socket()
创建 UDP socket                           创建 UDP socket
   ↓                                         ↓
bind()                                      │
绑定本机 IP 和端口                           │
   ↓                                         │
recvfrom() ←──────────── sendto() ───────────┘
接收客户端数据                 向服务器发送数据
   ↓
sendto() ─────────────→ recvfrom()
向客户端发送数据               接收服务器数据
   ↓                                         ↓
close()                                  close()
关闭 socket                              关闭 socket
```

## 7.8 串口
### 7.8.1 宏
#### struct termios相关宏

需要包含的头文件：

```c
#include <termios.h>
```

struct termios 中的 c_iflag、c_oflag、c_cflag、c_lflag 和 c_cc 成员，需要配合一组宏来设置串口的工作方式。

---

##### c_cflag 常用宏

c_cflag 用于设置串口的硬件通信参数，例如数据位、停止位、校验位和接收功能。

```c
CLOCAL      // 忽略调制解调器控制线，串口程序中通常需要设置
CREAD       // 使能接收功能

CSIZE       // 数据位宽度的掩码，修改数据位之前通常先清除它
CS5         // 5 个数据位
CS6         // 6 个数据位
CS7         // 7 个数据位
CS8         // 8 个数据位

CSTOPB      // 设置时使用 2 个停止位，清除时使用 1 个停止位

PARENB      // 使能奇偶校验
PARODD      // 设置时为奇校验，清除时为偶校验

HUPCL       // 最后一个进程关闭串口时降低调制解调器控制线
CRTSCTS     // 启用 RTS/CTS 硬件流控
```

常见设置：

```c
/* 允许本地连接并使能接收 */
newtio.c_cflag |= CLOCAL | CREAD;

/* 设置为 8 个数据位 */
newtio.c_cflag &= ~CSIZE;
newtio.c_cflag |= CS8;

/* 设置为 1 个停止位 */
newtio.c_cflag &= ~CSTOPB;

/* 关闭奇偶校验 */
newtio.c_cflag &= ~PARENB;

/* 关闭硬件流控 */
newtio.c_cflag &= ~CRTSCTS;
```

---

##### c_iflag 常用宏

c_iflag 用于控制接收到的数据如何处理。

```c
IGNBRK      // 忽略 BREAK 状态
BRKINT      // 检测到 BREAK 时产生中断处理

IGNPAR      // 忽略存在奇偶校验错误或帧错误的字符
PARMRK      // 对奇偶校验错误或帧错误进行特殊标记
INPCK       // 启用输入数据的奇偶校验检查
ISTRIP      // 将接收到字符的最高位清零

INLCR       // 将输入的换行符 NL 转换为回车符 CR
IGNCR       // 忽略输入的回车符 CR
ICRNL       // 将输入的回车符 CR 转换为换行符 NL

IXON        // 启用输出方向的软件流控
IXOFF       // 启用输入方向的软件流控
IXANY       // 任意字符都可以重新启动被暂停的输出
```

例如使用奇偶校验时：

```c
newtio.c_iflag |= INPCK;
```

不需要软件流控时通常可以关闭：

```c
newtio.c_iflag &= ~(IXON | IXOFF | IXANY);
```

---

##### c_oflag 常用宏

c_oflag 用于设置数据发送出去之前是否进行额外处理。

```c
OPOST       // 启用输出数据处理
ONLCR       // 输出 NL 时转换为 CR + NL
OCRNL       // 输出 CR 时转换为 NL
ONOCR       // 在每行开头不输出 CR
ONLRET      // NL 执行回车功能
```

串口进行原始数据通信时，通常关闭输出处理：

```c
newtio.c_oflag &= ~OPOST;
```

这样 write 写入的数据通常不会再经过终端输出转换。

---

##### c_lflag 常用宏

c_lflag 用于控制终端本地的数据处理方式。

```c
ICANON      // 启用规范模式，按行读取数据
ECHO        // 回显输入字符
ECHOE       // 回显擦除字符
ECHOK       // 执行删除一行时进行相应回显
ECHONL      // 即使关闭 ECHO，也回显换行符

ISIG        // 使 INTR、QUIT、SUSP 等字符产生信号
IEXTEN      // 启用实现定义的扩展输入处理

NOFLSH      // 收到信号字符时不清空输入、输出队列
TOSTOP      // 后台进程向终端写数据时产生 SIGTTOU 信号
```

串口进行原始数据通信时，通常关闭规范模式、回显和信号处理：

```c
newtio.c_lflag &= ~(ICANON | ECHO | ECHOE | ISIG);
```

---

##### c_cc 常用宏

c_cc 是特殊控制字符数组，这些宏作为数组下标使用。

```c
VINTR       // 中断字符，通常对应 Ctrl+C
VQUIT       // 退出字符
VERASE      // 删除前一个字符
VKILL       // 删除当前输入行
VEOF        // 文件结束字符
VEOL        // 行结束字符

VSTART      // 软件流控中的开始字符
VSTOP       // 软件流控中的停止字符
VSUSP       // 挂起字符

VMIN        // 非规范模式下 read 返回前至少需要读取的字符数
VTIME       // 非规范模式下 read 的超时参数
```

串口应用编程中最常用的是 VMIN 和 VTIME：

```c
newtio.c_cc[VMIN]  = 1;
newtio.c_cc[VTIME] = 0;
```

表示在非规范模式下，read 至少读取到 1 个字符后才返回，并且不使用超时计时。

---

##### 常见的 8N1 原始串口配置

```c
/* 允许本地连接并使能接收 */
newtio.c_cflag |= CLOCAL | CREAD;

/* 8 个数据位 */
newtio.c_cflag &= ~CSIZE;
newtio.c_cflag |= CS8;

/* 无校验 */
newtio.c_cflag &= ~PARENB;

/* 1 个停止位 */
newtio.c_cflag &= ~CSTOPB;

/* 关闭规范模式、回显和信号处理 */
newtio.c_lflag &= ~(ICANON | ECHO | ECHOE | ISIG);

/* 关闭输出处理 */
newtio.c_oflag &= ~OPOST;

/* read 至少读取 1 个字节 */
newtio.c_cc[VMIN]  = 1;
newtio.c_cc[VTIME] = 0;
```
### 7.8.2 数据结构
#### struct termios

需要包含的头文件：

```c
#include <termios.h>
```

struct termios 是 Linux/Unix 中用于保存终端或串口配置参数的结构体。

串口的输入模式、输出模式、数据位、停止位、校验方式以及特殊控制字符等参数，都通过这个结构体进行配置。

常用成员可以表示为：

```c
struct termios
{
    tcflag_t c_iflag;      /* 输入模式标志 */
    tcflag_t c_oflag;      /* 输出模式标志 */
    tcflag_t c_cflag;      /* 控制模式标志 */
    tcflag_t c_lflag;      /* 本地模式标志 */
    cc_t     c_cc[NCCS];   /* 特殊控制字符 */
};
```

不同系统的 struct termios 实际定义可能还包含其他成员。

常用成员：

|成员|作用|
|---|---|
|c_iflag|设置输入数据的处理方式|
|c_oflag|设置输出数据的处理方式|
|c_cflag|设置串口硬件通信参数|
|c_lflag|设置终端本地处理方式|
|c_cc|设置特殊控制字符和读取控制参数|

常见使用流程

```c
struct termios options;

/* 获取当前配置 */
tcgetattr(fd, &options);

/* 修改 options 中的各种参数 */

/* 设置波特率 */
cfsetispeed(&options, B115200);
cfsetospeed(&options, B115200);

/* 将配置设置到串口 */
tcsetattr(fd, TCSANOW, &options);
```
#### tcflag_t

需要包含的头文件：

```c
#include <termios.h>
```

tcflag_t 是 termios 接口定义的一种数据类型，用于保存各种终端和串口模式标志。

struct termios 中下面几个成员都使用 tcflag_t：

```c
tcflag_t c_iflag;
tcflag_t c_oflag;
tcflag_t c_cflag;
tcflag_t c_lflag;
```

这些成员中的每一位可以表示不同的配置选项，因此通常通过按位与、按位或等位操作进行修改。

例如：

```c
options.c_cflag |= CLOCAL;
```

表示打开 CLOCAL 标志。

```c
options.c_cflag &= ~CSIZE;
```

表示清除 CSIZE 对应的数据位设置。

tcflag_t 的具体底层整数类型由系统实现决定，程序通常不需要关心其实际字节大小。
#### speed_t

需要包含的头文件：

```c
#include <termios.h>
```

speed_t 是 termios 接口定义的数据类型，用于表示终端或串口的波特率。

cfsetispeed、cfsetospeed 和 cfsetspeed 的波特率参数都使用 speed_t。

例如：

```c
int cfsetispeed(struct termios *termios_p, speed_t speed);

int cfsetospeed(struct termios *termios_p, speed_t speed);
```

设置波特率时通常不直接填写数字，而是使用 termios.h 中定义的波特率宏：

```c
B9600
B19200
B38400
B57600
B115200
```

例如：

```c
cfsetispeed(&options, B115200);
cfsetospeed(&options, B115200);
```

表示将串口输入和输出波特率都设置为 115200。

speed_t 的具体底层整数类型由系统实现决定，程序通常直接使用 B9600、B115200 等波特率宏进行设置。
### 7.8.3 函数
#### tcgetattr

```c
/**
 * @brief  获取终端或串口当前的 termios 配置参数。
 *
 * @param  fd: 已经打开的终端或串口设备的文件描述符。
 *
 * @param  termios_p: 指向 struct termios 的指针，
 *                    用于保存读取到的终端或串口配置。
 *
 * @retval 0: 获取成功。
 *
 * @retval -1: 获取失败，并设置 errno。
 */
#include <termios.h>

int tcgetattr(int fd, struct termios *termios_p);
```

作用：

tcgetattr 用于读取串口当前的配置参数，并保存到 struct termios 结构体中。

通常在修改串口参数之前，先使用 tcgetattr 获取原来的配置。

```c
struct termios options;

if (tcgetattr(fd, &options) == -1)
{
    /* 获取失败 */
}
```
#### tcsetattr

```c
/**
 * @brief  将 struct termios 中的配置设置到终端或串口设备。
 *
 * @param  fd: 已经打开的终端或串口设备的文件描述符。
 *
 * @param  optional_actions: 指定新的配置什么时候生效。
 *
 * @param  termios_p: 指向保存新配置的 struct termios 结构体。
 *
 * @retval 0: 设置成功。
 *
 * @retval -1: 设置失败，并设置 errno。
 */
#include <termios.h>

int tcsetattr(int fd,
              int optional_actions,
              const struct termios *termios_p);
```

optional_actions 常用取值：

```c
TCSANOW      // 立即使新的配置生效

TCSADRAIN    // 等待已经发送的数据发送完成后，再使新配置生效

TCSAFLUSH    // 等待已经发送的数据发送完成，
             // 丢弃尚未读取的输入数据，然后使新配置生效
```

常见使用：

```c
struct termios options;

/* 修改 options 中的串口参数 */

if (tcsetattr(fd, TCSANOW, &options) == -1)
{
    /* 设置失败 */
}
```
#### tcflush

```c
/**
 * @brief  清空终端或串口中尚未处理的输入数据或输出数据。
 *
 * @param  fd: 已经打开的终端或串口设备的文件描述符。
 *
 * @param  queue_selector: 指定需要清空的数据队列。
 *
 * @retval 0: 操作成功。
 *
 * @retval -1: 操作失败，并设置 errno。
 */
#include <termios.h>

int tcflush(int fd, int queue_selector);
```

queue_selector 常用取值：

```c
TCIFLUSH     // 丢弃已经接收到、但程序尚未读取的输入数据

TCOFLUSH     // 丢弃等待发送、但尚未发送出去的输出数据

TCIOFLUSH    // 同时清空输入和输出数据
```

常见使用：

```c
tcflush(fd, TCIOFLUSH);
```

表示清空当前串口尚未处理的输入和输出数据。
#### cfsetispeed

```c
/**
 * @brief  设置 struct termios 中的输入波特率。
 *
 * @param  termios_p: 指向需要修改的 struct termios 结构体。
 *
 * @param  speed: 要设置的输入波特率。
 *
 * @retval 0: 设置成功。
 *
 * @retval -1: 设置失败。
 */
#include <termios.h>

int cfsetispeed(struct termios *termios_p, speed_t speed);
```

speed 使用 speed_t 类型，通常使用 termios.h 中定义的波特率宏，例如：

```c
B9600
B19200
B38400
B57600
B115200
```

常见使用：

```c
struct termios options;

cfsetispeed(&options, B115200);
```

表示把输入波特率设置为 115200。

cfsetispeed 只是修改 struct termios 中保存的配置。

通常还需要调用 tcsetattr，才会把配置真正设置到串口设备。

## 7.9 I2C

**测光强、距离、红外:**
[[AP3216C.pdf#page=10]]
**I2C读写eeprom的原理图与芯片手册**
[[i2c_eeprom_module_v1.0.pdf]]
[[AT24cxx.pdf]]
### 7.9.1 宏
#### I2C设备相关宏

```c
#include <linux/i2c.h>
#include <linux/i2c-dev.h>

#define I2C_M_RD          0x0001  /* i2c_msg 为读操作，不设置则表示写操作 */

#define I2C_SLAVE         0x0703  /* 设置当前要访问的 I2C 从设备地址 */

#define I2C_SLAVE_FORCE   0x0706  /* 强制设置从设备地址，即使该设备已被内核驱动占用 */

#define I2C_RDWR          0x0707  /* 使用多个 i2c_msg 完成组合 I2C 读写传输 */

#define I2C_SMBUS         0x0720  /* 执行 SMBus 传输 */
```

**用法示例：**
**I2C_M_RD** 用在 i2c_msg.flags 中：

```c
struct i2c_msg msg;

msg.flags = 0;          /* 写 */
msg.flags = I2C_M_RD;   /* 读 */
```

**I2C_SLAVE** 通常和 ioctl() 配合，用来指定后续要访问的从设备：

```c
int fd;

fd = open("/dev/i2c-0", O_RDWR);

ioctl(fd, I2C_SLAVE, 0x50);
```

表示：

```text
使用 /dev/i2c-0
        ↓
访问设备地址 0x50
```

如果设备地址已经被某个内核驱动占用：

```c
ioctl(fd, I2C_SLAVE, 0x50);
```

可能失败。

**I2C_SLAVE_FORCE** 可以强制访问：

```c
ioctl(fd, I2C_SLAVE_FORCE, 0x50);
```

一般不建议随意使用，因为可能和已有内核驱动同时访问同一个设备。

I2C_RDWR 用于普通 I2C 的组合传输：

```c
struct i2c_rdwr_ioctl_data rdwr;

ioctl(fd, I2C_RDWR, &rdwr);
```

可以实现：

```text
写 i2c_msg
    ↓
Repeated START
    ↓
读 i2c_msg
    ↓
STOP
```

**I2C_SMBUS** 用于 SMBus 方式传输：

```c
struct i2c_smbus_ioctl_data args;

ioctl(fd, I2C_SMBUS, &args);
```

实际编写用户程序时，一般优先使用 libi2c 提供的 i2c_smbus_() 函数，而不是自己直接构造 I2C_SMBUS ioctl 参数。

### 7.9.2 数据类型
#### i2c_adapter

i2c_adapter 用来表示一个 I2C BUS，也就是一个 I2C Controller。

一个芯片中可能有多个 I2C Controller，每个控制器对应一个 i2c_adapter。

```c
#include <linux/i2c.h>

struct i2c_adapter {
    struct module *owner;                       /* 拥有该 I2C Adapter 的内核模块 */
    unsigned int class;                         /* Adapter 的设备类别，用于设备探测 */
    const struct i2c_algorithm *algo;           /* I2C 数据传输算法 */
    void *algo_data;                            /* 传输算法使用的私有数据 */

    const struct i2c_lock_operations *lock_ops; /* I2C 总线的加锁、解锁操作 */
    struct rt_mutex bus_lock;                   /* I2C 总线互斥锁 */
    struct rt_mutex mux_lock;                   /* I2C 多路复用相关互斥锁 */
    int timeout;                                /* I2C 传输超时时间 */
    int retries;                                /* I2C 传输失败时的重试次数 */
    struct device dev;                          /* Linux 设备模型中的 device 对象 */

    int nr;                                     /* 第几个 I2C BUS / I2C Controller */
    char name[48];                              /* I2C Adapter 的名称 */
    struct completion dev_released;             /* 用于等待 Adapter 对应设备被释放 */

    struct mutex userspace_clients_lock;        /* 保护 userspace_clients 链表 */
    struct list_head userspace_clients;         /* 用户空间创建的 I2C Client 链表 */

    struct i2c_bus_recovery_info *bus_recovery_info; /* I2C 总线恢复相关信息 */
    const struct i2c_adapter_quirks *quirks;    /* I2C Controller 的特殊限制 */
};
```

当前阶段重点记住：

- nr：表示这是第几个 I2C Controller。
    
- algo：指向 i2c_algorithm，表示这个 I2C Controller 怎么传输数据。
    

可以简单理解为：**i2c_adapter 表示一个 I2C Controller。**

代码示例：

```c
struct i2c_adapter *adapter;

/* 获取编号为 0 的 I2C Adapter */
adapter = i2c_get_adapter(0);

if (adapter) {
    /* adapter->nr 为该 I2C Adapter 的编号 */
    printk("I2C adapter nr = %d\n", adapter->nr);

    /* 使用完成后释放 */
    i2c_put_adapter(adapter);
}
```

这里的 `0` 表示获取第 0 个 I2C BUS / I2C Controller。
#### i2c_algorithm

i2c_algorithm 用来描述 I2C Controller 的数据传输方法。

i2c_adapter 中的 algo 成员指向 i2c_algorithm，通过其中的函数完成普通 I2C 或 SMBus 数据传输。

```c
#include <linux/i2c.h>

struct i2c_algorithm {
    int (*master_xfer)(struct i2c_adapter *adap,
                       struct i2c_msg *msgs,
                       int num);                /* 使用普通 I2C 方式传输 i2c_msg */

    int (*smbus_xfer)(struct i2c_adapter *adap,
                      u16 addr,
                      unsigned short flags,
                      char read_write,
                      u8 command,
                      int size,
                      union i2c_smbus_data *data); /* 使用 SMBus 方式传输数据 */

    u32 (*functionality)(struct i2c_adapter *); /* 返回 Adapter 支持的 I2C/SMBus 功能 */

#if IS_ENABLED(CONFIG_I2C_SLAVE)
    int (*reg_slave)(struct i2c_client *client);   /* 注册 I2C 从机 */
    int (*unreg_slave)(struct i2c_client *client); /* 注销 I2C 从机 */
#endif
};
```

master_xfer 中：

- adap：要使用的 I2C Controller。
    
- msgs：要传输的 i2c_msg 数组。
    
- num：要传输的 i2c_msg 数量。
    

smbus_xfer 用来进行 SMBus 数据传输。

可以简单理解为：**i2c_algorithm 表示 I2C Controller 怎么传输数据。**

代码示例：

```c
static int my_i2c_xfer(struct i2c_adapter *adap,
                       struct i2c_msg *msgs,
                       int num)
{
    /* 根据 msgs 中的内容进行 I2C 数据传输 */

    return num;
}

static u32 my_i2c_func(struct i2c_adapter *adap)
{
    return I2C_FUNC_I2C;
}

static const struct i2c_algorithm my_i2c_algo = {
    .master_xfer  = my_i2c_xfer,
    .functionality = my_i2c_func,
};
```

这里把：

```c
my_i2c_xfer
```

赋给 master_xfer，表示这个 I2C Controller 使用 my_i2c_xfer 完成普通 I2C 数据传输。

#### i2c_client

i2c_client 用来表示连接在 I2C 总线上的一个 I2C Device。

一个 I2C Device 最重要的信息是设备地址，以及它连接在哪一个 I2C Controller 上。

```c
#include <linux/i2c.h>

struct i2c_client {
    unsigned short flags;          /* I2C Device 的相关标志 */
    unsigned short addr;           /* I2C 设备地址 */
    char name[I2C_NAME_SIZE];      /* I2C Device 的名称 */
    struct i2c_adapter *adapter;    /* 设备所连接的 I2C Adapter */
    struct device dev;             /* Linux 设备模型中的 device 对象 */
    int irq;                       /* 设备使用的中断号 */
    struct list_head detected;     /* 用于连接已探测到的 I2C Device */

#if IS_ENABLED(CONFIG_I2C_SLAVE)
    i2c_slave_cb_t slave_cb;       /* I2C 从机模式下的回调函数 */
#endif
};
```

当前阶段重点记住：

- addr：表示这个 I2C Device 的设备地址。
    
- adapter：表示这个设备连接在哪一个 I2C Controller 上。
    

例如设备地址为 0x50：

```text
i2c_client
    │
    ├── addr = 0x50
    │
    └── adapter ──→ 对应的 i2c_adapter
```

可以简单理解为：**i2c_client 表示一个 I2C Device。**

代码示例：

```c
struct i2c_client *client;

/* 假设 client 已经指向某个 I2C 设备 */

printk("device address = 0x%x\n", client->addr);
printk("I2C bus = %d\n", client->adapter->nr);
```

例如：

```c
client->addr = 0x50;
```

表示该 i2c_client 对应设备地址为 0x50 的 I2C Device。

而：

```c
client->adapter
```

则可以找到该设备所在的 I2C Adapter。
#### i2c_msg

i2c_msg 用来描述一次 I2C 数据传输，也就是告诉 I2C Controller：

- 要访问哪个 I2C 设备
    
- 本次是读还是写
    
- 要传输多少字节
    
- 数据保存在哪里
    

一个 i2c_msg **要么表示一次读操作，要么表示一次写操作**。

```c
#include <linux/i2c.h>

struct i2c_msg {
    __u16 addr;     /* I2C 设备地址 */

    __u16 flags;    /* 传输标志，主要用于指定读写方向 */

#define I2C_M_RD            0x0001  /* 读操作 */
#define I2C_M_TEN           0x0010  /* 使用 10 位设备地址 */
#define I2C_M_RECV_LEN      0x0400  /* 接收长度由从机返回的数据决定 */
#define I2C_M_NO_RD_ACK     0x0800  /* 读操作时不产生正常的 ACK */
#define I2C_M_IGNORE_NAK    0x1000  /* 忽略 NACK */
#define I2C_M_REV_DIR_ADDR  0x2000  /* 反转地址中的读写方向位 */
#define I2C_M_NOSTART       0x4000  /* 本次传输前不产生 START */
#define I2C_M_STOP          0x8000  /* 本次消息结束后产生 STOP */

    __u16 len;      /* 要发送或接收的数据字节数 */
    __u8 *buf;      /* 指向发送数据或接收数据的缓冲区 */
};
```

其中当前阶段最重要的是：

- addr：指定要访问的 I2C Device 地址。
    
- flags：指定本次传输是读还是写。
    
- len：指定要传输多少个字节。
    
- buf：指向实际的数据缓冲区。
    

flags 中最常用的是 I2C_M_RD：

```c
msg.flags = 0;          /* 写操作 */

msg.flags = I2C_M_RD;   /* 读操作 */
```

也就是：

```text
flags 的 bit0 = 0
        ↓
       写

flags 的 bit0 = I2C_M_RD
        ↓
       读
```

例如，要读取设备地址为 0x50 的 EEPROM 中存储地址 0x10 处的 1 个字节，需要构造两个 i2c_msg：

```c
u8 data_addr = 0x10;
i8 data;
struct i2c_msg msgs[2];

/* 第 1 个 i2c_msg：写入要访问的 EEPROM 存储地址 0x10 */
msgs[0].addr  = 0x50;          /* EEPROM 的设备地址 */
msgs[0].flags = 0;             /* 写操作 */
msgs[0].len   = 1;             /* 写 1 个字节 */
msgs[0].buf   = &data_addr;    /* 要发送的数据：0x10 */

/* 第 2 个 i2c_msg：从 EEPROM 读取 1 个字节 */
msgs[1].addr  = 0x50;          /* EEPROM 的设备地址 */
msgs[1].flags = I2C_M_RD;      /* 读操作 */
msgs[1].len   = 1;             /* 读 1 个字节 */
msgs[1].buf   = &data;         /* 读取到的数据保存到 data */
```

对应的传输过程可以理解为：

```text
msgs[0]：写

设备 0x50
   ↓
发送 0x10
   ↓
告诉 EEPROM：我要访问存储地址 0x10


msgs[1]：读

设备 0x50
   ↓
读取 1 Byte
   ↓
保存到 data
```

之所以需要两个 i2c_msg，是因为：

```text
第一个 i2c_msg
    ↓
写操作：发送存储地址 0x10

第二个 i2c_msg
    ↓
读操作：读取该地址中的数据
```

一个 i2c_msg 只能表示一个方向的传输，因此这种“先写地址、再读数据”的操作需要两个 i2c_msg。

可以简单理解为：

```text
i2c_msg
   │
   ├── addr   → 和哪个 I2C Device 通信
   ├── flags  → 读还是写
   ├── len    → 传多少字节
   └── buf    → 数据放在哪里
```

i2c_msg 主要表示：**一次具体的 I2C 读或写传输。**

#### i2c_rdwr_ioctl_data

i2c_rdwr_ioctl_data 用于在用户空间通过 ioctl + I2C_RDWR 进行普通 I2C 传输。

它本身不保存具体的数据，而是保存：

- 要传输的 i2c_msg 数组
    
- i2c_msg 的数量
    

课程中的普通 I2C 访问流程就是先构造一个或多个 i2c_msg，再通过 i2c_rdwr_ioctl_data 交给 ioctl(file, I2C_RDWR, &rdwr) 执行。

```c
#include <linux/i2c.h>
#include <linux/i2c-dev.h>

struct i2c_rdwr_ioctl_data {
    struct i2c_msg *msgs;    /* 指向要传输的 i2c_msg 数组 */
    __u32 nmsgs;             /* i2c_msg 的数量 */
};
```

其中：

```text
msgs
↓
指向一个或多个 i2c_msg

nmsgs
↓
表示 msgs 数组中有多少个 i2c_msg
```

例如：

```c
struct i2c_msg msgs[2];
struct i2c_rdwr_ioctl_data rdwr;

rdwr.msgs  = msgs;
rdwr.nmsgs = 2;
```

表示：

```text
rdwr
 │
 ├── msgs  ──→ msgs[0]
 │             msgs[1]
 │
 └── nmsgs = 2
```

构造完成后通常配合 I2C_RDWR 使用：

```c
ioctl(fd, I2C_RDWR, &rdwr);
```

例如读取设备地址为 0x50 的 EEPROM 中地址 0x10 处的 1 个字节：

```c
#include <linux/i2c.h>
#include <linux/i2c-dev.h>
#include <sys/ioctl.h>

unsigned char data_addr = 0x10;
unsigned char data;

struct i2c_msg msgs[2];
struct i2c_rdwr_ioctl_data rdwr;

/* 第 1 个 message：写入要访问的 EEPROM 存储地址 */
msgs[0].addr  = 0x50;
msgs[0].flags = 0;
msgs[0].len   = 1;
msgs[0].buf   = &data_addr;

/* 第 2 个 message：读取该地址中的 1 个字节 */
msgs[1].addr  = 0x50;
msgs[1].flags = I2C_M_RD;
msgs[1].len   = 1;
msgs[1].buf   = &data;

/* 把两个 i2c_msg 交给 i2c_rdwr_ioctl_data */
rdwr.msgs  = msgs;
rdwr.nmsgs = 2;

/* 执行这组 I2C 传输 */
ioctl(fd, I2C_RDWR, &rdwr);
```

对应关系：

```text
i2c_rdwr_ioctl_data
        │
        ├── msgs
        │     │
        │     ├── msgs[0] → 写：发送地址 0x10
        │     │
        │     └── msgs[1] → 读：读取 1 字节
        │
        └── nmsgs = 2
```

可以简单理解为：

```text
i2c_msg
↓
描述“一次读或一次写”

i2c_rdwr_ioctl_data
↓
把一个或多个 i2c_msg 组织起来

ioctl + I2C_RDWR
↓
执行整组 I2C 传输
```
### 7.9.3 函数
#### i2c_transfer

```c
/**
 * @brief  通过指定的 I2C Adapter 传输一个或多个 i2c_msg。
 *
 * @param  adap: 指向要使用的 i2c_adapter，即指定 I2C Bus。
 *
 * @param  msgs: 指向要传输的 i2c_msg 数组。
 *
 * @param  num: i2c_msg 的数量。
 *
 * @retval 正数: 成功执行的 i2c_msg 数量。
 *
 * @retval 负数: 传输失败，返回负的错误码。
 */
#include <linux/i2c.h>

int i2c_transfer(struct i2c_adapter *adap,
                 struct i2c_msg *msgs,
                 int num);
```

i2c_transfer 是 Linux **内核中的 I2C 函数**，主要供 I2C 驱动代码使用，普通用户空间 APP 不能直接调用它。

多个 i2c_msg 会作为一次组合传输执行，中间通常使用 Repeated START，最后才产生 STOP。

**用法示例：**
例如从地址为 0x50 的 EEPROM 中读取存储地址 0x10 的 1 个字节：

```c
u8 data_addr = 0x10;
u8 data;

struct i2c_msg msgs[2];

msgs[0].addr  = 0x50;
msgs[0].flags = 0;
msgs[0].len   = 1;
msgs[0].buf   = &data_addr;

msgs[1].addr  = 0x50;
msgs[1].flags = I2C_M_RD;
msgs[1].len   = 1;
msgs[1].buf   = &data;

ret = i2c_transfer(adapter, msgs, 2);
```

对应：

```text
msgs[0]
写 0x10
   ↓
告诉 EEPROM 要访问哪个存储地址

Repeated START

msgs[1]
读取 1 Byte
   ↓
保存到 data
```

成功时：

```c
ret == 2
```

表示两个 i2c_msg 都执行成功。
### 7.9.4 I2C 编程流程


# 8 第三方库与组件

## 8.1 FreeType 字体库

### 数据类型表

| 类型           | 代码中的变量 | 作用                                         |
| -------------- | ------------ | -------------------------------------------- |
| `FT_Library`   | `library`    | FreeType 字体库对象                          |
| `FT_Face`      | `face`       | 字体对象，表示打开的字体文件及其中的某个字体 |
| `FT_GlyphSlot` | `slot`       | 字形槽，用来保存当前加载的字形               |
| `FT_Vector`    | `pen`        | 二维向量，本代码准备作为字形平移量           |
| `FT_Bitmap`    | `bitmap`     | 字形渲染后生成的位图                         |
| `FT_Int`       | `i、j、p、q` | FreeType 定义的整数类型                      |

```
说明：
FT_Face 内部自带一个字形槽，可以通过 face->glyph 访问。

每次加载新字符时，字形槽中原来的内容会被新字符覆盖。
```

### 函数表

| 函数                 | 代码中的调用                                         | 作用                                             |
| -------------------- | ---------------------------------------------------- | ------------------------------------------------ |
| `FT_Init_FreeType`   | `FT_Init_FreeType(&library)`                         | 初始化 FreeType 字体库，得到字体库对象 `library` |
| `FT_New_Face`        | `FT_New_Face(library, argv[1], 0, &face)`            | 打开字体文件，创建字体对象 `face`                |
| `FT_Set_Pixel_Sizes` | `FT_Set_Pixel_Sizes(face, font_size, 0)`             | 设置后续加载字形时使用的字体像素大小             |
| `FT_Set_Transform`   | `FT_Set_Transform(face, 0, &pen)`                    | 设置字形的旋转、缩放或平移；当前代码中被注释     |
| `FT_Load_Char`       | `FT_Load_Char(face, chinese_str[0], FT_LOAD_RENDER)` | 加载指定字符，并将字形渲染成位图                 |

```text
说明：

FT_Init_FreeType：
必须先调用，用来初始化 FreeType 字体库。

FT_New_Face：
在字体库初始化后调用，用来打开指定字体文件。

FT_Set_Pixel_Sizes：
在加载字符前调用，用来设置字体显示大小。

FT_Set_Transform：
在加载字符前调用，用来设置字形变换。
当前代码中没有实际执行。

FT_Load_Char：
加载并渲染指定字符。
渲染结果保存在 face->glyph 中，
生成的位图可以通过 face->glyph->bitmap 访问。
```

### 各数据类型之间的关系

```
FT_Library : FreeType 字体库对象
    │
    │ 通过 FT_New_Face() 创建字体对象
    ▼
FT_Face : 字体对象，表示打开的字体文件中的一个字体
    │
    │ 通过 face->glyph 获取字形槽
    ▼
FT_GlyphSlot : 字形槽，保存当前加载字符的字形信息
    │
    │ 使用 FT_Load_Char(..., FT_LOAD_RENDER) 渲染字形
    │
    │ 通过 slot->bitmap 获取位图
    ▼
FT_Bitmap : 字形渲染后的像素位图
    │
    │ bitmap->width   位图宽度
    │ bitmap->rows    位图高度
    │ bitmap->buffer  位图像素数据
    ▼
draw_bitmap() : 用户自己编写的函数，遍历位图数据并绘制到 LCD


FT_Vector : 独立的二维向量类型
    │
    ├── pen.x：水平方向平移量
    └── pen.y：垂直方向平移量
    │
    └── 可作为 FT_Set_Transform() 的平移参数


FT_Int : FreeType 定义的整数类型
    │
    └── 用于坐标、循环变量、宽度和高度等普通整数数据
```

### 数据类型

#### face->glyph->bitmap

```
FT_Face 	  face;
FT_GlyphSlot  slot;
	
slot = face->glyph;
作用：取得 face 自带的字形槽，并让 slot 指向这个字形槽。

FT_GlyphSlot slot;
说明：字形槽用于保存当前加载字符的：字形图像,字形位图,字形尺寸,字形位置等信息

每次调用 FT_Load_Char 加载新字符后：slot 中原来的字形数据会被新字符的数据覆盖。
```

`FT_Bitmap` 在代码中使用的成员：

| 成员             | 作用                     |
| ---------------- | ------------------------ |
| `bitmap->width`  | 位图宽度，单位是像素     |
| `bitmap->rows`   | 位图高度，单位是像素行   |
| `bitmap->buffer` | 保存位图像素数据的缓冲区 |

#### FT_Library

```c
/**
 * @brief  FreeType 字体库对象。
 *
 *         FT_Library 是 FreeType 中最上层的对象，
 *         用来管理字体对象、字形对象、内存管理器等资源。
 *
 * 常用成员：
 *         FT_Library 是不透明指针类型，
 *         内部成员不对应用程序公开，不能直接访问。
 *
 * 创建方式：
 *         使用 FT_Init_FreeType() 创建。
 *
 * 代码中的变量：
 *         FT_Library library;
 *
 * 与其他类型的关系：
 *         FT_Library 可以用来创建一个或多个 FT_Face 字体对象。
 */
#include <ft2build.h>

typedef struct FT_LibraryRec_ *FT_Library;
```

代码中的使用：

```c
FT_Library library;

error = FT_Init_FreeType(&library);
```

```text
说明：

library：
保存初始化后的 FreeType 字体库对象。

后续调用 FT_New_Face 时，
需要把 library 作为参数传入。
```

---

#### FT_Face

```c
/**
 * @brief  字体对象。
 *
 *         FT_Face 表示字体文件中的一个字体及其样式。
 *         一个字体文件中可能包含一个或多个 FT_Face。
 *
 * 创建方式：
 *         使用 FT_New_Face() 创建。
 *
 * 代码中的变量：
 *         FT_Face face;
 *
 * 与其他类型的关系：
 *         FT_Face 由 FT_Library 创建。
 *         FT_Face 内部拥有一个 FT_GlyphSlot。
 */
#include <ft2build.h>

typedef struct FT_FaceRec_ *FT_Face;
```

代码中的使用：

```c
FT_Face face;

error = FT_New_Face(library, argv[1], 0, &face);
```

访问字形槽：

```c
slot = face->glyph;
```

```text
说明：

face：
表示 argv[1] 指定字体文件中的第一个字体对象。

face->glyph：
取得 face 内部自带的字形槽。
```

---

#### FT_GlyphSlot

```c
/**
 * @brief  字形槽。
 *
 *         FT_GlyphSlot 用来保存当前加载字符的字形数据。
 *
 *         每次调用 FT_Load_Char() 或 FT_Load_Glyph() 时，
 *         字形槽中原来的内容都会被新字形覆盖。
 *
 * 获取方式：
 *         通过 face->glyph 获取。
 *
 * 代码中的变量：
 *         FT_GlyphSlot slot;
 *
 * 与其他类型的关系：
 *         FT_GlyphSlot 属于 FT_Face。
 *         FT_GlyphSlot 内部包含 FT_Bitmap。
 */
typedef struct FT_GlyphSlotRec_ *FT_GlyphSlot;
```

代码中的使用：

```c
FT_GlyphSlot slot;

slot = face->glyph;
```

加载字符：

```c
error = FT_Load_Char(face,
                     chinese_str[0],
                     FT_LOAD_RENDER);
```

取得字形位图：

```c
slot->bitmap
```

```text
说明：

使用 FT_LOAD_RENDER 加载字符后，
渲染生成的位图会保存在 slot->bitmap 中。

slot 由 face 管理，
不需要应用程序单独创建或释放。
```

---

#### FT_Vector

```c
/**
 * @brief  二维向量。
 *
 *         FT_Vector 用来保存二维坐标、移动距离或平移量。
 *
 * 常用成员：
 *
 *         x	：水平方向的坐标或移动量。
 *
 *         y	：垂直方向的坐标或移动量。
 *
 * 代码中的变量：
 *         FT_Vector pen;
 *
 * 代码中的用途：
 *         准备用作 FT_Set_Transform() 的平移参数。
 */
#include <ft2build.h>

typedef struct FT_Vector_
{
    FT_Pos x;
    FT_Pos y;

} FT_Vector;
```

代码中的使用目前被注释：

```c
FT_Vector pen;

//pen.x = 0;
//pen.y = 0;

//FT_Set_Transform(face, 0, &pen);
```

```text
说明：

pen.x：
字形在水平方向上的平移量。

pen.y：
字形在垂直方向上的平移量。

当 FT_Vector 用作 FT_Set_Transform 的平移参数时，
x 和 y 通常使用 26.6 定点格式。

也就是：
64 表示移动 1 个像素。
32 表示移动 1/2 个像素。
```

---

#### FT_Bitmap

```c
/**
 * @brief  字形位图。
 *
 *         FT_Bitmap 用来保存字形渲染后得到的像素数据。
 *
 * 常用成员：
 *
 *         rows
 *              位图的行数，也就是位图高度。
 *
 *         width
 *              位图每行的像素数量，也就是位图宽度。
 *
 *         pitch
 *              位图每行数据实际占用的字节数。
 *
 *         buffer
 *              指向位图像素数据缓冲区。
 *
 *         num_grays
 *              灰度级数量。
 *
 *         pixel_mode
 *              位图像素格式。
 *              例如单色位图、灰度位图或 BGRA 位图。
 *
 *         palette_mode
 *              调色板模式，通常不使用。
 *
 *         palette
 *              调色板地址，通常不使用。
 *
 * 代码中的用途：
 *         接收 FT_Load_Char() 渲染后生成的字形位图。
 *
 * 与其他类型的关系：
 *         FT_Bitmap 是 FT_GlyphSlot 中的成员。
 *         可以通过 slot->bitmap 访问。
 */
#include <ft2build.h>

typedef struct FT_Bitmap_
{
    unsigned int   rows;
    unsigned int   width;
    int            pitch;
    unsigned char *buffer;
    unsigned short num_grays;
    unsigned char  pixel_mode;
    unsigned char  palette_mode;
    void          *palette;

} FT_Bitmap;
```

代码中的使用：

```c
void draw_bitmap(FT_Bitmap *bitmap,
                 FT_Int x,
                 FT_Int y);
```

取得位图宽度和高度：

```c
FT_Int x_max = x + bitmap->width;
FT_Int y_max = y + bitmap->rows;
```

读取像素数据：

```c
bitmap->buffer[q * bitmap->width + p]
```

```text
说明：

bitmap->width：
字形位图宽度。

bitmap->rows：
字形位图高度。

bitmap->buffer：
保存字形每个像素的灰度值。

bitmap->pitch：
位图一行实际占用的字节数。
在通用代码中，计算每行地址时应考虑 pitch。

当前代码使用：
q * bitmap->width + p

这相当于假设：
每个像素占 1 字节，
并且 pitch 等于 width。
```

#### FT_Matrix

`FT_Matrix` 是 FreeType 中的二维变换矩阵，用来对字形进行旋转、缩放、倾斜或镜像。

```
#include <ft2build.h>

typedef struct FT_Matrix_
{
    FT_Fixed xx;
    FT_Fixed xy;
    FT_Fixed yx;
    FT_Fixed yy;
} FT_Matrix;
```

矩阵形式：

```
┌         ┐
│ xx   xy │
│ yx   yy │
└         ┘
```

代码中的旋转矩阵：

```
matrix.xx = (FT_Fixed)( cos(angle) * 0x10000L);
matrix.xy = (FT_Fixed)(-sin(angle) * 0x10000L);
matrix.yx = (FT_Fixed)( sin(angle) * 0x10000L);
matrix.yy = (FT_Fixed)( cos(angle) * 0x10000L);
```

作用：把字形旋转 `angle` 对应的角度。

`FT_Fixed` 是 16.16 定点数：

```
1.0 = 0x10000
0.5 = 0x08000
2.0 = 0x20000
```

#### FT_BBox

`FT_BBox` 用来保存一个图形或字形的边界框，也就是能够包住该图形的最小矩形。

数据结构

```c
#include <ft2build.h>

typedef struct FT_BBox_
{
    FT_Pos xMin;
    FT_Pos yMin;
    FT_Pos xMax;
    FT_Pos yMax;
} FT_BBox;
```

成员说明

| 成员   | 说明                  |
| ------ | --------------------- |
| `xMin` | 边界框最左侧的 x 坐标 |
| `yMin` | 边界框最下方的 y 坐标 |
| `xMax` | 边界框最右侧的 x 坐标 |
| `yMax` | 边界框最上方的 y 坐标 |

```text
左下角坐标：(xMin, yMin)
右上角坐标：(xMax, yMax)
```

### 函数

#### FT_Init_FreeType

```
/**
 * @brief  初始化 FreeType 字体库。
 *
 * @param  alibrary：用于保存初始化后得到的 FreeType 字体库对象。
 *
 * @retval 0：初始化成功。
 * @retval 非0：初始化失败，返回 FreeType 错误码。
 */
FT_Error FT_Init_FreeType(FT_Library *alibrary);
```

#### FT_New_Face

```
/**
 * @brief  从指定字体文件中创建字体对象。
 *
 * @param  library：已经初始化的 FreeType 字体库对象。
 *
 * @param  filepathname：字体文件路径。
 *
 * @param  face_index：字体文件中的字体索引。
 *         0 表示使用第一个字体对象。
 *
 * @param  aface：用于保存创建后的 FT_Face 字体对象。
 *
 * @retval 0：创建成功。
 * @retval 非0：创建失败，返回 FreeType 错误码。
 */
#include <ft2build.h>
 
FT_Error FT_New_Face(FT_Library library,
                     const char *filepathname,
                     FT_Long face_index,
                     FT_Face *aface);
```

运行示例：

```
./程序名 font.ttf
说明：
argv[1] 就是 font.ttf。
```

#### FT_Set_Pixel_Sizes

```
/**
 * @brief  设置字体的像素大小。
 *
 * @param  face：要设置的字体对象。
 *
 * @param  pixel_width：字体的名义像素宽度。
 *
 * @param  pixel_height：字体的名义像素高度。
 *
 * @retval 0：设置成功。
 * @retval 非0：设置失败，返回 FreeType 错误码。
 */
FT_Error FT_Set_Pixel_Sizes(FT_Face face,
                            FT_UInt pixel_width,
                            FT_UInt pixel_height);
```

代码中的使用：

```
int font_size = 24;

FT_Set_Pixel_Sizes(face, font_size, 0);
参数说明：

face：
FT_New_Face 创建的字体对象。

font_size：
字体的像素宽度。
默认值为 24，也可以由 argv[2] 指定。

0：
像素高度设置为 0，
表示高度根据宽度自动确定。
```

运行示例：

```
./程序名 font.ttf 32
说明：

argv[1] 是字体文件路径。
argv[2] 是字体像素大小。

此时：
font_size = 32
注意：
FT_Set_Pixel_Sizes 设置的是字体的名义像素尺寸。

实际生成的单个字形位图，
不一定正好等于设置的宽度和高度。
```

#### FT_Set_Transform

```
/**
 * @brief  设置加载字形时使用的变换矩阵和平移量。
 *
 * @param  face：要设置的字体对象。
 *
 * @param  matrix：二维变换矩阵。
 *         NULL 表示不进行旋转、缩放等矩阵变换。
 *
 * @param  delta：平移向量。
 *         NULL 表示不进行平移。
 *
 * @retval 无。
 */
#include <ft2build.h>
 
void FT_Set_Transform(FT_Face face,
                      FT_Matrix *matrix,
                      FT_Vector *delta);
```

代码中的使用

```
FT_Vector pen;

pen.x = 0;
pen.y = 0;

FT_Set_Transform(face, &matrix, &pen);

含义：

- 使用 matrix 旋转字形；
- pen.x 和 pen.y`都为 0，因此不进行平移。

FT_Set_Transform() 只是保存变换规则，真正的变换发生在后面加载字形时：

FT_Set_Transform(face, &matrix, &pen);

FT_Load_Char(face,
             chinese_str[0],
             FT_LOAD_RENDER);
```

执行过程：

```
设置旋转矩阵
    ↓
FT_Set_Transform() 保存变换规则
    ↓
FT_Load_Char() 加载字形
    ↓
旋转字形轮廓
    ↓
生成旋转后的位图
```

常见写法

```
/* 只旋转，不平移 */
FT_Set_Transform(face, &matrix, NULL);

/* 不旋转，只平移 */
FT_Set_Transform(face, NULL, &pen);

/* 不进行任何变换 */
FT_Set_Transform(face, NULL, NULL);
```

#### FT_Load_Char

```
/**
 * @brief  根据字符编码加载字形，并保存到 face 的字形槽中。
 *
 * @param  face：字体对象。
 *
 * @param  char_code：要加载字符的字符编码。
 *
 * @param  load_flags：字形加载方式。
 *
 *         @arg FT_LOAD_RENDER
 *              加载字形后立即把字形渲染成位图。
 *
 * @retval 0：加载成功。
 * @retval 非0：加载失败，返回 FreeType 错误码。
 */
#include <ft2build.h>
 
FT_Error FT_Load_Char(FT_Face face,
                      FT_ULong char_code,
                      FT_Int32 load_flags);
```

代码中的使用：

```
wchar_t *chinese_str = L"繁";

error = FT_Load_Char(face,
                     chinese_str[0],
                     FT_LOAD_RENDER);
参数说明：

face：
FT_New_Face 创建的字体对象。

chinese_str[0]：
宽字符字符串中的第一个字符，
这里表示汉字“繁”的字符编码。

FT_LOAD_RENDER：
加载字形后立即渲染成位图。
```

### 代码执行流程

```
1. FT_Init_FreeType
   初始化 FreeType 字体库，得到 library。

2. FT_New_Face
   打开字体文件，得到 face。

3. face->glyph
   取得 face 自带的字形槽，保存到 slot。

4. FT_Set_Pixel_Sizes
   设置字体像素大小。

5. FT_Set_Transform
   设置字形变换和平移。
   当前代码中被注释，没有实际执行。

6. FT_Load_Char
   加载“繁”字并渲染成位图。

7. slot->bitmap
   取得渲染完成的字形位图。

8. draw_bitmap
   把字形位图逐像素绘制到 LCD。
简单记忆：

library：
FreeType 字体库对象。

face：
从字体文件创建的字体对象。

slot：
保存当前字形的字形槽。

bitmap：
字形渲染后得到的像素位图。
```
## 8.2 tslib 触摸屏
### 8.2.1 命令

#### `ts_print`

```
在终端中持续打印触摸坐标和压力值：

适合检查触摸屏是否能够正常读取数据。
```

#### `ts_print_raw`

```
打印未经校准和过滤的原始触摸数据：

适合检查驱动层是否能够产生原始触摸数据。
```

#### `ts_calibrate`

```text
执行触摸屏坐标校准：
校准完成后，通常会把参数保存到：
/etc/pointercal
```

#### `ts_test`

```
运行单点触摸测试程序：

可以通过图形界面测试画线、拖动等触摸操作。
```

#### `ts_test_mt`

```
运行多点触摸测试程序：

适合测试支持多点触摸的触摸屏设备。
```

---
### 8.2.2 宏

多点触摸（Multi-Touch）绝对事件代码，用于表示触点槽位、位置、压力、接触面积等信息。

```c
#include <linux/input-event-codes.h>

#define ABS_MT_SLOT         0x2f   /* 当前正在修改的触摸槽位 */

#define ABS_MT_TOUCH_MAJOR  0x30   /* 触摸区域椭圆的主轴大小 */
#define ABS_MT_TOUCH_MINOR  0x31   /* 触摸区域椭圆的次轴大小，圆形时可省略 */

#define ABS_MT_WIDTH_MAJOR  0x32   /* 接近触摸面的工具区域主轴大小 */
#define ABS_MT_WIDTH_MINOR  0x33   /* 接近触摸面的工具区域次轴大小 */

#define ABS_MT_ORIENTATION  0x34   /* 触摸椭圆的方向 */

#define ABS_MT_POSITION_X   0x35   /* 触摸点中心的 X 坐标 */
#define ABS_MT_POSITION_Y   0x36   /* 触摸点中心的 Y 坐标 */

#define ABS_MT_TOOL_TYPE    0x37   /* 触摸工具类型 */
#define ABS_MT_BLOB_ID      0x38   /* 一组相关触摸数据的编号 */
#define ABS_MT_TRACKING_ID  0x39   /* 一次触摸接触的唯一跟踪编号 */

#define ABS_MT_PRESSURE     0x3a   /* 触摸压力 */
#define ABS_MT_DISTANCE     0x3b   /* 触摸工具与表面的悬停距离 */

#define ABS_MT_TOOL_X       0x3c   /* 触摸工具中心的 X 坐标 */
#define ABS_MT_TOOL_Y       0x3d   /* 触摸工具中心的 Y 坐标 */
```
### 8.2.3 数据类型

#### struct tsdev

`struct tsdev` 表示一个由 tslib 管理的触摸屏设备。

它属于**不透明结构体**：`tslib.h` 中只声明了这个结构体，没有公开它的内部成员。因此，应用程序不能直接访问其内部成员，只能通过 `ts_setup()`、`ts_fd()`、`ts_read_mt()`、`ts_close()` 等 tslib 函数操作它。

```c
/**
 * @brief tslib 触摸屏设备对象。
 *
 * struct tsdev 的内部成员没有在 tslib.h 中公开。
 * 程序一般只声明 struct tsdev 指针。
 *
 * 必需头文件：
 * #include <tslib.h>
 */

#include <tslib.h>

/* tslib.h 中的结构体声明 */
struct tsdev;

/* 常用的变量声明形式 */
struct tsdev *ts;
```

代码示例：

```c
/* ts_setup() 成功后，ts 指向一个 tslib 触摸屏设备对象 */
struct tsdev *ts = ts_setup(NULL, 0);

if (ts != NULL) {
    /* 此处可以使用 ts 调用其他 tslib 函数 */

    ts_close(ts);
}
```

---

#### struct ts_sample_mt

| 成员            | 在源文件中的作用          |
| ------------- | ----------------- |
| `x`           | 保存触点的 X 坐标        |
| `y`           | 保存触点的 Y 坐标        |
| `tracking_id` | 源文件通过它判断槽位中是否存在触点 |
| `valid`       | 判断本次读取是否包含该槽位的新数据 |

```c
/**
 * @brief 保存一个多点触摸槽位的采样数据，
		  例如坐标、压力、槽位编号、触点跟踪编号和数据是否有效。
 *
 * 必需头文件：
 * #include <tslib.h>
 */

#include <tslib.h>

struct ts_sample_mt {
    int x;                       /* X 坐标 */
    int y;                       /* Y 坐标 */
    unsigned int pressure;       /* 压力值 */

    int slot;                    /* 触摸槽位编号 */
    int tracking_id;             /* 触点跟踪编号 非0：有触点；0：触点结束/抬起 */
    int tool_type;               /* 触摸工具类型 */

    int tool_x;                  /* 触摸工具的 X 坐标 */
    int tool_y;                  /* 触摸工具的 Y 坐标 */

    unsigned int touch_major;    /* 触摸区域主轴大小 */
    unsigned int width_major;    /* 触摸工具主轴宽度 */
    unsigned int touch_minor;    /* 触摸区域次轴大小 */
    unsigned int width_minor;    /* 触摸工具次轴宽度 */

    int orientation;             /* 触摸区域方向 */
    int distance;                /* 工具与触摸表面的距离 */
    int blob_id;                 /* 触点集合编号 */

    struct timeval tv;           /* 事件时间 */

    short pen_down;              /* BTN_TOUCH 状态 通常：1按下，0松开 */
    short valid;                 /* 本次采样是否包含新数据 非0：有新数据；0：本次没更新 */
};
```

代码示例：

```c
/* 定义并初始化一个多点触摸采样数据 */
struct ts_sample_mt point = {0};

/* 设置当前触点的数据 */
point.x = 629;
point.y = 364;
point.tracking_id = 10;
point.valid = 1;

/* 数据有效并且当前槽位中存在触点时，读取坐标 */
if (point.valid && point.tracking_id != -1) {
    int x = point.x;
    int y = point.y;
}
```

### 8.2.4 函数

#### ts_setup()

```c
/**
 * @brief 寻找、打开并配置触摸屏设备。
 *
 * @param dev_name 触摸屏设备路径。
 *                 传入 NULL 时，由 tslib 查找触摸设备。
 *
 * @param nonblock 是否使用非阻塞方式。
 *                 0：阻塞方式。
 *                 非 0：非阻塞方式。
 *
 * @return 成功：返回 struct tsdev 指针。
 * @return 失败：返回 NULL。
 *
 * 必需头文件：
 * #include <tslib.h>
 */

#include <tslib.h>

struct tsdev *ts_setup(const char *dev_name, int nonblock);
```

代码示例：

```c
/* NULL：由 tslib 查找设备；0：使用阻塞方式 */
struct tsdev *ts = ts_setup(NULL, 0);

if (ts == NULL) {
    /* 触摸屏设备打开或配置失败 */
}
```

---

#### ts_fd()

```c
/**
 * @brief 获取 tslib 当前使用的触摸屏设备文件描述符。
 *
 * @param ts 有效的 tslib 触摸屏设备指针。
 *
 * @return 返回触摸屏设备的文件描述符。
 *
 * 必需头文件：
 * #include <tslib.h>
 */

#include <tslib.h>

int ts_fd(struct tsdev *ts);
```

代码示例：

```c
/* 必须先获得一个有效的 tslib 设备 */
struct tsdev *ts = ts_setup(NULL, 0);

if (ts != NULL) {
    int fd = ts_fd(ts);

    /* 此处可以把 fd 传给 ioctl() 等系统调用 */

    ts_close(ts);
}
```

---

#### ts_read_mt()

```c
/**
 * @brief 读取经过 tslib 处理的多点触摸数据。
 *
 * @param ts    有效的 tslib 触摸屏设备指针。
 * @param samp  保存读取结果的二维数据空间。
 * @param slots 每组数据包含的最大触摸槽位数。
 * @param nr    希望读取的采样组数。
 *
 * @return 成功：返回实际读取到的采样组数。
 * @return 失败：返回负数。
 *
 * 必需头文件：
 * #include <tslib.h>
 */

#include <tslib.h>

int ts_read_mt(struct tsdev *ts,
               struct ts_sample_mt **samp,
               int slots,
               int nr);
```

代码示例：

```c
/************************** 读一组数据 **************************/
struct ts_sample_mt **samp_mt;
int max_slots = 5;

samp_mt = malloc(sizeof(*samp_mt));
samp_mt[0] = calloc(max_slots, sizeof(**samp_mt));


if (samp_mt != NULL && samp_mt[0] != NULL) {
    int ret = ts_read_mt(ts, samp_mt, max_slots, 1);
}

/************************** 读多组数据 **************************/
int nr = 2;
int i;

struct ts_sample_mt **samp_mt;

samp_mt = malloc(nr * sizeof(*samp_mt));

for (i = 0; i < nr; i++) {
    samp_mt[i] = calloc(max_slots, sizeof(**samp_mt));
}

if (samp_mt != NULL && samp_mt[0] != NULL) {
    int ret = ts_read_mt(ts, samp_mt, max_slots, 1);
}
```

---

#### ts_close()

```c
/**
 * @brief 关闭触摸屏设备并释放相关资源。
 *
 * @param ts 有效的 tslib 触摸屏设备指针。
 *
 * @return 0：关闭成功。
 * @return 负数：关闭失败。
 *
 * 必需头文件：
 * #include <tslib.h>
 */

#include <tslib.h>

int ts_close(struct tsdev *ts);
```

代码示例：

```c
/* 必须先打开并配置触摸屏设备 */
struct tsdev *ts = ts_setup(NULL, 0);

if (ts != NULL) {
    /* 触摸屏使用完毕后再关闭 */
    int ret = ts_close(ts);

    if (ret < 0) {
        /* 关闭触摸屏设备失败 */
    }
}
```

## 8.3 i2c-tools

### 介绍

i2c-tools 是 Linux 用户空间中用于访问和调试 I2C 设备的一套工具，同时也提供 libi2c 编程接口。

它主要包含两类内容：

- 命令行工具：i2cdetect、i2cget、i2cset、i2cdump、i2ctransfer 等。
    
- libi2c 编程接口：提供一系列 i2c_smbus_*() 函数，可在应用程序中通过 SMBus 方式访问 I2C 设备。
    

Linux 中通常通过 `/dev/i2c-0`、`/dev/i2c-1` 等设备节点访问不同的 I2C Bus。

Ubuntu / Debian 可以安装：

```bash
sudo apt install i2c-tools
```

查看当前安装的版本：

```bash
i2cdetect -V
```

源码版本可以从 i2c-tools 官方源码包获取并自行编译。

### 命令行工具
#### i2cdetect：I2C 检测

i2cdetect 用于查看系统中的 I2C Bus、查询 I2C Bus 支持的功能以及扫描总线上的 I2C 设备。

|命令|选项|参数|
|---|---|---|
|i2cdetect|-l -F -y -a|I2CBUS|

```bash
-l：列出当前系统中的 I2C Adapter / I2C Bus / I2C Controller

-F：查看指定 I2C Bus 支持的功能
    I2CBUS 为 0、1、2 等总线编号

-y：执行命令时不再询问确认，直接执行

-a：扫描全部 I2C 地址，包括默认不会扫描的保留地址

扫描结果：

--：该地址没有检测到 I2C 设备

UU：该地址存在 I2C 设备，并且已经被内核驱动占用

数值：
例如 1e，表示地址 0x1e 上检测到了 I2C 设备，
但没有被对应的内核设备驱动占用


example

# 查看当前系统中有哪些 I2C Bus
i2cdetect -l

# 查看 I2C Bus 0 支持哪些功能
i2cdetect -F 0

# 扫描 I2C Bus 0 上有哪些设备
i2cdetect -y -a 0
```
#### i2cget：读取 I2C 数据

i2cget 用于从 I2C / SMBus 设备读取数据或寄存器内容。

| 命令     | 选项       | 参数                                                 |
| ------ | -------- | -------------------------------------------------- |
| i2cget | -f -y -a | I2CBUS CHIP-ADDRESS [DATA-ADDRESS [MODE [LENGTH]]] |

```text
-f：强制访问，即使该设备已经被内核驱动占用

-y：取消执行前的确认提示，直接执行

-a：允许访问保留地址范围


I2CBUS：
I2C Bus 编号，例如 0、1、2

CHIP-ADDRESS：
I2C 设备地址

DATA-ADDRESS：
芯片内部寄存器地址 / Command

MODE：

b：Read Byte Data，读取 1 字节，默认

w：Read Word Data，读取 2 字节

c：先 Write Byte，再 Receive Byte

s：SMBus Block Read

i：I2C Block Read

p：
追加到模式后表示启用 SMBus PEC，例如 bp、wp

LENGTH：
Block Read 时指定读取长度，范围通常为 1～32
```

example：

```bash
# 从 I2C Bus 1、设备 0x2d 的寄存器 0x11 读取 1 字节
i2cget -y 1 0x2d 0x11

# 从寄存器 0x00 读取一个 16 bit Word
i2cget -y 1 0x48 0x00 w

# 从设备 0x50 的 0x00 开始读取 8 字节
i2cget -y 4 0x50 0x00 i 8
```

---

#### i2cset：写入 I2C 数据

i2cset 用于向 I2C / SMBus 设备的寄存器写入数据。

| 命令     | 选项             | 参数                                                  |
| ------ | -------------- | --------------------------------------------------- |
| i2cset | -f -y -m -r -a | I2CBUS CHIP-ADDRESS DATA-ADDRESS [VALUE] ... [MODE] |

```text
-f：强制访问已被内核驱动占用的设备

-y：取消执行前确认

-m MASK：
只修改 MASK 中为 1 的位，其余位保持原值

-r：
写入完成后重新读取并检查结果

-a：
允许访问保留地址范围


I2CBUS：
I2C Bus 编号

CHIP-ADDRESS：
I2C 设备地址

DATA-ADDRESS：
芯片内部寄存器地址 / Command

VALUE：
要写入的数据


MODE：

c：只发送 DATA-ADDRESS，不发送 VALUE

b：写 1 字节，默认

w：写 16 bit Word

s：SMBus Block Write

i：I2C Block Write

p：
追加到模式后启用 PEC
```

example：

```bash
# 给设备 0x2d 的寄存器 0x11 写入 0x42
i2cset -y 1 0x2d 0x11 0x42

# 写入一个 16 bit 数据
i2cset -y 1 0x48 0x02 0x5000 w

# 只发送寄存器地址，不发送数据
i2cset -y 0 0x50 0x10
```

---

#### i2cdump：查看 I2C 寄存器内容

i2cdump 用于一次查看一个 I2C 设备的一段或全部寄存器内容。

|命令|选项|参数|
|---|---|---|
|i2cdump|-f -r -y -a|I2CBUS ADDRESS [MODE]|

```text
-f：强制访问已被内核驱动占用的设备

-r FIRST-LAST：
只读取指定寄存器范围

-y：
取消执行前确认

-a：
允许访问保留地址


MODE：

b：按 Byte 读取，默认

w：按 16 bit Word 读取

i：使用 I2C Block Read

c：连续读取，适合支持地址自动递增的设备

W：类似 w，但只在偶数寄存器地址发出读命令
```

example：

```bash
# 查看 Bus 9 上地址 0x50 设备的寄存器
i2cdump 9 0x50

# 不询问，使用 I2C Block Read
i2cdump -y 9 0x50 i

# 只查看寄存器 0x00～0x3f
i2cdump -r 0x00-0x3f 1 0x2d
```

不要对未知设备地址随意执行 i2cdump，某些读取方式可能被特殊设备解释为写操作。

---

#### i2ctransfer：组合 I2C 传输

i2ctransfer 用于自己构造一个或多个 I2C Message，并把它们组合成一次 I2C Transfer。

它使用普通 I2C 传输，不是 SMBus 固定格式。

|命令|选项|参数|
|---|---|---|
|i2ctransfer|-a -b -f -v -y|I2CBUS DESC [DATA] ...|

DESC 格式：

```text
{r|w}LENGTH[@ADDRESS]
```

含义：

```text
r：读

w：写

LENGTH：
本条 message 传输的字节数

@ADDRESS：
I2C 设备地址
后续 message 地址不变时可以省略
```

例如：

```text
w1@0x50

w：
写操作

1：
写 1 字节

@0x50：
设备地址为 0x50
```

example：

```bash
# 向 EEPROM 0x50 写入地址 0x64，然后读取 8 字节
i2ctransfer -y 0 w1@0x50 0x64 r8

# 向设备 0x1e 的寄存器 0 写入 0x04
i2ctransfer -y 0 w2@0x1e 0x00 0x04

# 指定寄存器 0x0c 后连续读取 2 字节
i2ctransfer -y 0 w1@0x1e 0x0c r2
```

一次包含多个 DESC 时：

```text
START
 ↓
第一个 Message
 ↓
Repeated START
 ↓
第二个 Message
 ↓
STOP
```

---

libi2c 的 SMBus 函数在用户空间使用，通常需要：

```c
#include <linux/i2c-dev.h>
#include <i2c/smbus.h>
```

编译时链接 libi2c：

```bash
gcc test.c -li2c -o test
```

使用这些函数之前，一般先：

```c
int fd;

fd = open("/dev/i2c-0", O_RDWR);

ioctl(fd, I2C_SLAVE, 0x50);
```

之后所有 i2c_smbus_() 操作都针对这个 fd 当前指定的从设备。

### 函数
#### open_i2c_dev

```c
/**
 * @brief  根据 I2C Bus 编号打开对应的 I2C 设备节点。
 *
 * @param  i2cbus: I2C Bus 编号，例如 0 表示 I2C Bus 0。
 *
 * @param  filename: 用于保存打开的 I2C 设备节点路径。
 *
 * @param  size: filename 缓冲区的大小。
 *
 * @param  quiet: 是否禁止输出打开失败时的错误信息。
 *                0 表示输出错误信息，非 0 表示不输出。
 *
 * @retval >=0: 打开成功，返回 I2C 设备的文件描述符。
 *
 * @retval -1: 打开 I2C 设备失败。
 *
 * @retval -EOVERFLOW: filename 缓冲区太小，设备节点路径被截断。
 */
#include "i2cbusses.h"

int open_i2c_dev(int i2cbus, char *filename,
                 size_t size, int quiet);
```

open_i2c_dev() 是 i2c-tools 自己封装的辅助函数，不是 Linux 系统调用。

函数会根据 i2cbus 构造对应的 I2C 设备节点，并调用 open() 以读写方式打开。

会依次尝试类似下面的设备节点：

```text
/dev/i2c/0
/dev/i2c-0
```

代码示例：

```c
char filename[20];
int fd;

fd = open_i2c_dev(0, filename, sizeof(filename), 0);

if (fd < 0)
{
    printf("open i2c device failed\n");
    return -1;
}
```

说明：

```text
0：
表示打开 I2C Bus 0。

filename：
函数执行后保存实际使用的设备节点路径，
例如 /dev/i2c-0。

sizeof(filename)：
告诉函数 filename 缓冲区有多大。

0：
quiet = 0，打开失败时允许输出错误信息。

fd：
打开成功后保存 I2C 设备文件描述符，
后续可以使用 ioctl() 等接口访问 I2C 设备。
```

#### set_slave_addr

```c
/**
 * @brief  为已经打开的 I2C 设备文件设置要访问的从设备地址。
 *
 * @param  file: I2C 设备文件描述符，通常由 open_i2c_dev() 返回。
 *
 * @param  address: 要访问的 I2C 从设备地址，例如 0x50。
 *
 * @param  force: 是否强制设置从设备地址。
 *                0：使用 I2C_SLAVE。
 *                非0：使用 I2C_SLAVE_FORCE，即使设备已被内核驱动占用也强制访问。
 *
 * @retval 0: 设置成功。
 *
 * @retval 负数: 设置失败，返回对应 errno 的负值。
 */
#include "i2cbusses.h"

int set_slave_addr(int file, int address, int force);
```

set_slave_addr() 是 i2c-tools 自己封装的辅助函数，内部通过 ioctl() 配合 I2C_SLAVE 或 I2C_SLAVE_FORCE 设置当前要访问的 I2C 从设备地址。

代码示例：

```c
char filename[20];
int fd;
int ret;

fd = open_i2c_dev(0, filename, sizeof(filename), 0);
if (fd < 0)
{
    return -1;
}

/* 设置要访问的从设备地址为 0x50，不强制访问 */
ret = set_slave_addr(fd, 0x50, 0);
if (ret < 0)
{
    return -1;
}
```

说明：

```text
fd：
表示已经打开的 I2C Bus。

0x50：
表示后续要访问设备地址为 0x50 的 I2C 从设备。

force = 0：
正常设置从设备地址。

force != 0：
强制设置从设备地址。
```

#### i2c_smbus_write_byte_data

```c
/**
 * @brief  使用 SMBus Write Byte Data 方式，向 I2C 从设备写入 1 字节数据。
 *
 * @param  file: 已打开的 I2C 设备文件描述符。
 *
 * @param  command: SMBus Command 字节。
 *                  对于很多寄存器型 I2C 设备，通常可以理解为寄存器地址。
 *
 * @param  value: 要写入的 1 字节数据。
 *
 * @retval 0: 写入成功。
 *
 * @retval -1: 写入失败，并设置 errno。
 *
 * @note   当该函数用于向 AT24C02 写数据时，函数返回后 AT24C02 还需要进行
 *         EEPROM 内部写操作，内部写周期 tWR 最大为 10 ms。
 *         简单处理时可在写成功后延时 10 ms，再进行下一次读写；
 *         也可以通过 ACK Polling 判断内部写操作是否已经完成。
 *
 *         这里的 10 ms 是 AT24C02 芯片本身的要求，
 *         不是 i2c_smbus_write_byte_data() 函数本身要求的延时时间。
 */
#include <i2c/smbus.h>

__s32 i2c_smbus_write_byte_data(int file,
                                __u8 command,
                                __u8 value);
```

i2c_smbus_write_byte_data() 是 i2c-tools 中 libi2c 提供的用户空间库函数，不是 Linux 系统调用，也不是 Linux 内核函数。

使用该函数前，通常需要先打开 `/dev/i2c-X`，并通过 I2C_SLAVE 或 I2C_SLAVE_FORCE 设置要访问的从设备地址。

调用：

```c
i2c_smbus_write_byte_data(fd, 0x00, 0x03);
```

可以理解为：

```text
Command = 0x00
Data    = 0x03
```

对于将 Command 作为寄存器地址使用的设备，相当于：

```text
向 0x00 寄存器写入 0x03
```

对应的 SMBus Write Byte Data 传输格式可以简单理解为：

```text
START
  ↓
Slave Address + Write
  ↓
ACK
  ↓
Command
  ↓
ACK
  ↓
Data
  ↓
ACK
  ↓
STOP
```

代码示例：

```c
int ret;

/* 向当前选择的 I2C 从设备的 0x00 寄存器写入 0x03 */
ret = i2c_smbus_write_byte_data(fd, 0x00, 0x03);

if (ret < 0)
{
    perror("i2c_smbus_write_byte_data");
    return -1;
}
```

使用 libi2c 时，编译链接通常需要添加：

```bash
-li2c
```

例如：

```bash
gcc test.c -o test -li2c
```

内部调用关系可以简单理解为：

```text
i2c_smbus_write_byte_data()
        ↓
i2c_smbus_access()
        ↓
ioctl(file, I2C_SMBUS, ...)
        ↓
Linux i2c-dev
        ↓
I2C 控制器驱动
        ↓
I2C 从设备
```

#### i2c_smbus_read_i2c_block_data

```c
/**
 * @brief  使用 SMBus I2C Block Read 方式，从 I2C 从设备连续读取多个字节的数据。
 *
 * @param  file: 已打开的 I2C 设备文件描述符。
 *
 * @param  command: SMBus Command 字节。
 *                  对于很多寄存器型设备，通常可以理解为起始寄存器地址。
 *
 * @param  length: 希望读取的数据长度，最大为 32 字节。
 *
 * @param  values: 用于保存读取数据的缓冲区。
 *
 * @retval >0: 读取成功，返回实际读取到的字节数。
 *
 * @retval <0: 读取失败。
 */
#include <i2c/smbus.h>

__s32 i2c_smbus_read_i2c_block_data(int file,
                                    __u8 command,
                                    __u8 length,
                                    __u8 *values);
```

i2c_smbus_read_i2c_block_data() 是 i2c-tools 中 libi2c 提供的用户空间库函数，用于从指定 Command 开始连续读取多个字节。

这里的 I2C Block Read 和 SMBus Block Read 不完全相同：读取多少字节由主机通过 length 指定，而不是由从设备返回长度。

对于把 Command 当作寄存器地址使用的设备：

```c
i2c_smbus_read_i2c_block_data(fd, 0x0C, 2, buf);
```

可以简单理解为：

```text
从 0x0C 开始连续读取 2 字节数据
        ↓
buf[0] ← 第 1 个字节
buf[1] ← 第 2 个字节
```

代码示例：

```c
__u8 buf[2];
int ret;

ret = i2c_smbus_read_i2c_block_data(fd, 0x0C, 2, buf);

if (ret < 0)
{
    perror("i2c_smbus_read_i2c_block_data");
    return -1;
}
```
# 9 Linux 驱动开发

## 9.1 写驱动设备流程

记录字符设备驱动源码从准备、实现文件操作，到注册设备、释放资源以及指定模块入口和出口的基本编写顺序。

```
开始编写字符设备驱动
        ↓
① 基础准备
   ├── 包含内核头文件
   └── 定义 major、缓冲区、class 等
        ↓
② 实现文件操作
   ├── open / read / write / release
   └── 填入 struct file_operations
        ↓
③ 初始化并注册设备
   ├── register_chrdev()   注册字符设备
   ├── class_create()      创建 class
   └── device_create()     创建设备
        ↓
④ 退出并释放资源
   ├── device_destroy()
   ├── class_destroy()
   └── unregister_chrdev()
        ↓
⑤ 指定模块入口和出口
   ├── module_init()
   ├── module_exit()
   └── MODULE_LICENSE()
        ↓
驱动源码完成

```

## 9.2 内核基础

整理驱动开发中最基础的内核模块、初始化与退出标记以及内核日志相关内容。

### 宏

#### THIS_MODULE

```c
#include <linux/module.h>

THIS_MODULE

```

THIS\_MODULE 表示当前内核模块。

在可加载内核模块中，它是指向当前模块对应 struct module 的指针。

常用于告诉内核某个对象属于当前模块。

```c
#include <linux/fs.h>
#include <linux/module.h>

static const struct file_operations demo_fops = {
    .owner = THIS_MODULE,
};

```

这里把 demo\_fops 的 owner 设置为 THIS\_MODULE，表示这组文件操作属于当前内核模块。

#### MODULE\_LICENSE

```c
#include <linux/module.h>

MODULE_LICENSE("GPL");

```

MODULE\_LICENSE 用于声明内核模块的许可证信息。

例如：

```c
MODULE_LICENSE("GPL");

```

表示该模块声明使用 GPL 许可证。

它属于模块信息声明宏，不是函数。

#### `__init`、`__exit`

```c
#include <linux/init.h>

#define __init ...
#define __exit ...

/* 使用形式 */
static int __init func_init(void);
static void __exit func_exit(void);

```

`__init`：标记初始化阶段使用的函数，使函数代码被放入内核专门的初始化代码段。

`__exit`：标记退出阶段使用的函数，使函数代码被放入内核专门的退出代码段。

例如：

```c
static int driver_ready;

static int __init demo_init(void)
{
    driver_ready = 1;
    return 0;
}

static void __exit demo_exit(void)
{
    driver_ready = 0;
}

```

这里的 demo\_init 被标记为初始化函数代码，demo\_exit 被标记为退出函数代码。

它们属于 Linux 内核的修饰宏，不是函数。

### 函数

#### module_init

```c
/**
 * @brief  指定内核模块的初始化入口函数。
 *
 * @param  initfn: 模块初始化函数，函数形式通常为 int func(void)。
 *
 * @retval 无: module_init 本身是函数式宏，没有供调用者接收的返回值。
 */
#include <linux/module.h>

module_init(initfn);

```

类型：函数式宏。

当模块被加载时，内核会执行 module\_init 指定的初始化函数。

```c
static int __init demo_init(void)
{
    /* 在这里完成驱动初始化工作 */
    return 0;
}

module_init(demo_init);

```

这里先真正定义了 demo\_init，然后通过 module\_init 把它指定为模块初始化入口。

#### module_exit

```c
/**
 * @brief  指定内核模块的退出函数。
 *
 * @param  exitfn: 模块退出函数，函数形式通常为 void func(void)。
 *
 * @retval 无: module_exit 本身是函数式宏，没有供调用者接收的返回值。
 */
#include <linux/module.h>

module_exit(exitfn);

```

类型：函数式宏。

卸载可加载模块时，内核会执行 module\_exit 指定的退出函数。

```c
static void __exit demo_exit(void)
{
    /* 在这里释放驱动占用的资源 */
}

module_exit(demo_exit);

```

这里先真正定义了 demo\_exit，然后通过 module\_exit 把它指定为模块退出入口。

#### printk

```c
/**
 * @brief  向 Linux 内核日志缓冲区输出格式化信息。
 *
 * @param  fmt: 格式字符串，使用方式与 printf 的格式字符串类似。
 *
 * @param  ...: 与格式字符串对应的可变参数。
 *
 * @retval 返回实际输出的字符数量。
 */
#include <linux/printk.h>

int printk(const char *fmt, ...);

```

printk 是内核空间使用的日志输出函数，不是用户空间的 printf。

```c
int major = 100;

printk("hello: major = %d\n", major);

```

这段代码中 major 已明确赋值为 100，因此日志中会输出类似：

```text
hello: major = 100

```

内核日志可以通过 dmesg 等方式查看。

## 9.3 内核通用机制

整理与具体设备类型无关、在不同驱动中都可能使用的通用内核机制，例如用户空间与内核空间的数据交互和错误处理。

### 宏

#### `__user`

```c
#include <linux/compiler.h>

/* 使用形式 */
char __user *buf;
const char __user *buf;

```

`__user` 用于标记一个指针指向的是用户空间地址。

例如驱动的 read 回调：

```c
static ssize_t demo_read(struct file *file,
                         char __user *buf,
                         size_t size,
                         loff_t *offset)
{
    /*
     * buf 由内核传给驱动，
     * 它指向调用 read() 的用户程序提供的缓冲区。
     */
    return 0;
}

```

这里的 `__user` 明确表示 buf 指向用户空间内存。

它是修饰宏，不是数据类型。

例如：

```c
char __user *buf;

```

表示 buf 指向用户空间内存。

它主要用于内核源码的类型检查和静态检查，本身不是数据类型。

普通编译情况下通常不会产生实际运行代码。

### 函数

#### copy_to_user

```c
/**
 * @brief  将数据从内核空间复制到用户空间。
 *
 * @param  to: 用户空间目标地址。
 *
 * @param  from: 内核空间源地址。
 *
 * @param  n: 需要复制的字节数。
 *
 * @retval 0: 指定数据全部复制成功。
 *
 * @retval 非0: 没有成功复制的字节数。
 */
#include <linux/uaccess.h>

unsigned long copy_to_user(void __user *to,
                           const void *from,
                           unsigned long n);

```

```c
#include <linux/errno.h>
#include <linux/fs.h>
#include <linux/uaccess.h>

static ssize_t demo_read(struct file *file,
                         char __user *buf,
                         size_t size,
                         loff_t *offset)
{
    char kernel_buf[] = "hello";
    size_t copy_size = sizeof(kernel_buf);

    /* 用户提供的缓冲区较小时，只复制能够容纳的部分 */
    if (size < copy_size)
        copy_size = size;

    if (copy_to_user(buf, kernel_buf, copy_size) != 0)
        return -EFAULT;

    return copy_size;
}

```

这里：

```text
buf
→ read 回调传入的用户空间缓冲区

kernel_buf
→ 内核空间中的数据

copy_size
→ 实际准备复制的字节数

```

因此这次调用的实际含义就是：把 kernel\_buf 中的数据复制给调用 read() 的用户程序。

#### copy_from_user

```c
/**
 * @brief  将数据从用户空间复制到内核空间。
 *
 * @param  to: 内核空间目标地址。
 *
 * @param  from: 用户空间源地址。
 *
 * @param  n: 需要复制的字节数。
 *
 * @retval 0: 指定数据全部复制成功。
 *
 * @retval 非0: 没有成功复制的字节数。
 */
#include <linux/uaccess.h>

unsigned long copy_from_user(void *to,
                             const void __user *from,
                             unsigned long n);

```

```c
#include <linux/errno.h>
#include <linux/fs.h>
#include <linux/uaccess.h>

static char kernel_buf[32];

static ssize_t demo_write(struct file *file,
                          const char __user *buf,
                          size_t size,
                          loff_t *offset)
{
    size_t copy_size = size;

    if (copy_size > sizeof(kernel_buf))
        copy_size = sizeof(kernel_buf);

    if (copy_from_user(kernel_buf, buf, copy_size) != 0)
        return -EFAULT;

    return copy_size;
}

```

这里：

```text
buf
→ write 回调传入的用户空间数据

kernel_buf
→ 驱动自己的内核空间缓冲区

copy_size
→ 实际复制的字节数

```

因此这次调用的实际含义就是：把用户程序通过 write() 写入的数据保存到驱动的 kernel\_buf 中。

#### PTR_ERR

```c
/**
 * @brief  从 Linux 内核错误指针中取出其中保存的错误码。
 *
 * @param  ptr: 错误指针。
 *
 * @retval 返回错误指针中保存的错误码，通常为负数。
 */
#include <linux/err.h>

static inline long PTR_ERR(const void *ptr);

```

```c
#include <linux/device.h>
#include <linux/err.h>
#include <linux/module.h>

static int create_demo_class(void)
{
    struct class *demo_class;

    demo_class = class_create(THIS_MODULE, "demo_class");

    if (IS_ERR(demo_class))

    {
        err = PTR_ERR(demo_class);
        printk("class_create failed, err = %d\n", err);

        return err;    
    }

    class_destroy(demo_class);
    return 0;
}

```

这里 demo\_class 来自 class\_create。

如果 class\_create 失败，demo\_class 中保存的不是正常 class 地址，而是错误指针；PTR\_ERR 把其中的错误码取出来作为函数返回值。

#### IS_ERR

```c
/**
 * @brief  判断一个指针是否为 Linux 内核错误指针。
 *
 * @param  ptr: 需要判断的指针。
 *
 * @retval true: ptr 是错误指针。
 *
 * @retval false: ptr 不是错误指针。
 */
#include <linux/err.h>

static inline bool IS_ERR(const void *ptr);

```

```c
#include <linux/device.h>
#include <linux/err.h>
#include <linux/module.h>

static int create_demo_class(void)
{
    struct class *demo_class;

    demo_class = class_create(THIS_MODULE, "demo_class");

    if (IS_ERR(demo_class))
        return PTR_ERR(demo_class);

    class_destroy(demo_class);
    return 0;
}

```

这里 IS\_ERR 判断 class\_create 返回的 demo\_class 是否是错误指针。

不能仅通过 demo\_class 是否等于 NULL 来判断 class\_create 是否失败。

## 9.4 文件与设备

整理字符设备驱动所依赖的 VFS 文件操作接口、设备号以及设备注册和注销相关内容。

### 数据类型

#### struct file_operations

```c
#include <linux/fs.h>

/* Linux 4.9，省略当前未学习的成员 */
struct file_operations {
    struct module *owner;

    ssize_t (*read)(struct file *file,
                    char __user *buf,
                    size_t count,
                    loff_t *ppos);

    ssize_t (*write)(struct file *file,
                     const char __user *buf,
                     size_t count,
                     loff_t *ppos);

    int (*open)(struct inode *inode,
                struct file *file);

    int (*release)(struct inode *inode,
                   struct file *file);

    /* 还有其他成员 */
};

```

struct file\_operations 用来保存一组文件操作函数指针。

把驱动自己的函数填入对应成员后，用户程序对设备文件进行相应操作时，内核就可以找到驱动对应的处理函数。

| 成员 作用   |               |
| ------- | ------------- |
| owner   | 指定这组文件操作所属的模块 |
| open    | 文件被打开时调用      |
| read    | 读取文件时调用       |
| write   | 写入文件时调用       |
| release | 文件被关闭时调用      |

```c
#include <linux/fs.h>
#include <linux/module.h>

static int demo_open(struct inode *inode, struct file *file)
{
    return 0;
}

static ssize_t demo_read(struct file *file,
                         char __user *buf,
                         size_t size,
                         loff_t *offset)
{
    return 0;
}

static const struct file_operations demo_fops = {
    .owner = THIS_MODULE,
    .open  = demo_open,
    .read  = demo_read,
};

```

这里 demo\_open 和 demo\_read 都已经真正定义。

demo\_fops 的作用就是建立：

```text
open 操作 → demo_open
read 操作 → demo_read

```

这种对应关系。

#### struct file

```c
#include <linux/fs.h>

/* Linux 4.9，省略大量成员 */
struct file {
    struct inode *f_inode;
    const struct file_operations *f_op;
    loff_t f_pos;
    void *private_data;

    /* 还有其他成员 */
};

```

struct file 表示内核中的一个**已经打开的文件对象**。

用户程序每成功打开一次文件或设备文件，内核都会建立相应的打开文件对象。

| 成员 作用         |                            |
| ------------- | -------------------------- |
| f\_inode      | 指向该文件对应的 inode             |
| f\_op         | 指向当前文件使用的 file\_operations |
| f\_pos        | 当前文件读写位置                   |
| private\_data | 可供驱动保存本次打开实例的私有数据          |

#### struct inode

```c
#include <linux/fs.h>

/* Linux 4.9，省略大量成员 */
struct inode {
    unsigned long i_ino;
    dev_t i_rdev;
    loff_t i_size;

    const struct file_operations *i_fop;

    union {
        struct pipe_inode_info *i_pipe;
        struct block_device *i_bdev;
        struct cdev *i_cdev;
        char *i_link;
        unsigned i_dir_seq;
    };

    /* 还有其他成员 */
};

```

struct inode 用来描述文件系统中的一个文件对象。

对于设备文件，其中还可以保存设备号以及与具体设备相关的信息。

| 成员 作用   |                        |
| ------- | ---------------------- |
| i\_ino  | inode 编号               |
| i\_rdev | 设备文件对应的设备号             |
| i\_size | 文件大小                   |
| i\_fop  | 文件对应的 file\_operations |
| i\_cdev | 字符设备对应的 cdev           |

#### loff_t

```c
#include <linux/types.h>

typedef __kernel_loff_t loff_t;

```

loff\_t 是 Linux 中用于表示文件偏移位置的数据类型。

在 read、write 等文件操作回调中，经常通过 loff\_t 指针表示当前文件位置。

```c
#include <linux/fs.h>

static ssize_t demo_read(struct file *file,
                         char __user *buf,
                         size_t size,
                         loff_t *offset)
{
    loff_t old_offset = *offset;

    /* 假设本次读取了 4 字节 */
    *offset = old_offset + 4;

    return 4;
}

```

这里 offset 由内核作为 read 回调参数传入。

如果进入函数时：

```text
*offset = 10

```

本次读取 4 字节后：

```text
*offset = 14

```

因此 loff\_t 在这里表示的就是文件中的位置。

### 函数

#### MKDEV

```c
/**
 * @brief  根据主设备号和次设备号生成完整的设备号。
 *
 * @param  ma: 主设备号。
 *
 * @param  mi: 次设备号。
 *
 * @retval 返回组合后的 dev_t 类型设备号。
 */
#include <linux/kdev_t.h>

MKDEV(ma, mi);

```

类型：函数式宏。

```c
unsigned int major = 240;
unsigned int minor = 0;
dev_t devno;

devno = MKDEV(major, minor);

```

这里：

```text
major = 240
minor = 0

```

所以 devno 表示的就是设备号：

```text
240:0

```

MKDEV 的作用就是把分开的主设备号和次设备号组合成一个完整的 dev\_t 设备号。

#### register_chrdev

```c
/**
 * @brief  注册字符设备，并将字符设备与 file_operations 关联。
 *
 * @param  major: 主设备号。
 *                传入 0 时由内核动态分配主设备号；
 *                大于 0 时尝试使用指定主设备号。
 *
 * @param  name: 字符设备注册名称。
 *
 * @param  fops: 指向该字符设备 file_operations 的指针。
 *
 * @retval 大于0: major 为 0 时，返回动态分配到的主设备号。
 *
 * @retval 0: 使用指定主设备号注册成功。
 *
 * @retval 负数: 注册失败，返回对应的负错误码。
 */
#include <linux/fs.h>

static inline int register_chrdev(
    unsigned int major,
    const char *name,
    const struct file_operations *fops);

```

```c
#include <linux/fs.h>
#include <linux/module.h>

static int demo_open(struct inode *inode, struct file *file)
{
    return 0;
}

static const struct file_operations demo_fops = {
    .owner = THIS_MODULE,
    .open  = demo_open,
};

static int demo_register(void)
{
    int major;

    major = register_chrdev(0, "demo", &demo_fops);

    if (major < 0)
        return major;

    /*
     * 注册成功后：
     * major      = 内核动态分配的主设备号
     * "demo"     = 字符设备注册名称
     * demo_fops  = 该字符设备对应的文件操作
     */

    return major;
}

```

这里的 demo\_fops 和 demo\_open 都已经定义，因此可以清楚看到 register\_chrdev 建立的是：

```text
字符设备
    ↓
demo_fops
    ↓
demo_open 等驱动回调函数

```

#### unregister_chrdev

```c
/**
 * @brief  注销之前通过 register_chrdev 注册的字符设备。
 *
 * @param  major: 注册字符设备时使用或获得的主设备号。
 *
 * @param  name: 注册字符设备时使用的名称。
 *
 * @retval 无返回值。
 */
#include <linux/fs.h>

static inline void unregister_chrdev(
    unsigned int major,
    const char *name);

```

```c
#include <linux/fs.h>
#include <linux/module.h>

static const struct file_operations demo_fops = {
    .owner = THIS_MODULE,
};

static void demo(void)
{
    int major;

    major = register_chrdev(0, "demo", &demo_fops);

    if (major < 0)
        return;

    /*
     * 此时 major 就是上面注册成功后得到的主设备号。
     * 不再使用该字符设备时，用同一个 major 和名称进行注销。
     */
    unregister_chrdev(major, "demo");
}

```

这里的 major 不是凭空出现的，而是前面的 register\_chrdev 注册成功后得到的主设备号。

## 9.5 Linux 设备模型

整理 Linux 设备模型中 class 和 device 的创建、管理与销毁接口，用于组织设备并建立对应的设备对象。

### 函数

#### class_create

```c
/**
 * @brief  创建一个 Linux 设备类别 class。
 *
 * @param  owner: 拥有该 class 的内核模块，
 *                模块驱动中通常传入 THIS_MODULE。
 *
 * @param  name: class 的名称。
 *
 * @retval 正常指针: 创建成功，返回 struct class 指针。
 *
 * @retval 错误指针: 创建失败，返回编码了错误码的错误指针，
 *                   可使用 IS_ERR 和 PTR_ERR 判断和获取错误码。
 */
#include <linux/device.h>

class_create(owner, name);

```

类型：函数式宏。

```c
#include <linux/device.h>
#include <linux/err.h>
#include <linux/module.h>

static int  __init hello_init(void)

{
    printk("%s %s line: %d\n", __FILE__, __FUNCTION__, __LINE__);
    
    major = register_chrdev(0, "hello", &hello_drv_op);
    hello_class = class_create(THIS_MODULE, "hello_class");
    if (IS_ERR(hello_class))
    {
        int err;

        err = PTR_ERR(hello_class);

        printk("class_create failed, err = %d\n", err);

        unregister_chrdev(major, "my_hello");

        return err;    
    }

    device_create(hello_class, NULL, MKDEV(major, 0), NULL, "hello");

    return 0;

}

```

这里 demo\_class 已明确声明，并直接接收 class\_create 的返回值，因此可以看到这个返回指针后续如何判断和使用。

#### class_destroy

```c
/**
 * @brief  销毁之前创建的设备类别 class。
 *
 * @param  cls: 需要销毁的 struct class 指针。
 *
 * @retval 无返回值。
 */
#include <linux/device.h>

void class_destroy(struct class *cls);

```

```c
#include <linux/device.h>
#include <linux/err.h>
#include <linux/module.h>

static void demo(void)
{
    struct class *demo_class;

    demo_class = class_create(THIS_MODULE, "demo_class");

    if (IS_ERR(demo_class))
        return;

    /* demo_class 确实来自前面的 class_create */
    class_destroy(demo_class);
}

```

这里可以直接看出 class\_destroy 使用的 demo\_class 是前面 class\_create 成功创建出来的对象，而不是一个来源不明的指针。

#### device_create

```c
/**
 * @brief  在指定 class 中创建并注册一个设备。
 *
 * @param  cls: 设备所属的 class。
 *
 * @param  parent: 父设备指针，没有父设备时可以传入 NULL。
 *
 * @param  devt: 设备号，通常使用 MKDEV 生成。
 *
 * @param  drvdata: 与设备关联的驱动私有数据，
 *                  不需要时可以传入 NULL。
 *
 * @param  fmt: 设备名称格式字符串。
 *
 * @param  ...: 与 fmt 对应的可变参数。
 *
 * @retval 正常指针: 创建成功，返回 struct device 指针。
 *
 * @retval 错误指针: 创建失败，返回编码了错误码的错误指针。
 */
#include <linux/device.h>

struct device *device_create(
    struct class *cls,
    struct device *parent,
    dev_t devt,
    void *drvdata,
    const char *fmt,
    ...);

```

```c
#include <linux/device.h>
#include <linux/err.h>
#include <linux/kdev_t.h>
#include <linux/module.h>

static int demo(void)
{
    struct class *demo_class;
    struct device *demo_device;
    unsigned int major = 240;
    dev_t devno;

    /*
     * 假设主设备号 240 已经通过字符设备注册接口注册成功。
     */
    devno = MKDEV(major, 0);

    demo_class = class_create(THIS_MODULE, "demo_class");
    if (IS_ERR(demo_class))
        return PTR_ERR(demo_class);

    demo_device = device_create(demo_class,
                                NULL,
                                devno,
                                NULL,
                                "demo");

    if (IS_ERR(demo_device)) {
        class_destroy(demo_class);
        return PTR_ERR(demo_device);
    }

    return 0;
}

```

这个示例中各参数来源是明确的：

```text
demo_class
→ class_create 创建得到

NULL
→ 当前没有父设备

devno
→ 由主设备号 240、次设备号 0 通过 MKDEV 生成

NULL
→ 当前不保存额外驱动私有数据

"demo"
→ 创建的设备名称

```

#### device_destroy

```c
/**
 * @brief  删除指定 class 中对应设备号的设备。
 *
 * @param  cls: 设备所属的 class。
 *
 * @param  devt: 要删除设备的设备号。
 *
 * @retval 无返回值。
 */
#include <linux/device.h>

void device_destroy(struct class *cls, dev_t devt);

```

```c
#include <linux/device.h>
#include <linux/err.h>
#include <linux/kdev_t.h>
#include <linux/module.h>

static void demo(void)
{
    struct class *demo_class;
    struct device *demo_device;
    dev_t devno = MKDEV(240, 0);   /* 假设 240:0 已经注册 */

    demo_class = class_create(THIS_MODULE, "demo_class");
    if (IS_ERR(demo_class))
        return;

    demo_device = device_create(demo_class,
                                NULL,
                                devno,
                                NULL,
                                "demo");

    if (IS_ERR(demo_device)) {
        class_destroy(demo_class);
        return;
    }

    /*
     * 上面确实创建了 devno 对应的设备，
     * 不再使用时再用同一个 class 和 devno 删除。
     */
    device_destroy(demo_class, devno);

    class_destroy(demo_class);
}

```

这里 device\_destroy 的两个参数都有明确来源：

```text
demo_class
→ 前面 class_create 创建的设备类别

devno
→ 前面 device_create 创建设备时使用的同一个设备号

```

这样才能明确看出 device\_create 和 device\_destroy 之间的对应关系。


# 相关文件
[[系统修改与环境配置记录]]
[[嵌入式Linux应用开发完全手册V5.3_IMX6ULL_Pro开发板.pdf]]
[[c_c++]]
[[更改说明]]
# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 

# # 
