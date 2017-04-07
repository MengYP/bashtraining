# Linux
## 一、Linux 常用命令

命令基本格式： `命令 [选项] [参数]` 

>注意：
>- 个别命令使用不遵循此格式;  
>- 当有多个选项时， 可以写在一起;   
>- 简化选项与完整选项： `-a` 等于 `--all`

`[root@localhost ~]#`

* `root`       代表当前登录用户
* `localhost`  主机名
* `~`          当前所在目录（家目录）
* `#`          超级用户的提示符
*  普通用户的提示符是 `$` 
*  `Linux`中，管理员账号是`root`

查询目录中内容： `ls`

命令格式： `ls [选项] [文件或目录]`

>选项：
>- `-a` 显示所有文件，包括隐藏文件
（`liunx`中以`.`开头的文件是隐藏文件）
>- `-l` 显示详细信息
>- `-d` 查看目录属性
>- `-h` 人性化显示文件大小
>- `-i` 显示`inode`（每一个文件都有一个id号）
>
> 命令： `ll`  相当于  `ls -l`

`-rw-r--r--`
>- `-`  ：文件类型
>>第一位符号含义：
>>>-  `-` 代表文件; 
>>>-  `d` 代表目录; 
>>>-  `|` 代表软链接文件）
>
>- `rw-`  ：u所有者    
>- `r--`   ：g所属组    
>- `r--`   ：o其他人 
>- `r`读   `w`写   `x`执行

* 注意：`liunx`中有七种文件类型，`文件`、`目录`、`软连接`、`块设备文件`、`字符设备文件`、`套接字文件`、`管道文件`。

### 1、目录处理命令

#### 1.1 建立目录： `mkdir`

命令格式： `mkdir -p [目录名]`

>`-p` 递归创建
>
>英文：`make directories`

#### 1.2 切换所在目录： `cd`

命令格式：`cd [目录]`

>英文愿意：`change directory`

>简化操作：
>>- `cd ~` 或者 `cd`   ：进入当前用户的家目录
>>- `cd –`  进入上次目录
>>- `cd ..`  进入上一级目录
>>- `cd .`   进入当前目录

* 清屏快捷键： `Ctrl + L` 

>`相对路径`：参照当前所在目录，进行查找。
如：`[root@imooc ~]# cd ../usr/local/src/`
>
>`绝对路径`：从根目录开始指定，一级一级递归。在任何目录下，都能进入指定位置。
如： `[root@imooc ~]# cd /etc/` 

#### 1.3 查询所在目录位置： `pwd`

命令格式 ： `pwd`

>英文愿意：`print working directory`

#### 1.4 删除空目录： `rmdir`

命令格式： `rmdir [目录名]`

>英文愿意：`remove empty directories`
>
>注意：只能刪除空目录。

#### 1.5 删除文件或目录：rm

命令格式：`rm -rf [文件或目录]`

>英文愿意：`remove`
>
>选项：
>>- `-r` 删除目录
>>- `-f`  强制

#### 1.6 复制命令：`cp` 

命令格式： `cp [选项] [原文件或目录] [目标目录]`

>英文：`copy`
>选项： 
>>- `-r` ：复制目录
>>- `-p` ：连带文件属性复制
>>- `-d` ：若原文件是链接文件，则复制链接属性
>>- `-a` ：相当与 -pdr

#### 1.7 剪切或改名命令： `mv`

命令格式： `mv [原文件或目录] [目标目录]`

>英文：`move`
>
>原目录和目标目录**在同一个目录中**就是**改名**命令;
>
>原目录和目标目录**不在同一个目录中**就是**剪切**命令。

#### 1.8 常用目录的作用

>- `/`       根目录
>- `/bin`    命令保存目录（普通用户就可以读取的命令）
>- `/boot`   启动目录，启动相关文件
>- `/dev`    设备文件保存目录
>- `/etc`    配置文件保存目录
>- `/home`   普通用户的家目录
>- `/lib`    系统库保存目录
>- `/mnt`    系统挂载目录（常用）
>- `/media`  挂载目录

* 根目录下的`bin`和`sbin`，`usr`目录下的`bin`和`sbin`，这四个目录都是用来保存系统命令的。
* bin目录下是任何用户都能执行;
* sbin目录下只有root超级用户才能够执行;

>- `/root`   超级用户的家目录
>- `/tmp`  临时目录
>- `/proc`  直接写入内存的
>- `/sys`
>>  
>>`proc`和`sys`目录不能直接操作，这两个目录保存的是内存的过载点。
>- `/usr`  系统软件资源目录
>- `/var`  系统相关文档内容

* 可以在家目录`root`或`home`，以及`tmp`目录下随便放内容。

#### 1.9 链接命令：`ln`

命令格式：`ln -s [原文件] [目标文件]`

>英文：link
>
>功能描述：生成链接文件
>
>选项：`-s` 创建软链接


>硬链接：
>>- 1、拥有相同的`i`节点和存储`block`块，可以看做是同一个文件。
>>- 2、可通过`i`节点识别。
>>- 3、不能跨分区。
>>- 4、不能针对目录使用。
>>- 5、对一个文件**添加一个硬链接**，它的**引用计数会加1**。
>>- 6、删除原文件，硬链接文件仍然可以使用。

>软链接：
>
>>- 1、类似`windows`快捷方式
>>- 2、软链接拥有自己打`i`节点和`Block`块，但是数据块中只保存原文件打文件名和`i`节点号，并没有实际打文件数据。
>>- 3、`lrwxrwxrwx`    
`l`软链接
软链接文件权限都为：`rwxrwxrwx`
>>- 4、修改任意文件，另一个都改变。
>>- 5、删除原文件，软链接不能使用。
>
>注意：软链接创建一定要写绝对路径。

### 2、文件搜索命令

#### 2.1 文件搜索命令： `locate`

命令格式：`locate 文件名`

> 在后台数据库中按文件名搜索，**搜索速度更快**。
>
>`/var/lib/mlocate`  是存放  `#locate` 命令所搜索的后台数据库  `mlocate.db`
>
>`updatedb`  ：更新数据库
>
>只能按文件名搜索，遵循配置文件。
>
>`/etc/updatedb.com`  配置文件
>
>>- `PRUNE_BIND_MOUNTS=”yes”`   ：#开启搜索限制
>>- `PRUNEFS =`      	：#搜索时，不搜索的文件系统
>>- `PRUNENAMES=`     ：#搜索时，不搜索打文件类型
>>- `PRUNEPATHS=`     ：#搜索时，不搜索打路径
		
#### 2.2 搜索命令的命令 ：`whereis与which`

命令格式： `whereis 命令名字`

>搜索命令所在路径及帮助文档所在位置。
>选项： 
>>- `-b`  ：只查找可执行文件
>>- `-m` ：只查找帮助文件

命令格式：`which 命令名字`

>搜索命令所在路径及别名
		
>PATH环境变量：
>
>定义的是系统搜索命令的路径

```bash
$ echo $PATH
/home/ubuntu/bin:/home/ubuntu/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```	

#### 2.3 文件搜索命令：`find`

命令格式：`find [搜索范围] [搜索条件]`    

>搜索文件 ：`find  / -name install.log`

>避免大范围搜索，会非常耗费系统资源 
>
>完全匹配，不是模糊查询。
>
>`find` 是在系统当中搜索符合条件的文件名。如果需要匹配，使用通配符匹配，通配符是完全匹配。
>
>`find /root -iname install.log` : 不区分大小写
>
>`find /root -user root` ：按照所有者搜索
>
>`find /root -nouser` ：查找没有所有者的文件


>`find /var/log/ -mtime +10` ：查找10天前修改的文件
>>- `-10` 10天内修改文件
>>- `10`  10天当天修改的文件
>>- `+10` 10天前修改的文件
>>
>>- `atime`   ：文件访问时间
>>- `ctime`   ： 改变文件属性
>>- `mtime`   ： 修改文件内容


>`find .(目录) -size 25k`  ：查找文件大小是25KB的文件
>>- `-25k`     小于25KB的文件
>>- `25k`     等于25KB的文件
>>- `+25k`     大于25KB的文件


>`find . -inum   262422` ：查找i节点是262422的文件


>`find /etc -size +20k -a -size -50k` ：查找/etc/目录下，大于20KB并且小于50KB的文件
>>- `-a`  `and`   逻辑与， 两个条件都满足
>>- `-o`  `or`   逻辑或， 两个条件满足一个即可


>`find /etc -size +20k -a -size -50k -exec ls -lh {}  \;` ：查找/etc/目录下，大于20KB并且小于50KB的文件，并显示详细信息
>
>>`-exec/-ok  命令 {} \;`    对搜索结果执行操作。


#### 2.4 `Linux`中的通配符

`*`   匹配任意内容

`?`   匹配任意一个字符

`[]`  匹配任意一个中括号内的字符


#### 2.5 `grep`命令

命令格式： `grep [选项] 字符串 文件名`

> 在文件当中匹配符合 条件的字符串
> 选项：
>>- `-i`  忽略大小写
>>- `-v`  排除指定字符串
	

>`find`命令与`grep`命令的区别
>>
>>`find`命令：在系统当中搜索符合条件打文件名，如果需要匹配，使用通配符匹配，通配符是完全匹配。
>>
>>`grep`命令：在文件当中搜索符合条件打字符串，如果需要匹配，使用正则表达式匹配，正则表达式是包含匹配。

### 3、帮助命令

#### 3.1 帮助命令 `man`

命令格式：`man 命令`

>获取指定命令的帮助
>`man ls`  ： 查看`ls`的帮助

>`man`的级别：
>>- `1`  ：查看命令的帮助
>>- `2` ：查看可被内核调用的函数的帮助
>>- `3` ：查看函数和函数库的帮助
>>- `4` ：查看特殊文件的帮助（主要是`/dev`目录下的文件）
>>- `5` ：查看配置文件的帮助
>>- `6` ：查看游戏的帮助
>>- `7` ：查看其它杂项的帮助
>>- `8` ：查看系统管理员可用命令的帮助
>>- `9` ：查看和内核相关文件的帮助

查看命令拥有哪个级别的帮助：

格式：`man -f 命令`
相当于： `whatis 命令`

举例： 
```bash
$ man -5 passwd
$ man -4 null
$ man -8 ifconfig
```

查看和命令相关的所有帮助：

命令格式：`man -k 命令`

相当于：`apropos 命令`

例如：
```bash
apropos passwd
```

#### 3.2 其他帮助命令

1》选项帮助：

命令格式： `命令 --help`

>获取命令选项的帮助

例如： 
```bash
ls –help
```


2》`shell` 内部命令帮助：

命令格式： `help shell 内部命令`

>获取`shell`内部命令的帮助

例如： 
```bash
whereis cd  # 确定是否是`shell`内部命令
help cd     # 获取内部命令帮助
```

3》详细命令帮助`info`

命令格式： `info 命令名字`：

>- `回车` ： 进入子帮助页面（带有*号标记）
>- `u`   ： 进入上层页面
>- `n`   ：进入下一个帮助小节
>- `p`   ：进入上一个帮助小节
>- `-q`  ： 退出


### 4、压缩与解压缩命令

> 常用压缩格式：`.zip`  `.gz`   `.bz2`  `.tar.gz`       `.tar.bz2`

#### 4.1 格式 `.zip` 

命令格式：`zip  压缩文件名  原文件`  ：压缩文件

命令格式： `zip -r 压缩文件名  原目录`  ：压缩目录

命令格式：`unzip  压缩文件`  ： 解压缩`.zip`文件

#### 4.2 格式 `.gz`

命令格式：`gzip 原文件` ：压缩为`.gz`格式的压缩文件，原文件会消失

命令格式：`gzip -c 原文件 > 压缩文件` ：压缩为`.gz`格式，原文件保留。
例如：`gzip -c testdir > testdir.gz`

命令格式：`gzip -r 目录` ：压缩目录下所有的子文件，但是不能压缩目录

命令：`gzip -d 压缩文件` ：解压缩文件

命令：`gunzip 压缩文件`  ：解压缩文件

#### 4.3 格式 `.bz2`

命令格式：`bzip2 原文件`  ：压缩为.bz2格式，不保留原文件

命令格式：`bzip2 -k 原文件` ：压缩之后保留原文件

>注意：`bzip2`命令不能压缩目录。

命令格式：`bzip2 -d 压缩文件`  ：解压缩，-k保留压缩文件

命令格式：`bunzip2 压缩文件`  ：解压缩， -k保留压缩文件
	
#### 4.4 格式 `.tar.gz` 

命令格式： `tar -cvf  打包文件名  原文件`

>选项：
>>- `-c`  ：打包
>>- `-v`  ：显示过程
>>- `-f` ：制定打包后的文件名
>>- `-x`  ： 解打包

命令格式：`tar -xvf 打包文件名` ：解打包命令

例如： `tar -cvf  test.tar  test`

例如：`tar -xvf  test.tar`

* 其实`.tar.gz`格式是先打包为`.tar`格式，再压缩为`.gz`格式

命令格式： `tar -zcvf 压缩包名.tar.gz  原文件`

>选项： `-z`  压缩为`.tar.gz`格式

命令格式： `tar -zxvf  压缩包名.tar.gz`

>选项：`-x`  解压缩`.tar.gz`格式


#### 4.5  格式 `.tar.bz2`

* 其实`.tar.bz2`格式是先打包为`.tar`格式，再压缩为`.bz2`格式

命令格式： `tar -zcvf 压缩包名.tar.bz2  原文件`

>选项： `-z`   压缩为`.tar.bz2`格式

命令格式： `tar -zxvf  压缩包名.tar.bz2`

>选项：
>>- `-x` ：解压缩`.tar.bz2`格式
>>- `-t` ：只查看不解压


### 5、关机和重启命令

#### 5.1  `shutdown`命令

命令格式： `shutdown [选项] 时间`

>选项：
>>- `-c`  ：取消当前一个关机命令
>>- `-h`  ： 关机
>>- `-r`  ：重启

#### 5.2  其他的关机命令

`halt`

`poweroff`

`init 0`

#### 5.3  其他重启命令

`boot`

`init 6`

#### 5.4 系统运行级别

>- `0` ：  关机
>- `1` ： 单用户
>- `2` ： 不完全多用户，不含NFS服务
>- `3` ： 完全多用户
>- `4` ：  未分配
>- `5` ： 图形界面
>- `6` ：  重启

`cat /etc/inittab`  ：修改系统默认运行级别

> `id:3:initdefault:`

`runlevel`  ：查询系统运行级别

#### 5.5 退出登录命令

`logout`

### 6、其他常用命令

#### 6.1 挂载命令

1》查询与自动挂载

`mount` ：查询系统中已经挂载的设备

`mount -a`  ：依据配置文件`/etc/fstab`的内容（自动挂载相关配置内容）

2》 挂载命令格式

`mount [-t 文件系统]  [-o 特殊选项] 设备文件名 挂载点`

>选项：
>
>>`-t 文件系统` ： 加入文件系统类型来指定挂载的类型，可以`ext3`、`ext4`、`iso9660`等文件系统
>>
>>`-o 特殊选项` ： 可以指定挂载的额外选项
>>
>>特殊选项：
>>>- `atime / noatime`：更新访问时间/不更新访问时间。访问分区文件时，是否更新文件的访问时间，默认为更新
>>>- `async/sync` ：异步/同步，默认为异步
>>>- `auto/noauto`：自动/手动，`mount -a` 命令执行时，是否会自动安装`/etc/fstab`文件内容挂载，默认为自动
>>>- `defaults`：定义默认值，相当于`rw`,`suid`,`dev`,`exec`,`quto`,`nouser`,`async`这七个选项
>>>- `exec/noexec`：执行/不执行，设定是否允许在文件系统中执行可执行文件，默认是exec允许
>>>- `remount`：重新挂载已经挂载的文件系统，一般用于指定修改特殊权限
>>>- `rw/ro` ：读写/只读，文件系统挂载时，是否具有读写权限，默认时`rw`
>>>- `suid/nosuid`：具有/不具有SUID权限，设定文件系统是否具有`SUID`和`SGID`的权限，默认时具有
>>>- `user/nouser`：允许/不允许普通用户挂载，设定文件系统是否允许普通用户挂载，默认是不允许，只有`root`可以挂载分区
>>>- `usrquota`：写入代表文件系统支持用户磁盘配额，默认不支持
>>>- `grpquota`：写入代表文件系统支持组磁盘配额，默认不支持

3》 挂载光盘

`mkdir /mnt/cdrom/` ：建立挂载点

`mount -t iso9660  /dev/cdrom  /mnt/cdrom/` ：挂载光盘

`mount /dev/sr0 /mnt/cdrom/`

4》 卸载命令

`umount` ： 设备文件名或挂载点

`umount /mnt/cdrom`

5》 挂载U盘

`fdisk -l`  ：查看U盘设备文件名

`mount -t  vfat /dev/sdb1 /mnt/usb/`

* 注意：Linux默认是不支持NTFS文件系统的
		

#### 6.2 用户登录查看 和 用户交互命令

1》命令格式：`w 用户名`

>查看登录用户信息。
>
>命令输出：
>>- `USER`：登录的用户名
>>- `TTY`：登录终端
>>- `FROM`：从哪个IP地址登录
>>- `LOGIN@`：登录时间；
>>- `IDLE`：用户闲置时间；
>>- `JCPU`：指的是和该终端连接的所有进程占用的时间。这个时间里并不包括过去的后台作业时间，但却包括当前正在运行的后台作业所占用的时间；
>>- `PCPU`：是指当前进程所占用的时间；
>>- `WHAT`：当前正在运行的命令

2》命令格式： `who 用户名`

>查看登录用户信息。
>命令输出：
>>- 用户名    
>>- 登录终端    
>>- 登录时间（登录来源IP地址）

3》 命令格式 ： `last`

>查询当前登录和过去登录的用户信息。
>
>`last`命令默认时读取 `/var/log/wtmp` 文件数据
>
>命令输出：
>>- 用户名   
>>- 登录终端  
>>- 登录IP    
>>- 登录时间   
>>- 退出时间（在线时间）

4》命令格式：`lastlog`

>查看所有用户的最后一次登录时间。
>
>`lastlog`命令默认时读取 `/var/log/lastlog` 文件内容。
>
>命令输出：	
>>- 用户名   
>>- 登录终端   
>>- 登录IP   
>>- 最后一次登录时间



## 二、Shell 


## 三、VI 编辑器


#License
GPL v3
