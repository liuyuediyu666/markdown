# 其他类

##### watch

watch -n 1 -d nvidia-smi（这是一个命令组合，watch -n 1后面可跟命令，-n是刷新时间，-d是高亮显示变化）

watch -n 1 free

##### ~符号指代/home/user目录（windows下默认就是**C盘/Users/用户名**）





### 

# 帮助系统

### man(按q退出)

man command







# BASH(bourne again shell)

man bash 包含很多内键的指令说明，如man cd。

~/.bash_history  # 记录着bash的历史命令

/etc/shells  # 该文件注册记录可用的shell

/etc/passwd  # 每个账号对应哪种shell

/lib/modules/$(uname -r)/kernel  # linux核心模块所在目录

/etc/profile  # linux环境变量配置文件

空格+反斜杠(用在指令尾表示换行)

ctrl+a(移动到命令头)。ctrl+e(移动到命令尾)。ctrl+u(删除到命令头)。ctrl+k(删除到命令尾)

ctrl+c(终止目前命令)。ctrl+z(暂停目前的命令)。

ctrl+s(暂停屏幕输出)。ctrl+q(恢复屏幕输出)。

ctrl+d(输入结束(EOF)，可用于退出程序)。

ctrl+m(等于enter)。

### alias

alias(查看所有别名)。

alias lm='ls -al'



### clear(清屏)



### history

history 3

ctrl+r+关键词(搜索历史命令，左右键确定，重复按ctrl+r是在该搜索条件下往前滚动查询)。







### 操作环境

##### source(读入环境配置文件，也可用小数点代替(.))

source ~/.bashrc

source /home/whl/conda/bin/activate

source 变量文件  # 激活该环境变量





# BASH变量(环境变量PATH,HOME,MAIL,SHELL)

bash环境中的数值运算仅能达到整数运算，小数将被舍去。

bash中的变量类型默认为字符串。

PATH变量：当你执行某个指令，系统会按PATH中的路径顺序搜寻指令，如果找不到，就会显示command not found。

HOME家目录

SHELL使用的是哪个shell

HISTSIZE存储的历史命令个数

MAIL邮件路径

LANG使用的字符集

RANDOM随机数，使用echo $RANDOM可取得随机数。

echo ${PATH}  # 显示变量

variable=value  # 设定或修改变量值，内容有空格可使用引号。单引号内$等为一般字符，双引号内为为特殊字符。可用(反斜杠+特殊字符)将特殊字符变为一般字符。

echo $(uname -r)  # 当指定中包含其他指令时，使用$()。

PATH=${PATH}/home/bin  # 扩增变量内容。可用"$PATH"替换${PATH} 

export  # 将自定义变量转成环境变量，因为子程序只继承父程序的环境变量，不继承自定义变量，所以共享要转为环境变量。

unset PATH  # 取消变量。

env和export都可以列出当前环境变量。

set和declare能列出所有变量，不只是环境变量。

type [-tpa] cd  # 查看指定是否为bash自带指令。对于非内置指令，还能查到目录位置，相当于which功能。

$也是变量，代表当前这个shell的PID，可用echo $$显示。

?也是变量，代表上一个指令的回传值，可用echo $?显示，0代表执行成功，上个指令执行错误会返回错误码。

read [-pt] var  # 获取用户输入的变量。-p提示内容，-t等待秒数。

declare [-aixr] var  # -a将var变为数组类型，-i将var变为整数类型，-x将var变为环境变量同export，-r将var变成只读，且不能unset。

declare +x var  # 取消var的环境变量设置，变为非环境变量。

declare -p var  # 显示var变量的类型设置。

declare -a var  # var[1]='zhangsan'这样设置数组的值，echo ${var[1]}显示数组的值。

ulimit用来限制用户资源占用，如开启文件数量，如可使用CPU时间，如可使用内存量等等。











# 进程管理与SELinux

### free(查看内存)

free [-b|-k|-m|-g|-h]

### top(查看进程)

### kill(管理背景工作)

kill [-9] PID

### lsof(列出被进程所开启的文件名)

lsof -i :8091（查看8091端口被哪个进程占用，查到PID）







# 文件与目录管理

### which

which [-a] command  # -a参数是查找所有，而不只是第一个指令文件。





### ls(支持通配符)

ll -dSr /target/*  # -d列出目标目录本身(一定要配合*通配符)-S按文件大小排序-r反向排序，也就是列出该目录所有对像并按大小排序。

ll /target1 /target2  # 支持多目标

ll | wc -l  # 统计文件个数

ll | wc -c  # 统计总的容量大小

ll -h  # 文件大小显示单位

ll -rt  # 结果按时间排序并反向排序



### cat,tac,nl,head,tail,more,less,od

cat从第一行显示。

tac从最后一行显示。

nl 显示行号。

cat | more。

ll | more(翻页查看)。ll | less(前后均可翻页)。ll | head -n 12。ll | tail -n 12。

##### tail -f file -n 22

等同于--follow=descriptor，根据文件描述符进行追踪，当文件改名或被删除，追踪停止

##### tail -F

等同于--follow=name  --retry，根据文件名进行追踪，并保持重试，即该文件被删除或改名后，如果再次创建相同的文件名，会继续追踪







### cp，scp

cp [-r] /target .

scp [-r] local_file remote@remote_ip:/home/dir



### mkdir

mkdir -p /a/b/c  # 递归创建目录



### cd

### pwd

### rm

rm -rf file





### mv

mv -r raw_file new_file







### tree

yum install tree

tree  目标目录  # 列出所有层，默认操作当前目录

tree -L 1  # 只列出第一层

tree -L 1 -C  # 加颜色

tree -L 1 -C -p  # 加权限信息

tree -L 1 -C -p -f  # 加相对路径

tree -L 3 -C -p  -d  # 只列文件夹



# 磁盘与文件系统

### df(列出文件系统的整体磁盘使用量)

df -h

### du(评估文件系统的磁盘使用量)

du -sh

du -sh *





# 压缩和解压

### gzip(zip,gzip,compress)(压缩和解压都会删除原文件)

-c：将压缩数据输出到屏幕

-d：解压缩

-t：

-v：显示压缩比

-#：压缩等级，默认-6

gzip -9 -c target > aim.gz  # 将target压缩到aim.gz，不删除源文件(>的重定向功能)。

zgrep -n 'str' target.gz  # 查找.gz中的'str'，不用解压，-n显示行数。

zcat：查看gz中的文本(zcat/zmore/zless对应cat/more/less)

znew命令可将compress压缩成的.Z文件转成gzip格式。

### bzip2(压缩比高于gzip)

-c：将压缩数据输出到屏幕

-d：解压缩

-k：保留源文件

-z：压缩的参数（默认值，可以不加）

-v：显示压缩比

-#：压缩等级，默认-6

### tar

-c(建立打包文件)。-t(查看包文件内容)。-x(解包)。

-z(.tar.gz)。-j(.tar.bz2)。-J(.tar.xz)。

-v(显示过程)。

-f(待解压包名)(将打包名称)。

-C(指定解包目录)。

-p(保留原本文件的权限与属性)。

tar -zcv -f 将打包名称 目录1 目录2 目录3

tar -ztv -f 待查看包名

tar -zxv -f 待解压包名 -C 指定解压目录  # 默认解压到当前文件夹

tar -zxv -f 目标压缩包 某个文件  # 这种只解压个别文件的方法，不能使用-C参数。

下面的命领是打包/my目录下所有文件，但排除etc开头的文件，以及包本身name.tar.gz。

tar -zc -f /my/name.tar.gz --exclude=/my/etc* --exclude=/my/name.tar.gz /my

tar -zc -f /my/name.tar.gz --newer-mtime='20210131' /home/*  # 打包31号以后的文件

### zip

zip -q -r html.zip /home/html  # -q是静默 -r是递归目录

zip -d html.zip x/y/z/a.txt  # 从html.zip中删除x/y/z/a.txt文件

unzip -n或-o html.zip -d /tmp  # -n不覆盖-o覆盖-d目标目录，默认当前目录

unzip -v html.zip  # 不解压只查看压缩文件目录信息

unzip -l html.zip  # 相对-v信息更少，只有文件名和时间和大小

unzip file.zip  # 直接解压到当前目录

cat text.z* > testall.zip 然后 unzip testall.zip  # 对分卷压缩包合并然后再解压。

# 账号管理

linux系统的所有账号保存在/etc/passwd文件中

### su

su(su root)  # 切换到root，目录不变。如果是(su -)则切换到/root目录

su - user  # 切换到user

### sudo

### w

### who(显示登录者)

### last(显示登录记录)

### lastlog





# vim

vim撤销一步 u







# 其他待分类

ifconfig（网卡信息）

ip a（网卡信息）

time  # 命令前面加time可显示程序运作时间。

find /etc -newer /etc/passwd  # 查找所有比passwd新的文件

yum list installed somename  # 安装软件

ps -ef | grep jupyter

file + 文件或文件夹，可返回文件类型相关信息。

useradd [－d home] [－s shell] [－c comment] [－m [－k template]] [－f inactive] [－e expire ] [－p passwd] [－r] name

wget命令

which 查看可执行文件的位置。
whereis 查看文件的位置。 
locate  配合数据库查看文件位置。
find  实际搜寻硬盘查询文件名称。



##### 鸟哥私房菜整理



查所有变量：set

declare 

echo ${$}：$代表目前这个shell的线程代号，即PID。

echo${?}：上一个指令回传值。

type -a ls，查看指令的搜索顺序。

##### 上传下载

sz 文件名：将指定的文件下载到本地机器，会弹出窗口指定下载路径。

rz -E：会弹出窗口，选择文件上传到远程机器。直接拖到xshell也有同样效果。





##### grep(后面可加引号也可不加引号)

cat | grep

ll | grep

find | grep

##### 窗口滚动

linux执行命令时，用滚轮翻页会不停跳到当前行更新内容，用[shift] + pageup可解决

##### linux一个看不懂的命令

find / -type d -iname cuda 2>&1 | grep -v 'Permission denied'









# 待处理

##### 关于nohup &的用法

https://www.cnblogs.com/baby123/p/6477429.html

##### 如何给linux增加回收站功能

https://www.cnblogs.com/qzqdy/p/9299595.html

##### linux换源需要系统学习一下

##### GCC相关

https://gcc.gnu.org/

https://gcc.gnu.org/onlinedocs/libstdc++/manual/abi.html

##### linux目录结构，重点文件位置，作用

##### linux环境配置

##### 发行版介绍

Redhat系列：Redhat、Centos、Fedora等

Debian系列：Debian、Ubuntu等

Redhat系列
1、常见的安装包格式为：rpm包，安装rpm包的命令是：rpm-参数
2、包的管理工具：yum
3、支持tar包

Debian系列
1、常见的安装包格式为：deb包，安装deb包的命令是：dpkg-参数
2、包的管理工具：apt-get
3、支持tar包

##### 阮一峰分享的linux命令窗口空间，比xshell窗口好用

http://www.ruanyifeng.com/blog/2019/10/tmux.html