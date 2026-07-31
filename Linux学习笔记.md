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

| 命令     | 说明                    |
| -------- | ----------------------- |
| h        | 光标向左移动            |
| j        | 光标向下移动            |
| k        | 光标向上移动            |
| l        | 光标向右移动            |
| 0        | 移动到当前行行首        |
| $        | 移动到当前行行尾        |
| gg       | 移动到文件第一行        |
| G        | 移动到文件最后一行      |
| nG       | 移动到第 n 行，例如 10G |
| Ctrl + f | 向下翻一页              |
| Ctrl + b | 向上翻一页              |

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

| 选项             | 作用                              |
| ---------------- | --------------------------------- |
| -o               | 指定输出文件名                    |
| -E               | 只进行预处理                      |
| -S               | 只进行预处理和编译，生成汇编文件  |
| -c               | 只编译生成目标文件，不链接        |
| -Wall            | 显示更多警告信息                  |
| -Werror          | 将警告当成错误处理                |
| -g               | 生成调试信息，方便gdb调试         |
| -I   （大写的i） | 指定头文件路径                    |
| -L               | 指定库文件路径                    |
| -l   （小写的L） | 指定链接的库                      |
| -D               | 定义宏                            |
| -O               | 优化程序                          |
| -v               | verbose，显示编译过程中的详细信息 |

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

## 3.6 常见错误

### gcc: command not found

```bash
原因:
没有安装gcc，或者环境变量没有配置好

解决:
安装gcc，或者检查PATH环境变量
```

### arm-linux-gcc: command not found

```bash
原因:
没有安装ARM交叉编译器，或者交叉编译器路径没有加入PATH

解决:
检查交叉编译器是否存在
检查环境变量PATH是否配置正确
```

### Permission denied

```bash
原因:
程序没有执行权限

解决:
chmod +x hello
./hello
```

### No such file or directory

```bash
原因:
文件不存在，或者当前目录不对

解决:
ls
pwd
cd 到程序所在目录
```

### Exec format error

```bash
原因:
程序架构不匹配

常见情况:
把虚拟机gcc编译出来的程序，放到ARM开发板上运行

解决:
使用ARM交叉编译器重新编译
```

## 3.7 常用编译命令总结

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

| 命令          | 作用                            |
| ------------- | ------------------------------- |
| `make`        | 执行默认目标                    |
| `make clean`  | 执行 `clean` 目标，清理生成文件 |
| `make app`    | 执行 `app` 目标                 |
| `make -C dir` | 进入 `dir` 目录执行 `make`      |

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

## 开发板亮屏/息屏

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

# 7 宏

## 7.1 宏参数

### 输入事件类型宏（EV_*）

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

### 信号宏（SIG*）

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

### fd控制宏（F_*）

#### 概括

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

#### F_SETOWN

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

#### F_GETFL

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

#### F_SETFL

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

## 7.2 宏函数

### EVIOCGBIT

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

### fd集合

#### FD_ZERO：清空集合

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

#### FD_SET：将fd加入集合

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

#### FD_ISSET：判断是否在集合

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



# 8 数据类型

## 输入设备相关

### struct input_id

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

### struct input_event

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

## 访问硬件方式相关

### struct pollfd

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

### struct timeval

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

### fd_set

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



# 9 功能函数

## ioctl : 设备控制函数

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

## fcntl：文件描述符控制函数

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

## getpid：获取进程ID

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

## mmap ：地址映射函数

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

## memset：内存数据设置函数

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

## munmap：取消地址映射函数

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

## fstat：获取文件属性信息函数

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

## poll： 监视文件

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

## select：监视文件

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

## signal：设置信号处理方式

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

# 10 c中常用函数与数据类型

## 10.1 数据类型



## 10.2 函数

### 10.2.1 字符相关函数

#### strtoul：字符串转整型函数

```c
/**
 * @brief  将字符串转换成 unsigned long 类型的无符号整数。
 *
 * @param  str: 要转换的字符串。
 *
 * @param  endptr: 用于保存转换结束位置的指针。
 *                 不需要时可以传入 NULL。
 *
 * @param  base: 转换时使用的进制。
 *               0 表示根据字符串前缀自动判断进制。
 *               10 表示十进制。
 *               16 表示十六进制。
 *
 * @retval 转换得到的 unsigned long 类型数值。
 */
unsigned long strtoul(const char *str,
                      char **endptr,
                      int base);
```

代码示例：

```
unsigned long num;

num = strtoul("30", NULL, 10);

/*
 * 将字符串 "30" 按照十进制转换。
 *
 * 转换结果：
 * num = 30
 */
```

#### strcmp：比较字符串大小

```c
/**
 * @brief  按字符逐个比较两个字符串的大小。
 *
 * @param  s1: 指向第一个以 '\0' 结尾的字符串。
 *
 * @param  s2: 指向第二个以 '\0' 结尾的字符串。
 *
 * @retval 0: 两个字符串内容相同。
 *
 * @retval 负数: s1 小于 s2。
 *
 * @retval 正数: s1 大于 s2。
 */
#include <string.h>

int strcmp(const char *s1, const char *s2);
```

代码示例：

```c
int result;

result = strcmp("apple", "banana");

/*
 * 比较字符串 "apple" 和 "banana"。
 *
 * 结果：
 * result < 0；
 * 表示 "apple" 小于 "banana"。
 *
 * strcmp() 的正数或负数具体是多少没有固定要求，
 * 判断时应与 0 比较。
 */
```

#### str_delete：字符删除

```c
/**
 * @brief  从字符串的指定下标开始删除指定数量的字符。
 *
 * @param  str: 需要修改的字符串。
 *
 * @param  pos: 开始删除的位置，下标从 0 开始。
 *
 * @param  count: 需要删除的字符数量。
 *
 * @retval 无返回值。
 *
 * @note   str_delete() 不是 C 标准库函数，需要自行定义。
 */
#include <string.h>

void str_delete(char *str, size_t pos, size_t count)
{
    size_t len = strlen(str);

    if (pos >= len)
        return;

    if (count > len - pos)
        count = len - pos;

    memmove(str + pos,
            str + pos + count,
            len - pos - count + 1);
}
```

代码示例：

```c
char str[] = "abcdefg";

str_delete(str, 2, 3);

/*
 * 从下标 2 开始删除 3 个字符。
 *
 * 删除前：
 * "abcdefg"
 *
 * 删除的字符：
 * c、d、e
 *
 * 删除后：
 * "abfg"
 *
 * memmove() 会把后面的字符和结尾的 '\0'
 * 一起向前移动，覆盖需要删除的内容。
 */
```



### 10.2.2 内存相关函数

#### calloc

```c
/**
 * @brief  在堆内存中申请一块连续空间，并将申请到的内存全部初始化为 0。
 *
 * @param  nmemb: 要申请的元素个数。
 *
 * @param  size: 每个元素占用的字节数。
 *
 * @retval 非 NULL: 内存申请成功，返回所申请内存的首地址。
 *
 * @retval NULL: 内存申请失败。
 */
#include <stdlib.h>
void *calloc(size_t nmemb, size_t size);
```

代码示例：

```c
int *array;

array = calloc(10, sizeof(int));

/*
 * 申请可以存放 10 个 int 类型数据的连续内存空间。
 *
 * 申请的总大小：
 * 10 × sizeof(int)
 *
 * calloc() 会将这块内存中的所有字节初始化为 0。
 *
 * array：
 * 申请成功时，保存内存空间的首地址；
 * 申请失败时，值为 NULL。
 */
```

#### malloc

```c
/**
 * @brief  在堆内存中申请一块指定字节数的连续内存空间。
 *
 * @param  size: 要申请的内存字节数。
 *
 * @retval 非 NULL: 内存申请成功，返回所申请内存的首地址。
 *
 * @retval NULL: 内存申请失败。
 */
#include <stdlib.h>
void *malloc(size_t size);
```

代码示例：

```c
int *array;

array = malloc(10 * sizeof(int));

/*
 * 申请可以存放 10 个 int 类型数据的连续内存空间。
 *
 * 申请的总大小：
 * 10 × sizeof(int)
 *
 * malloc() 不会初始化申请到的内存，
 * 内存中原来的数据是不确定的。
 *
 * array：
 * 申请成功时，保存内存空间的首地址；
 * 申请失败时，值为 NULL。
 */
```

# 11 第三方库与组件

## 11.1 FreeType 字体库

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

### 功能函数表

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

### 数据类型详解

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

### 功能函数详解

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



# 尾页

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
