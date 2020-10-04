# Linux 简介

> 由芬兰人**林纳斯·托瓦兹**（Linus Torvalds）大学上学时出于个人爱好而编写的。
>

> Linux 是一套免费使用和自由传播的操作系统。
>
> Linux 支持多任务、多线程和多 CPU。
>
> Linux 运行　UNIX　工具软件、应用程序和网络协议。
>
> Linux 继承　UNIX　以网络为核心的设计思想，性能稳定。
>

> Linux 应用领域
>
>  LAMP（Linux + Apache + MySQL + PHP）
>
>  LNMP（Linux + Nginx+ MySQL + PHP） 
>



## ⋰Linux 安装

 https://www.runoob.com/linux/linux-install.html 



## ⋰Linux 命令大全

 https://www.runoob.com/linux/linux-command-manual.html 



# Linux 启动过程



## 内核引导

计算机电源打开

BIOS开机自检，启动硬件。

操作系统接管硬件。

操作系统读入 /boot 目录下的Linux内核文件。



## 运行 init

**init** 程序读取配置文件 /etc/inittab

> **init 进程**是系统所有进程的起点，没有这个进程，系统中任何进程都不会启动。



## 系统初始化

**init** 程序执行配置文件 /etc/inittab

>  /etc/inittab有这么一行： si::sysinit:/etc/rc.d/**rc.sysinit**　
>
> **rc.sysinit**是bash shell脚本
>
> rc.sysinit是每一个**运行级别**都要首先运行的重要脚本

配置文件执行**rc.sysinit**、完成系统初始化、

> 主要有：激活交换分区，检查磁盘，加载硬件模块以及其它一些需要优先执行任务。



## 建立终端 

**rc.sysinit**执行完毕后，返回init。

> 这时基本系统环境已经设置好了，各种守护进程也已经启动了

**init**打开**6个终端**，以便用户登录系统。

> 在inittab中的以下6行就是定义了6个终端
>
> 1:2345:respawn:/sbin/mingetty tty1
> 2:2345:respawn:/sbin/mingetty tty2
> 3:2345:respawn:/sbin/mingetty tty3
> 4:2345:respawn:/sbin/mingetty tty4
> 5:2345:respawn:/sbin/mingetty tty5
> 6:2345:respawn:/sbin/mingetty tty6



# SHELL

Shell是用户与Linux系统之间的接口进程。负责将用户的操作传给内核，这个进程是用户登录到系统后运行的命令解释器或某个特定的程序。

> Linux的Shell有许多种，每种都有不同的特点。常用的有
>
> - **sh(Bourne Shell)**
> - **csh(C Shell)**
> - ksh(Korn Shell), tcsh(TENEX/TOPS-20 type C Shell), bash(Bourne Again Shell)等。



系统管理员可以根据**Linux的用户系统文件/etc/passwd**为用户指定某个Shell。如果不指定Shell，那么系统使用sh为默认的登录Shell，即这个字段的值为/bin/sh。

用户的登录Shell也可以指定为某个特定的程序（此程序不是一个命令解释器）。

> 利用这一特点，我们**可以限制用户只能运行指定的应用程序**，在该应用程序运行结束后，用户就自动退出了系统。有些Linux 系统要求只有那些在系统中登记了的程序才能出现在这个字段中。



# Linux运行级别(runlevel)

运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动

运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登陆

运行级别2：多用户状态(没有NFS)

运行级别3：完全的多用户状态(有NFS)，登陆后进入控制台命令行模式

运行级别4：系统未使用，保留

运行级别5：X11控制台，登陆后进入图形GUI模式

运行级别6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动

# ？用户登录

一般来说，用户的登录方式有三种

（1）命令行登录

（2）ssh登录

（3）图形界面登录





## 图形模式与文字模式的切换

Linux预设提供了六个命令窗口终端机让我们来登录。

默认我们登录的就是第一个窗口，也就是tty1，这个六个窗口分别为tty1,tty2 … tty6，

**Ctrl + Alt + F1 ~ F6**：切换命令窗口

**Ctrl + Alt + F1 ~ F6**：进入命令窗口

**Ctrl + Alt + F7**：返回图形界面



## vmware 虚拟机

命令窗口切换的快捷键为 Alt + Space + F1~F6. 如果你在图形界面下请按Alt + Shift + Ctrl + F1~F6 切换至命令窗口。



## ⋰忘记密码解决方法

 https://www.runoob.com/linux/linux-forget-password.html 



##  ⋰Putty  远程登录

 https://www.runoob.com/linux/linux-remote-login.html 

# 关机

linux大多用在服务器，很少遇到关机的操作。毕竟服务器上跑一个服务是永无止境的，除非特殊情况下，不得已才会关机。

正确的关机流程为：**sync >** shutdown > reboot > halt



## sync ：数据同步到硬盘

```
sync 
```



## shutdown：关机

shutdown 会给系统计划一个时间关机。它可以被用于停止、关机、重启机器。

```shell
shutdown 	
#关机指令，你可以man shutdown 来看一下帮助文档。例如你可以运行如下命令关机：

shutdown –h 10 ‘This server will shutdown after 10 mins’ 	
#计算机将在10分钟后关机，并且会显示在登陆用户的当前屏幕中。

shutdown –h now 	#立马关机

shutdown –h 20:25 	#系统会在今天20:25关机

shutdown –h +10 	#十分钟后关机

shutdown –r now 	#系统立马重启

shutdown –r +10 	#系统十分钟后重启

```



## shutdown -c：取消关机

要取消即将进行的关机，只要输入下面的命令

```shell
 shutdown -c
```



## reboot ：重启

```shell
reboot #就是重启，等同于 shutdown –r now
```



## halt ：系统停止

halt 命令通知硬件来停止所有的 CPU 功能，但是仍然保持通电。你可以用它使系统处于低层维护状态。注意在有些情况会它会完全关闭系统。

```shell
halt #关闭系统，等同于shutdown –h now 和 poweroff
```





#  快捷键 

## Tab：命令补全

有『命令补全』与『文件补齐』的功能

```shell
[Tab]      ## 接在一串指令的第一个字的后面，则为『命令补全』
[Tab]      ## 接在一串指令的第二个字以后时，则为『文件补齐』
```

 若安装 bash-completion 软件，则在某些指令后面使用 [tab] 按键时，可以进行『选项/参数的补齐』功能！ 



## Ctrl + C ：命令停止

如果在Linux 底下输入了错误的指令或参数，想让当前的程序『停掉』的话，可以输入：

```shell
[Ctrl] + c 
```



## Ctrl + D：命令输入结束

『键盘输入结束(End Of File, EOF 或 End Of Input)』的意思

另外，他也可以用来取代 exit 的输入。

例如你想要直接离开文字接口，可以直接按下：

```shell
[Ctrl] + d   ## 相当于输入 exit
```



## Shift + PageUP |  Down：翻页 

```shell
[Shift]+[Page Up]    ## 往前翻页 
[Shift]+[Page Down]  ## 往后翻页
```



# 文件属性

为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。 

## 属性参数

> **d r-x r-x r-x**

代表这个文件是目录、文件或链接文件等等。

> [ **d** ]目录
>
> [ **-** ]文件
>
> [ **l** ]为链接文档(link file)
>
> [ **b** ]则表示为装置文件里面的可供储存的接口设备(可随机存取装置)
>
> [ **c** ]则表示为装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)



![363003_1227493859FdXT](https://www.runoob.com/wp-content/uploads/2014/06/363003_1227493859FdXT.png)



接下来的字符中，以三个为一组，且均为『rwx』 的三个参数的组合。

> **第1-3位**确定属主（该文件的所有者）拥有该文件的权限
>
> **第4-6位**确定属组（所有者的同组用户）拥有该文件的权限
>
> **第7-9位**确定其他用户拥有该文件的权限

> **[ r ]** 代表可读(read)
>
> **[ w ]** 代表可写(write)
>
> **[ x ]** 代表可执行(execute)



对于 root 用户一般情况下，文件的权限对其不起作用。





## ll ・ ls –l ：显示属性

来显示一个文件的属性以及文件所属的用户和组 

```shell
[root@www /]# ls -l
total 64
dr-xr-xr-x   2 root root 4096 Dec 14  2012 bin
dr-xr-xr-x   4 root root 4096 Apr 19  2012 boot
……
```



## chmod：更改属性

> 『-rwxrwxrwx』， 这九个权限是三个三个一组的！其中，我们可以使用数字来代表各个权限，各权限的分数对照表如下：
>
> - r:4
> - w:2
> - x:1
>
> 每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为： [-rwxrwx---] 分数则是：
>
> - owner = rwx = 4+2+1 = 7
> - group = rwx = 4+2+1 = 7
> - others= --- = 0+0+0 = 0
>
> 所以等一下我们设定权限的变更时，该文件的权限数字就是770！



变更权限的指令chmod的语法：

```shell
 chmod [-R] xyz 文件或目录
```

选项与参数：

- xyz : 就是刚刚提到的数字类型的权限属性，为 rwx 属性数值的相加。
- -R : 进行递归(recursive)的持续变更，亦即连同次目录下的所有文件都会变更

>  例：
>
>  将.bashrc这个文件所有的权限都设定启用 
>
>  ```shell
>  [root@www ~]# ls -al .bashrc
>  -rw-r--r--  1 root root 395 Jul  4 11:45 .bashrc
>  [root@www ~]# chmod 777 .bashrc
>  [root@www ~]# ls -al .bashrc
>  -rwxrwxrwx  1 root root 395 Jul  4 11:45 .bashrc
>  ```





## chgrp：更改所属的组

```shell
chgrp [-R] 属组名 文件名
```

参数选项

-R：递归更改文件属组，就是在更改某个目录文件的属组时，如果加上-R的参数，那么该目录下的所有文件的属组都会更改。



## chown：更改所属的主，组

```shell
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```



> 例：
>
> 进入 /root 目录（~）将install.log的拥有者改为bin这个账号：
>
> ```shell
> [root@www ~] cd ~
> [root@www ~]# chown bin install.log
> [root@www ~]# ls -l
> -rw-r--r--  1 bin  users 68495 Jun 25 08:53 install.log
> ```
>
> 
>

> 例：
>
> 将install.log的拥有者与群组改回为root 
>
> ```shell
> [root@www ~]# chown root:root install.log
> [root@www ~]# ls -l
> -rw-r--r--  1 root root 68495 Jun 25 08:53 install.log
> ```





# 文件与目录管理

>   Linux最顶级的目录为根目录  **/** 
>

> **绝对路径：**
> 由根目录 / 写起，例如： /usr/share/doc 这个目录。
>
> **相对路径：**
> 不是由 / 写起，例如由 /usr/share/doc 要到 /usr/share/man 底下时，可以写成： cd ../man 这就是相对路径的写法啦！



## ls ：列出目录

语法：

```shell
ls 目录名称
ls [--color={never,auto,always}] 目录名称
ls [--full-time] 目录名称
```

选项：

- -a ：全部的文件，连隐藏文件( 开头为 . ) 
- -d ：仅列出目录本身，不列出文件
- -l ：包含文件的属性与权限

> 例：
>
> 将root目录下的所有文件列出来(含属性与隐藏档)
>
> ```shell
> [root@www ~]# ls -al ~
> ```



## pwd ：显示当前目录路径

> 是 Print Working Directory 的缩写

语法：

```
[root@www ~]# pwd [-P]
```

选项：

- **-P** ：显示出确实的路径，而非使用连结 (link) 路径。

> 例：
>
> ```shell
> [root@www ~]# pwd
> /root   <== 显示出目录啦～
> ```



## cd ：切换目录

> 是Change Directory的缩写 
>

语法：

```shell
 cd [相对路径或绝对路径]
```

> 例：
> ```shell
> # 表示回到自己的root目录
> [root@www runoob]# cd ~
> 
> # 表示去到目前的上一级目录，亦即是 /root 的上一级目录的意思；
> [root@www ~]# cd ..
> ```
>





## mkdir ：创建目录

语法：

```shell
mkdir [-mp] 目录名称
```

选项与参数：

- -m ：配置文件的权限喔！直接配置，不需要看默认权限 (umask) 的脸色～
- -p ：帮助你直接将所需要的目录(包含上一级目录)递归创建起来！

> 例：
>
> 到/tmp下创建数个新目录：
>
> ```shell
> [root@www ~]# cd /tmp
> [root@www tmp]# mkdir test    <==创建一名为 test 的新目录
> [root@www tmp]# mkdir test1/test2/test3/test4
> mkdir: cannot create directory `test1/test2/test3/test4': 
> No such file or directory       <== 没办法直接创建此目录啊！
> [root@www tmp]# mkdir -p test1/test2/test3/test4
> ```



## cp ：复制

语法:

```shell
[root@www ~]# cp [-adfilprsu] 来源档(source) 目标档(destination)
[root@www ~]# cp [options] source1 source2 source3 .... directory
```

选项与参数：

- **-a：**相当於 -pdr 的意思，至於 pdr 请参考下列说明；(常用)
- **-d：**若来源档为连结档的属性(link file)，则复制连结档属性而非文件本身；
- **-f：**为强制(force)的意思，若目标文件已经存在且无法开启，则移除后再尝试一次；
- **-i：**若目标档(destination)已经存在时，在覆盖时会先询问动作的进行(常用)
- **-l：**进行硬式连结(hard link)的连结档创建，而非复制文件本身；
- **-p：**连同文件的属性一起复制过去，而非使用默认属性(备份常用)；
- **-r：**递归持续复制，用於目录的复制行为；(常用)
- **-s：**复制成为符号连结档 (symbolic link)，亦即『捷径』文件；
- **-u：**若 destination 比 source 旧才升级 destination ！

> 例：
>
> 用 root 身份，将 root 目录下的 .bashrc 复制到 /tmp 下，并命名为 bashrc
>
> ```shell
> [root@www ~]# cp ~/.bashrc /tmp/bashrc
> [root@www ~]# cp -i ~/.bashrc /tmp/bashrc
> cp: overwrite `/tmp/bashrc'? n  <==n不覆盖，y为覆盖
> ```





## mv ：移动・改名

语法：

```shell
[root@www ~]# mv [-fiu] source destination
[root@www ~]# mv [options] source1 source2 source3 .... directory
```

选项与参数：

- -f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖；

- -i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖！

- -u ：若目标文件已经存在，且 source 比较新，才会升级 (update)

  

## rm ：删除

语法：

```shell
 rm [-fir] 文件或目录
```

选项与参数：

- -f ：就是 force 的意思，忽略不存在的文件，不会出现警告信息；

- -i ：互动模式，在删除前会询问使用者是否动作

- -r ：**递归删除啊！最常用在目录的删除了！这是非常危险的选项！！！**

  

> 将刚刚在 cp 的实例中创建的 bashrc 删除掉
>
> ```shell
> [root@www tmp]# rm -i bashrc
> rm: remove regular file `bashrc'? y
> ```
>
> 如果加上 -i 的选项就会主动询问喔，避免你删除到错误的档名！



## rmdir ：仅删除空目录

语法：

```
 rmdir [-p] 目录名称
```

选项：

- **-p ：**连同上一级『空的』目录也一起删除

> 例：
>
> 删除 runoob 目录
>
> ```shell
> [root@www tmp]# rmdir runoob/
> ```

> 例：
>
> 将 mkdir 实例中创建的目录(/tmp 底下)删除掉！
>
> ```shell
> [root@www tmp]# ls -l   <==看看有多少目录存在？
> drwxr-xr-x  3 root  root 4096 Jul 18 12:50 test
> drwxr-xr-x  3 root  root 4096 Jul 18 12:53 test1
> drwx--x--x  2 root  root 4096 Jul 18 12:54 test2
> [root@www tmp]# rmdir test   <==可直接删除掉，没问题
> [root@www tmp]# rmdir test1  <==因为尚有内容，所以无法删除！
> rmdir: `test1': Directory not empty
> [root@www tmp]# rmdir -p test1/test2/test3/test4
> [root@www tmp]# ls -l        <==您看看，底下的输出中test与test1不见了！
> drwx--x--x  2 root  root 4096 Jul 18 12:54 test2
> ```
>
> 利用 -p 这个选项，立刻就可以将 test1/test2/test3/test4 一次删除。

 rmdir 仅能删除空的目录，可以使用 rm 命令来删除非空目录。





# 文件内容查看

## cat：由第一行开始显示文件内容

语法：

```shell
cat [-AbEnTv]
```

选项与参数：

- -A ：相当於 -vET 的整合选项，可列出一些特殊字符而不是空白而已；
- -b ：列出行号，仅针对非空白行做行号显示，空白行不标行号！
- -E ：将结尾的断行字节 $ 显示出来；
- -n ：列印出行号，连同空白行也会有行号，与 -b 的选项不同；
- -T ：将 [tab] 按键以 ^I 显示出来；
- -v ：列出一些看不出来的特殊字符

检看 /etc/issue 这个文件的内容：

```shell
[root@www ~]# cat /etc/issue
CentOS release 6.4 (Final)
Kernel \r on an \m
```



## tac ：由最后一行开始显示文件内容

tac与cat命令刚好相反，，可以看出 tac 是 cat 的倒着写！如：

```shell
[root@www ~]# tac /etc/issue

Kernel \r on an \m
CentOS release 6.4 (Final)
```



## nl  ：显示行号

语法：

```shell
nl [-bnw] 文件
```

选项与参数：

- -b ：指定行号指定的方式，主要有两种：
  -b a ：表示不论是否为空行，也同样列出行号(类似 cat -n)；
  -b t ：如果有空行，空的那一行不要列出行号(默认值)；
- -n ：列出行号表示的方法，主要有三种：
  -n ln ：行号在荧幕的最左方显示；
  -n rn ：行号在自己栏位的最右方显示，且不加 0 ；
  -n rz ：行号在自己栏位的最右方显示，且加 0 ；
- -w ：行号栏位的占用的位数。

> 实例一：用 nl 列出 /etc/issue 的内容
>
> ```shell
> [root@www ~]# nl /etc/issue
>      1  CentOS release 6.4 (Final)
>      2  Kernel \r on an \m
> ```
>
> 



## more：一页一页翻动

```shell
[root@www ~]# more /etc/man_db.config 
#
# Generated automatically from man.conf.in by the
# configure script.
#
# man.conf from man-1.6d
....(中间省略)....
--More--(28%)  <== 重点在这一行喔！你的光标也会在这里等待你的命令
```

在 more 这个程序的运行过程中，你有几个按键可以按的：

- 空白键 (space)：代表向下翻一页；
- Enter     ：代表向下翻『一行』；
- /字串     ：代表在这个显示的内容当中，向下搜寻『字串』这个关键字；
- :f      ：立刻显示出档名以及目前显示的行数；
- q       ：代表立刻离开 more ，不再显示该文件内容。
- b 或 [ctrl]-b ：代表往回翻页，不过这动作只对文件有用，对管线无用。



## less ：一页一页翻动

以下实例输出/etc/man.config文件的内容：

```sh
[root@www ~]# less /etc/man.config
#
# Generated automatically from man.conf.in by the
# configure script.
#
# man.conf from man-1.6d
....(中间省略)....
:   <== 这里可以等待你输入命令！
```

less运行时可以输入的命令有：

- 空白键  ：向下翻动一页；
- [pagedown]：向下翻动一页；
- [pageup] ：向上翻动一页；
- /字串   ：向下搜寻『字串』的功能；
- ?字串   ：向上搜寻『字串』的功能；
- n     ：重复前一个搜寻 (与 / 或 ? 有关！)
- N     ：反向的重复前一个搜寻 (与 / 或 ? 有关！)
- q     ：离开 less 这个程序；



## head：取出文件前面几行

语法：

```
head [-n number] 文件 
```

选项与参数：

- -n ：后面接数字，代表显示几行的意思

```
[root@www ~]# head /etc/man.config
```

默认的情况中，显示前面 10 行！若要显示前 20 行，就得要这样：

```
[root@www ~]# head -n 20 /etc/man.config
```



## tail：取出文件后面几行

语法：

```
tail [-n number] 文件 
```

选项与参数：

- -n ：后面接数字，代表显示几行的意思
- -f ：表示持续侦测后面所接的档名，要等到按下[ctrl]-c才会结束tail的侦测

```
[root@www ~]# tail /etc/man.config
# 默认的情况中，显示最后的十行！若要显示最后的 20 行，就得要这样：
[root@www ~]# tail -n 20 /etc/man.config
```



# Linux vi/vim

所有的 Unix Like 系统都会内建老式的 vi 编辑器 、功能已经很齐全了，但是还是有可以进步的地方。 

Vim是从 vi 发展出来的一个文本编辑器。代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。 



>   vim 的官方网站 ([http://www.vim.org](http://www.vim.org/))  

 ![img](https://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch.gif) 



## vi/vim 的三个模式 

 ![img](https://www.runoob.com/wp-content/uploads/2014/07/vim-vi-workmodel.png) 



### 命令模式

用户刚刚启动 vi/vim，便进入了命令模式。

此状态下敲击键盘动作会被Vim识别为命令，而非输入字符。比如我们此时按下i，并不会输入一个字符，i被当作了一个命令。

以下是常用的几个命令：

- **i** 切换到输入模式，以输入字符。
- **x** 删除当前光标所在处的字符。
- **:** 切换到底线命令模式，以在最底一行输入命令。

若想要编辑文本：启动Vim，进入了命令模式，按下i，切换到输入模式。

命令模式只有一些最基本的命令，因此仍要依靠底线命令模式输入更多命令。



### 输入模式

在命令模式下按下i就进入了输入模式。

在输入模式中，可以使用以下按键：

- **字符按键以及Shift组合**，输入字符
- **ENTER**，回车键，换行
- **BACK SPACE**，退格键，删除光标前一个字符
- **DEL**，删除键，删除光标后一个字符
- **方向键**，在文本中移动光标
- **HOME**/**END**，移动光标到行首/行尾
- **Page Up**/**Page Down**，上/下翻页
- **Insert**，切换光标为输入/替换模式，光标将变成竖线/下划线
- **ESC**，退出输入模式，切换到命令模式



### 底线命令模式

在命令模式下按下:（英文冒号）就进入了底线命令模式。

底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。

在底线命令模式中，基本的命令有（已经省略了冒号）：

- q 退出程序
- w 保存文件

按ESC键可随时退出底线命令模式。



## vi/vim 使用实例

###  **vi ［文件名］**：一般模式

直接输入  **vi 文件名**　就能够进入 vi 的一般模式了。请注意，记得 vi 后面一定要加文件名，不管该文件存在与否！ 

> 如果你想要使用 vi 来建立一个名为 linux.txt 的文件时，你可以这样做：
>
> ```
> $ vim linux.txt
> ```
>
> ```
> ［］            
> ～
> ～
> ～
> ～
> ～
> ～
> ～
> "linux.txt"
> ```



###   i・o・a  ：进入输入模式

在一般模式之中，只要按下 i, o, a 等字符就可以进入输入模式了！

在编辑模式当中，你可以发现在左下角状态栏中会出现 –INSERT- 的字样，那就是可以输入任意字符的提示。

> ```
> ［］            
> ～
> ～
> ～
> ～
> ～
> ～
> ～
> -- INSERT --
> ```

这个时候，键盘上除了 **Esc** 这个按键之外，其他的按键都可以视作为一般的输入按钮了，所以你可以进行任何的编辑。



###  按ESC ：回到一般模式

编辑完毕，按下 **Esc** 这个按钮即可

画面左下角不出现 – INSERT – 



## vi/vim 按键说明

 https://www.runoob.com/linux/linux-vim.html 



# Linux用户系统文件

>  完成用户管理的工作有许多种方法，但是每一种方法实际上都是对有关的系统文件进行修改。 
>
>  下面分别介绍这些文件的内容。 



## /etc/passwd：用户

> 文件是用户管理工作涉及的最重要的一个文件
>
> 这个文件对所有用户都是可读的
>
> Linux系统中的每个用户都在/etc/passwd文件中有一个对应的记录行，它记录了这个用户的一些基本属性。

它的内容类似下面的例子：

```shell
＃ cat /etc/passwd

root:x:0:0:Superuser:/:
daemon:x:1:1:System daemons:/etc:
bin:x:2:2:Owner of system commands:/bin:
sys:x:3:3:Owner of system files:/usr/sys:
adm:x:4:4:System accounting:/usr/adm:
uucp:x:5:5:UUCP administrator:/usr/lib/uucp:
auth:x:7:21:Authentication administrator:/tcb/files/auth:
cron:x:9:16:Cron daemon:/usr/spool/cron:
listen:x:37:4:Network daemon:/usr/net/nls:
lp:x:71:18:Printer administrator:/usr/spool/lp:
sam:x:200:50:Sam san:/home/sam:/bin/sh
```

从上面的例子我们可以看到，/etc/passwd中一行记录对应着一个用户，每行记录又被冒号(:)分隔为7个字段，其格式和具体含义如下：

```shell
sam:　　x:　　200:　　　　　50:　　　　Sam san:　　　/home/sam:　　/bin/sh
用户名:　口令:　用户标识号:　组标识号:　注释性描述:　　主目录:　　　　登录Shell

"用户名"
是代表用户账号的字符串。
通常长度不超过8个字符，并且由大小写字母和/或数字组成。
登录名中不能有冒号(:)，因为冒号在这里是分隔符。
为了兼容起见，登录名中最好不要包含点字符(.)，并且不使用连字符(-)和加号(+)打头。

"口令"
一些系统中，存放着加密后的用户口令字。
虽然这个字段存放的只是用户口令的加密串，不是明文，但是由于/etc/passwd文件对所有用户都可读，所以这仍是一个安全隐患。因此，现在许多Linux 系统（如SVR4）都使用了shadow技术，把真正的加密后的用户口令字存放到/etc/shadow文件中，而在/etc/passwd文件的口令字段中只存放一个特殊的字符，例如“x”或者“*”。

"用户标识号"
UID,是一个整数，系统内部用它来标识用户。一般情况下它与用户名是一一对应的。
如果几个用户名对应的用户标识号是一样的，系统内部将把它们视为同一个用户，但是它们可以有不同的口令、不同的主目录以及不同的登录Shell等。

'组标识号"
字段记录的是用户所属的用户组。
它对应着/etc/group文件中的一条记录。

"注释性描述"
字段记录着用户的一些个人情况。这个字段存放的是一段任意的注释性描述文字，
例如用户的真实姓名、电话、地址等，这个字段并没有什么实际的用途。
在不同的Linux 系统中，这个字段的格式并没有统一。
用finger命令输出。

"主目录"
用户的起始工作目录。它是用户在登录到系统之后所处的目录。
在大多数系统中，各用户的主目录都被组织在同一个特定的目录下，而用户主目录的名称就是该用户的登录名。各用户对自己的主目录有读、写、执行（搜索）权限，其他用户对此目录的访问权限则根据具体情况设置。

"登录Shell"
系统管理员可以根据系统情况和用户习惯为用户指定某个Shell。如果不指定Shell，那么系统使用sh为默认的登录Shell，即这个字段的值为/bin/sh。

```



### pseudo users：伪用户

这些用户在/etc/passwd文件中也占有一条记录，但是不能登录，因为它们的登录Shell为空。它们的存在主要是方便系统管理，满足相应的系统进程对文件属主的要求。

常见的伪用户如下所示：

```shell
bin 	#拥有可执行的用户命令文件 
sys 	#拥有系统文件 
adm 	#拥有帐户文件 
uucp 	#UUCP使用 
lp 		#lp或lpd子系统使用 
nobody 	#NFS使用
```

 除了上面列出的伪用户外，还有许多标准的伪用户，例如：audit, cron, mail, usenet等，它们也都各自为相关的进程和文件所需要。 



##  **/etc/shadow** ：用户口令

 它的文件格式与/etc/passwd类似，由若干个字段组成，字段之间用":"隔开

下面是/etc/shadow的一个例子：

```shell
＃ cat /etc/shadow

root:Dnakfw28zf38w:8764:0:168:7:::
daemon:*::0:0::::
bin:*::0:0::::
sys:*::0:0::::
adm:*::0:0::::
uucp:*::0:0::::
nuucp:*::0:0::::
auth:*::0:0::::
cron:*::0:0::::
listen:*::0:0::::
lp:*::0:0::::
sam:EkdiSECLWPdSa:9740:0:0::::
```



```shell
sam:　　	EkdiSECLWPdSa:　9740:　　　　0:　　　　　0::::
登录名:　　加密口令:　　　　最后修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志

"登录名"
是与/etc/passwd文件中的登录名相一致的用户账号

"口令"
字段存放的是加密后的用户口令字，长度为13个字符。如果为空，则对应用户没有口令，登录时不需要口令；
如果含有不属于集合 { ./0-9A-Za-z }中的字符，则对应的用户不能登录。

"最后一次修改时间"
表示的是从某个时刻起，到用户最后一次修改口令时的天数。
时间起点对不同的系统可能不一样。例如在SCO Linux 中，这个时间起点是1970年1月1日。

"最小时间间隔"
指的是两次修改口令之间所需的最小天数。

"最大时间间隔"
指的是口令保持有效的最大天数。

"警告时间"
字段表示的是从系统开始警告用户到用户密码正式失效之间的天数。

"不活动时间"
表示的是用户没有登录活动但账号仍能保持有效的最大天数。

"失效时间"
字段给出的是一个绝对的天数，如果使用了这个字段，那么就给出相应账号的生存期。
期满后，该账号就不再是一个合法的账号，也就不能再用来登录了。



```



## /etc/group：用户组

将用户分组是Linux 系统中对用户进行管理及控制访问权限的一种手段。

每个用户都属于某个用户组；一个组中可以有多个用户，一个用户也可以属于不同的组。

当一个用户同时是多个组中的成员时，在/etc/passwd文件中记录的是用户所属的主组，也就是登录时所属的默认组，而其他组称为附加组。用户要访问属于附加组的文件时，必须首先使用**newgrp**命令使自己成为所要访问的组中的成员。

/etc/group文件的一个例子如下：

```
root::0:root
bin::2:root,bin
sys::3:root,uucp
adm::4:root,adm
daemon::5:root,daemon
lp::7:root,lp
users::20:root,sam
```



```shell
users:　　　:　　　　20:　　　root,sam
组名:　　口令:　组标识号:　　　组内用户列表

"组名"
是用户组的名称，由字母或数字构成。与/etc/passwd中的登录名一样，组名不应重复。

"口令"
字段存放的是用户组加密后的口令字。一般Linux 系统的用户组都没有口令，即这个字段一般为空，或者是*。

"组标识号"
与用户标识号类似，也是一个整数，被系统内部用来标识组。

"组内用户列表"
是属于这个组的所有用户的列表/b]，不同用户之间用逗号(,)分隔。这个用户组可能是用户的主组，也可能是附加组。
```







# 用户管理

用户的账号一方面可以帮助系统管理员对使用系统的用户进行**跟踪**，并**控制他们对系统资源的访问**；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。

每个用户账号都拥有一个**唯一的用户名和各自的密码**。

用户在登录时键入正确的用户名和密码后，就能够进入系统和**自己的主目录**。

实现用户账号的管理，要完成的工作主要有如下几个方面：

- 用户账号的添加、删除与修改。
- 用户密码的管理。
- 用户组的管理。



## useradd：添加新用户

语法：

```shell
useradd 选项 用户名
```

参数说明：

- 选项:

  - -c comment 指定一段注释性描述。
  - -d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
  - -g 用户组 指定用户所属的用户组。
  - -G 用户组，用户组 指定用户所属的附加组。
  - -s Shell文件 指定用户的登录Shell。
  - -u 用户号 指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。

- 用户名:

  指定新账号的登录名。

> #### 例
>
> ```shell
>  useradd –d  /home/sam -m sam
> ```
>
> 此命令创建了一个用户sam，其中-d和-m选项用来为登录名sam产生一个主目录 /home/sam
>
> **/home为默认的用户主目录所在的父目录**。



> #### 例
>
> ```shell
>  useradd -s /bin/sh -g group –G adm,root gem
> ```
>
> 此命令新建了一个用户gem，该用户的登录Shell是 `/bin/sh`，它属于group用户组，同时又属于adm和root用户组，其中group用户组是其主组。
>
> 这里可能新建组：`#groupadd group及groupadd adm`
>
> 增加用户账号就是在/etc/passwd文件中为新用户增加一条记录，同时更新其他系统文件如/etc/shadow, /etc/group等。



##  userdel ：删除用户

其格式如下：

```
userdel 选项 用户名
```

- 选项
  -  **-r**，它的作用是把用户的主目录一起删除。

> 例：
>
> ```
> # userdel -r sam
> ```
>
> 此命令删除用户sam在系统文件中（主要是/etc/passwd, /etc/shadow, /etc/group等）的记录，同时删除用户的主目录。



##  usermod ：修改帐号

修改用户账号就是根据实际情况更改用户的有关属性，如用户号、主目录、用户组、登录Shell等。

格式：

```
usermod 选项 用户名
```

选项
- 包括`-c, -d, -m, -g, -G, -s, -u以及-o等`，这些选项的意义与`useradd`命令中的选项一样，可以为用户指定新的资源值。
- -l ，有些系统可以使用选项：新用户名、这个选项指定一个新的账号，即将原来的用户名改为新的用户名。

> 例
>
> ```
> # usermod -s /bin/ksh -d /home/z –g developer sam
> ```
>
> 此命令将用户sam的登录Shell修改为ksh，主目录改为/home/z，用户组改为developer。



## passwd ：用户密码管理

用户账号刚创建时没有密码，但是被系统锁定，无法使用，必须为其指定密码后才可以使用，

超级用户可以为自己和其他用户指定密码，普通用户只能用它修改自己的密码。

格式：

```shell
passwd 选项 用户名
```

 如果默认用户名，则修改当前用户的密码。 

选项：

- -l 锁定密码，即禁用账号。
- -u 密码解锁。
- -d 使账号无密码。
- -f 强迫用户下次登录时修改密码。

> 例
>
> 当前用户是sam，修改该用户自己的密码：
>
> ```shell
> $ passwd 
> Old password:****** 
> New password:******* 
> Re-enter new password:*******
> ```



> 例
>
> 当前用户是**超级用户**，指定任何用户的密码：
>
> ```shell
> # passwd sam 
> New password:******* 
> Re-enter new password:*******
> ```



普通用户修改自己的密码时，passwd命令会先询问原密码，验证后再要求用户输入两遍新密码，如果两次输入的密码一致，则将这个密码指定给用户

而超级用户为用户指定密码时，就不需要知道原密码。 



### passwd -d：空密码

> 为用户指定空密码时，执行下列形式的命令：
>
> ```shell
> # passwd -d sam
> ```
>
> 此命令将用户 sam 的密码删除，这样用户 sam 下一次登录时，系统就不再允许该用户登录了。



###   passwd -l：锁定登录

> passwd 命令还可以用 -l(lock) 选项锁定某一用户，使其不能登录，例如：
>
> ```shell
> # passwd -l sam
> ```





## ？添加批量用户

 https://www.runoob.com/linux/linux-user-manage.html 

  如果要添加几十个、上百个甚至上千个用户时 ，Linux系统提供了创建大量用户的工具，方法如下： 

### （1）创建用户文本

每一列按照`/etc/passwd`密码文件的格式书写，要注意每个用户的用户名、UID、宿主目录都不可以相同，其中密码栏可以留做空白或输入x号。一个范例文件user.txt内容如下：

```
user001::600:100:user:/home/user001:/bin/bash
user002::601:100:user:/home/user002:/bin/bash
user003::602:100:user:/home/user003:/bin/bash
user004::603:100:user:/home/user004:/bin/bash
user005::604:100:user:/home/user005:/bin/bash
user006::605:100:user:/home/user006:/bin/bash
```



### （2）导入用户文本

以root身份从刚创建的用户文件`user.txt`中导入数据，创建用户：

```
# newusers < user.txt
```

然后执行命令 `vipw` 或 `vi /etc/passwd` 

检查 `/etc/passwd` 文件是否出现导入数据，

检查用户的主目录是否已经创建。 



### （3）取消 shadow password 

这是为了方便下一步的密码转换工作，即先取消 `shadow password` 功能。

```
# pwunconv
```



### （4）创建密码文本

格式为：

```
用户名:密码
```

实例文件 `passwd.txt` 内容如下：

```
user001:123456
user002:123456
user003:123456
user004:123456
user005:123456
user006:123456
```



### （5）导入密码文本

创建用户密码，`chpasswd` 会将经过 `/usr/bin/passwd` 命令编码过的密码写入 `/etc/passwd` 的密码栏。

```
# chpasswd < passwd.txt
```



### （6）写入 shadow password

执行命令 `/usr/sbin/pwconv` 将密码编码为 `shadow password`，并将结果写入 `/etc/shadow`。

```
# pwconv
```

这样就完成了大量用户的创建了，之后您可以到/home下检查这些用户宿主目录的权限设置是否都正确，并登录验证用户密码是否正确。

# 用户组管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。

Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。 

用户组的管理涉及用户组的添加、删除和修改。

组的增加、删除和修改实际上就是对**/etc/group文件**的更新。 



## groupadd：增加用户组

格式：

```shell
groupadd 选项 用户组
```

选项：

- -g GID 指定新用户组的组标识号（GID）。

- -o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。

  

> #### 例1：
>
> 增加新组group1，指定标识号是 **当前 最大标识号加1**。
>
> ```shell
> # groupadd group1
> ```



> #### 例2：
>
> 增加新组group2，指定标识号101。
>
> ```shell
> # groupadd -g 101 group2
> ```



## groupdel：删除用户组

语法：

```
groupdel 用户组
```

> #### 例：
>
> 删除group1
>
> ```
> # groupdel group1
> ```



## groupmod：修改用户组属性

语法：

```
groupmod 选项 用户组
```

选项：

- -g GID 为用户组指定新的组标识号。
- -o 与-g选项同时使用，用户组的新GID可以与系统已有用户组的GID相同。
- -n新用户组 将用户组的名字改为新名字

> 实例1：
>
> 将组group2的组标识号修改为102。
>
> ```
> # groupmod -g 102 group2
> ```

> 实例2：
>
> 将组group2的标识号改为10000，组名修改为group3。
>
> ```
> # groupmod –g 10000 -n group3 group2
> ```



##  newgrp ：用户组切换

用户可以在登录后，使用命令newgrp切换到其他用户组，这个命令的参数就是目的用户组。例如：

```
$ newgrp root
```

这条命令将当前用户切换到root用户组，前提条件是root用户组确实是该用户的主组或附加组。类似于用户账号的管理，用户组的管理也可以通过集成的系统管理工具来完成。



## ⋰Linux　Userconf命令

Linux提供了集成的系统管理工具userconf，它可以用来对用户账号进行统一管理。

 https://www.runoob.com/linux/linux-comm-userconf.html 



# 磁盘管理

> Linux磁盘管理好坏直接关系到整个系统的性能问题。



## df：检查的磁盘空间占用情况

语法：

```
df [-ahikHTm] [目录或文件名]
```

选项与参数：

- -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；
- -k ：以 KBytes 的容量显示各文件系统；
- -m ：以 MBytes 的容量显示各文件系统；
- -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；
- -H ：以 M=1000K 取代 M=1024K 的进位方式；
- -T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；
- -i ：不用硬盘容量，而以 inode 的数量来显示

> 例 1
>
> 将系统内所有的文件系统列出来！
>
> ```shell
> [root@www ~]# df
> Filesystem      1K-blocks      Used Available Use% Mounted on
> /dev/hdc2         9920624   3823112   5585444  41% /
> /dev/hdc3         4956316    141376   4559108   4% /home
> /dev/hdc1          101086     11126     84741  12% /boot
> tmpfs              371332         0    371332   0% /dev/shm
> ```
>
> 在 Linux 底下如果 df 没有加任何选项，那么默认会将系统内所有的 (不含特殊内存内的文件系统与 swap) 都以 1 Kbytes 的容量来列出来！

> 例 2
>
> 将容量结果以易读的容量格式显示出来
>
> ```shell
> [root@www ~]# df -h
> Filesystem            Size  Used Avail Use% Mounted on
> /dev/hdc2             9.5G  3.7G  5.4G  41% /
> /dev/hdc3             4.8G  139M  4.4G   4% /home
> /dev/hdc1              99M   11M   83M  12% /boot
> tmpfs                 363M     0  363M   0% /dev/shm
> ```

> 例 3
>
> 将系统内的所有特殊文件格式及名称都列出来
>
> ```shell
> [root@www ~]# df -aT
> Filesystem    Type 1K-blocks    Used Available Use% Mounted on
> /dev/hdc2     ext3   9920624 3823112   5585444  41% /
> proc          proc         0       0         0   -  /proc
> sysfs        sysfs         0       0         0   -  /sys
> devpts      devpts         0       0         0   -  /dev/pts
> /dev/hdc3     ext3   4956316  141376   4559108   4% /home
> /dev/hdc1     ext3    101086   11126     84741  12% /boot
> tmpfs        tmpfs    371332       0    371332   0% /dev/shm
> none   binfmt_misc         0       0         0   -  /proc/sys/fs/binfmt_misc
> sunrpc  rpc_pipefs         0       0         0   -  /var/lib/nfs/rpc_pipefs
> ```

> 实例 4
>
> 将 /etc 底下的可用的磁盘容量以易读的容量格式显示
>
> ```shell
> [root@www ~]# df -h /etc
> Filesystem            Size  Used Avail Use% Mounted on
> /dev/hdc2             9.5G  3.7G  5.4G  41% /
> ```



## du：查看文件和目录使用的空间

du命令也是查看使用空间的，与 df 不一样的是，du 这个命令其实会直接到文件系统内去搜寻所有的文件数据。

语法：

```
du [-ahskm] 文件或目录名称
```

选项与参数：

- -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已。
- -h ：以人们较易读的容量格式 (G/M) 显示；
- -s ：列出总量而已，而不列出每个各别的目录占用容量；
- -S ：不包括子目录下的总计，与 -s 有点差别。
- -k ：以 KBytes 列出容量显示；
- -m ：以 MBytes 列出容量显示；

> 实例 1
>
> 只列出当前目录下的所有文件夹容量（包括隐藏文件夹）:
>
> ```shell
> [root@www ~]# du
> 8       ./test4     <==每个目录都会列出来
> 8       ./test2
> ....中间省略....
> 12      ./.gconfd   <==包括隐藏文件的目录
> 220     .           <==这个目录(.)所占用的总量
> ```
>
> 直接输入 du 没有加任何选项时，则 du 会分析当前所在目录的文件与目录所占用的硬盘空间。

> 实例 2
>
> 将文件的容量也列出来
>
> ```shell
> [root@www ~]# du -a
> 12      ./install.log.syslog   <==有文件的列表了
> 8       ./.bash_logout
> 8       ./test4
> 8       ./test2
> ....中间省略....
> 12      ./.gconfd
> 220     .
> ```

> 实例 3
>
> 检查根目录底下每个目录所占用的容量
>
> ```shell
> [root@www ~]# du -sm /*
> 7       /bin
> 6       /boot
> .....中间省略....
> 0       /proc
> .....中间省略....
> 1       /tmp
> 3859    /usr     <==系统初期最大就是他了啦！
> 77      /var
> ```
>
> 通配符 * 来代表每个目录。



## fdisk：磁盘分区表操作工具

fdisk 是 Linux 的磁盘分区表操作工具。

语法：

```shell
fdisk [-l] 装置名称
```

选项与参数：

- -l ：输出后面接的装置所有的分区内容。若仅有 fdisk -l 时， 则系统将会把整个系统内能够搜寻到的装置的分区均列出来。

> 实例 1
>
> 列出所有分区信息
>
> ```shell
> [root@AY120919111755c246621 tmp]# fdisk -l
> 
> Disk /dev/xvda: 21.5 GB, 21474836480 bytes
> 255 heads, 63 sectors/track, 2610 cylinders
> Units = cylinders of 16065 * 512 = 8225280 bytes
> Sector size (logical/physical): 512 bytes / 512 bytes
> I/O size (minimum/optimal): 512 bytes / 512 bytes
> Disk identifier: 0x00000000
> 
>     Device Boot      Start         End      Blocks   Id  System
> /dev/xvda1   *           1        2550    20480000   83  Linux
> /dev/xvda2            2550        2611      490496   82  Linux swap / Solaris
> 
> Disk /dev/xvdb: 21.5 GB, 21474836480 bytes
> 255 heads, 63 sectors/track, 2610 cylinders
> Units = cylinders of 16065 * 512 = 8225280 bytes
> Sector size (logical/physical): 512 bytes / 512 bytes
> I/O size (minimum/optimal): 512 bytes / 512 bytes
> Disk identifier: 0x56f40944
> 
>     Device Boot      Start         End      Blocks   Id  System
> /dev/xvdb2               1        2610    20964793+  83  Linux
> ```



> 实例 2
>
> 找出你系统中的根目录所在磁盘，并查阅该硬盘内的相关信息
>
> ```shell
> [root@www ~]# df /            <==注意：重点在找出磁盘文件名而已
> Filesystem           1K-blocks      Used Available Use% Mounted on
> /dev/hdc2              9920624   3823168   5585388  41% /
> 
> [root@www ~]# fdisk /dev/hdc  <==仔细看，不要加上数字喔！
> The number of cylinders for this disk is set to 5005.
> There is nothing wrong with that, but this is larger than 1024,
> and could in certain setups cause problems with:
> 1) software that runs at boot time (e.g., old versions of LILO)
> 2) booting and partitioning software from other OSs
>    (e.g., DOS FDISK, OS/2 FDISK)
> 
> Command (m for help):     <==等待你的输入！
> ```
>
> 输入 m 后，就会看到底下这些命令介绍
>
> ```shell
> Command (m for help): m   <== 输入 m 后，就会看到底下这些命令介绍
> Command action
>    a   toggle a bootable flag
>    b   edit bsd disklabel
>    c   toggle the dos compatibility flag
>    d   delete a partition            <==删除一个partition
>    l   list known partition types
>    m   print this menu
>    n   add a new partition           <==新增一个partition
>    o   create a new empty DOS partition table
>    p   print the partition table     <==在屏幕上显示分割表
>    q   quit without saving changes   <==不储存离开fdisk程序
>    s   create a new empty Sun disklabel
>    t   change a partition's system id
>    u   change display/entry units
>    v   verify the partition table
>    w   write table to disk and exit  <==将刚刚的动作写入分割表
>    x   extra functionality (experts only)
> ```
>
> 离开 fdisk 时按下 `q`，那么所有的动作都不会生效！相反的， 按下`w`就是动作生效的意思。
>
> ```shell
> Command (m for help): p  <== 这里可以输出目前磁盘的状态
> 
> Disk /dev/hdc: 41.1 GB, 41174138880 bytes        <==这个磁盘的文件名与容量
> 255 heads, 63 sectors/track, 5005 cylinders      <==磁头、扇区与磁柱大小
> Units = cylinders of 16065 * 512 = 8225280 bytes <==每个磁柱的大小
> 
>    Device Boot      Start         End      Blocks   Id  System
> /dev/hdc1   *           1          13      104391   83  Linux
> /dev/hdc2              14        1288    10241437+  83  Linux
> /dev/hdc3            1289        1925     5116702+  83  Linux
> /dev/hdc4            1926        5005    24740100    5  Extended
> /dev/hdc5            1926        2052     1020096   82  Linux swap / Solaris
> # 装置文件名 启动区否 开始磁柱    结束磁柱  1K大小容量 磁盘分区槽内的系统
> 
> Command (m for help): q
> ```
>
> 想要不储存离开吗？按下 q 就对了！不要随便按 w 啊！
>
> 使用 `p` 可以列出目前这颗磁盘的分割表信息，这个信息的上半部在显示整体磁盘的状态。



## mkfs：磁盘格式化

磁盘分割完毕后自然就是要进行文件系统的格式化，格式化的命令非常的简单，使用 `mkfs`（make filesystem） 命令。

语法：

```
mkfs [-t 文件系统格式] 装置文件名
```

选项与参数：

- -t ：可以接文件系统格式，例如 ext3, ext2, vfat 等(系统有支持才会生效)

> 实例 1
>
> 查看 mkfs 支持的文件格式
>
> ```shell
> [root@www ~]# mkfs[tab][tab]
> mkfs         mkfs.cramfs  mkfs.ext2    mkfs.ext3    mkfs.msdos   mkfs.vfat
> ```
>
> 按下两个[tab]，会发现 mkfs 支持的文件格式如上所示。

> 实例 2
>
> 将分区 /dev/hdc6（可指定你自己的分区） 格式化为 ext3 文件系统：
>
> ```shell
> [root@www ~]# mkfs -t ext3 /dev/hdc6
> mke2fs 1.39 (29-May-2006)
> Filesystem label=                <==这里指的是分割槽的名称(label)
> OS type: Linux
> Block size=4096 (log=2)          <==block 的大小配置为 4K 
> Fragment size=4096 (log=2)
> 251392 inodes, 502023 blocks     <==由此配置决定的inode/block数量
> 25101 blocks (5.00%) reserved for the super user
> First data block=0
> Maximum filesystem blocks=515899392
> 16 block groups
> 32768 blocks per group, 32768 fragments per group
> 15712 inodes per group
> Superblock backups stored on blocks:
>         32768, 98304, 163840, 229376, 294912
> 
> Writing inode tables: done
> Creating journal (8192 blocks): done <==有日志记录
> Writing superblocks and filesystem accounting information: done
> 
> This filesystem will be automatically checked every 34 mounts or
> 180 days, whichever comes first.  Use tune2fs -c or -i to override.
> # 这样就创建起来我们所需要的 Ext3 文件系统了！简单明了！
> ```



## fsck：磁盘检验

fsck（file system check）用来检查和维护不一致的文件系统。

若系统掉电或磁盘发生问题，可利用fsck命令对文件系统进行检查。

语法：

```
fsck [-t 文件系统] [-ACay] 装置名称
```

选项与参数：

- -t : 给定档案系统的型式，若在 /etc/fstab 中已有定义或 kernel 本身已支援的则不需加上此参数
- -s : 依序一个一个地执行 fsck 的指令来检查
- -A : 对/etc/fstab 中所有列出来的 分区（partition）做检查
- -C : 显示完整的检查进度
- -d : 打印出 e2fsck 的 debug 结果
- -p : 同时有 -A 条件时，同时有多个 fsck 的检查一起执行
- -R : 同时有 -A 条件时，省略 / 不检查
- -V : 详细显示模式
- -a : 如果检查有错则自动修复
- -r : 如果检查有错则由使用者回答是否修复
- -y : 选项指定检测每个文件是自动输入yes，在不确定那些是不正常的时候，可以执行 # fsck -y 全部检查修复。

> 实例 1
>
> 查看系统有多少文件系统支持的 fsck 命令：
>
> ```
> [root@www ~]# fsck[tab][tab]
> fsck         fsck.cramfs  fsck.ext2    fsck.ext3    fsck.msdos   fsck.vfat
> ```



> 实例 2
>
> 强制检测 /dev/hdc6 分区:
>
> ```
> [root@www ~]# fsck -C -f -t ext3 /dev/hdc6 
> fsck 1.39 (29-May-2006)
> e2fsck 1.39 (29-May-2006)
> Pass 1: Checking inodes, blocks, and sizes
> Pass 2: Checking directory structure
> Pass 3: Checking directory connectivity
> Pass 4: Checking reference counts
> Pass 5: Checking group summary information
> vbird_logical: 11/251968 files (9.1% non-contiguous), 36926/1004046 blocks
> ```
>
> 如果没有加上 -f 的选项，则由于这个文件系统不曾出现问题，检查的经过非常快速！若加上 -f 强制检查，才会一项一项的显示过程。



## mount：磁盘挂载

Linux 的磁盘挂载使用 `mount` 命令，卸载使用 `umount` 命令。

磁盘挂载语法：

```
mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n]  装置文件名  挂载点
```

> 实例 
>
> 用默认的方式，将刚刚创建的 /dev/hdc6 挂载到 /mnt/hdc6 上面！
>
> ```
> [root@www ~]# mkdir /mnt/hdc6
> [root@www ~]# mount /dev/hdc6 /mnt/hdc6
> [root@www ~]# df
> Filesystem           1K-blocks      Used Available Use% Mounted on
> .....中间省略.....
> /dev/hdc6              1976312     42072   1833836   3% /mnt/hdc6
> ```



## umount：磁盘卸载

磁盘卸载命令 `umount` 语法：

```
umount [-fn] 装置文件名或挂载点
```

选项与参数：

- -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下；
- -n ：不升级 /etc/mtab 情况下卸除。

> 卸载/dev/hdc6
>
> ```
> [root@www ~]# umount /dev/hdc6     
> ```

















































































