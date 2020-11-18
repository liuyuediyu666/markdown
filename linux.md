# linux

linux目录结构，重点文件位置，作用

linux环境配置

linux一个看不懂的命令

find / -type d -iname cuda 2>&1 | grep -v 'Permission denied'

linux环境变量设置是下面的文件/etc/profile

GCC相关

https://gcc.gnu.org/

https://gcc.gnu.org/onlinedocs/libstdc++/manual/abi.html



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

##### 关于nohup &的用法

https://www.cnblogs.com/baby123/p/6477429.html