# linux

linux目录结构，重点文件位置，作用

linux环境配置

linux一个看不懂的命令

find / -type d -iname cuda 2>&1 | grep -v 'Permission denied'

linux环境变量设置是下面的文件/etc/profile

GCC相关

https://gcc.gnu.org/

https://gcc.gnu.org/onlinedocs/libstdc++/manual/abi.html

~符号指代home目录（windows下默认就是**C盘/Users/用户名**）





### linux窗口操作相关

clear

history

ctrl + R + 关键词。 搜索历史命令。左右键确定。重复按ctrl + R 上滚。

##### tail命令

tail -f

等同于--follow=descriptor，根据文件描述符进行追踪，当文件改名或被删除，追踪停止

tail -F

等同于--follow=name  --retry，根据文件名进行追踪，并保持重试，即该文件被删除或改名后，如果再次创建相同的文件名，会继续追踪

tailf

等同于tail -f -n 10（貌似tail -f或-F默认也是打印最后10行，然后追踪文件），与tail -f不同的是，如果文件不增长，它不会去访问磁盘文件，所以tailf特别适合那些便携机上跟踪日志文件，因为它减少了磁盘访问，可以省电

常用操作

此时要想暂停刷新，使用【Ctrl】+【S】暂停终端。

若想继续终端，使用【Ctrl】+【Q】。

若想退出tail命令，直接使用【Ctrl】+【C】。

##### top命令

top有很多种用法。

##### file

file + 文件或文件夹，可返回文件类型相关信息。

##### free

查看内存使用情况

##### source ~/.bashrc

很常用

##### watch -n 1 nvidia-smi（这是一个命令组合）

watch -n 1 -d 是每隔一秒查看一次某命令的执行结果 -d是高亮显示有变化的项。

nvidia-smi就是查看显卡状态。

##### 窗口滚动

linux执行命令时，用滚轮翻页会不停跳到当前行更新内容，用[shift] + pageup可解决

##### tail

tail -f 文件名，监视文件的最后内容更新。







##### 上传下载

sz 文件名：将指定的文件下载到本地机器，会弹出窗口指定下载路径。

rz -E：会弹出窗口，选择文件上传到远程机器。直接拖到xshell也有同样效果。



##### 压缩解压

unzip test.zip 解压到当前目录

unzip -n test.zip -d /tmp 解压到指定目录（-n表示不覆盖已存在的同名文件）。

unzip -o test.zip -d /tmp 解压到指定目录（-n表示覆盖已存在的同名文件）。

unzip -v test.zip 查看压缩文件目录，但不解压。

分卷文件解压

第一步合并文件 cat text.z* > testall.zip

第二步解压：unzip testall.zip



linux其他解压命令

https://www.cnblogs.com/cxhfuujust/p/8193310.html









### 其它

linux换源需要系统学习一下

ifconfig（网卡信息）

ip a（网卡信息）

ls（）

ll（）

mkdir /asdf（）

mkdir -p /asdf/qwe/zxc（递归创建目录）

ll | grep 'abc'（查找目录中包含abc关键字，没引号也行）

su - 用户名(su - 切换到超级用户)（su root 切换到root用户）

cat filename（查看文件内容）

cd

pwd

watch -n 1 nvidia-smi（打开GPU监控面板，n=1秒1次）

lsof -i :8091（查看8091端口被哪个进程占用，查到PID）

kill 11234（用PID11234杀死进程）

kill-9 11234（-9强制杀死）

sudo kill -9 PID（需要sudo权限时使用）

source /home/workflow/conda/bin/activate（source命令的用法可以百度一下）

cp -r raw_file new_file

zip -r name.zip raw_file

mv -r raw_file new_file

rm -rf filename

vim filename

ll | wc -l（返回统计文件数量）

ll -rt（结果反向排序）

useradd [－d home] [－s shell] [－c comment] [－m [－k template]] [－f inactive] [－e expire ] [－p passwd] [－r] name

##### df和du相关命令

df --help

df -h

du --help

du -sh

du -sh *

wget命令

##### 关于nohup &的用法

https://www.cnblogs.com/baby123/p/6477429.html



which 查看可执行文件的位置。
whereis 查看文件的位置。 
locate  配合数据库查看文件位置。
find  实际搜寻硬盘查询文件名称。

# vim

vim撤销一步 u





# 鸟哥私房菜整理

linux

su然后输入密码，目录不变。

su - 然后输入密码，目录切换到/root。

linux系统的所有账号保存在/etc/passwd文件中

~/.bash_history记录着bash的历史命令

HISTSIZE可以设定历史记录数量

ll /root/*abc* ，支持通配符。

man 指令，调出帮助文档

type 指令，查类型，对于非内置指令，还能查到目录位置，相当于which功能

ctrl+u、k、a、e。光标操作

echo ${变量名}

环境变量：PATH,HOME,MAIL,SHELL

扩增变量：PATH=${PATH}:/home/bin

在子程序使用变量（升级为环境变量）：export PATH

取消变量：unset 变量名

查环境变量：env或export

查所有变量：set

declare 

echo ${$}：$代表目前这个shell的线程代号，即PID。

echo${?}：上一个指令回传值。

ll | more：一页一页看。

ll | less

ll | head

ll | tail

alias查看所有别名。

type -a ls，查看指令的搜索顺序。

source也可用.来代替

last 查看linux的用户登录记录。