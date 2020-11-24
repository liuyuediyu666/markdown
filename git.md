工作区(working tree)、暂存区(index或stage)、版本库、HEAD（游标）。暂存区属于版本库一部分。版本库在.git文件夹中。

.git文件夹中的refs文件夹保存的是remote命令配置的远程库信息。

.git文件夹中的FETCH_HEAD文件是git fetch命令保存的文件，未执行没有该文件。

一页显示不完时：q退出，h进入帮助页面。

一台机器只要生成一个密钥？

修改同一个文件也不一定冲突，只要两个修改隔了大概7行以上。7待确定。

文档最后一行最好是空行，就是如果本行有内容则回车到下一行且没有内容。

##### clone时https与git区别

git clone https://github.com/account/repository

git clone git@github.com:account/repository

第一种首次下载无需设置，可直接下载，但提交到远端时要进行设置

第二种下载时就要设置，具体可能是（user.name,user.email,密钥，具体还要验证）以后提交到远端直接提交即可

以上方式只能clone主分支，也就是master分支。clone其他分支见后面branch部分。

##### git中一些选项解释

-d --delete：删除

-f --force：强制 

-D --delete --force的快捷键

-m --move：移动或重命名 

-M --move --force的快捷键 

-r --remote：远程

 -a --all：所有 

##### 删除远程仓库文件的正确姿势（要用git rm）

仅在文件夹中右键删除文件，再进行add,commit,push，并不会删除远端仓库对应文件。正确操作如下：

第1步：git ls-tree HEAD：查看目前所有文件，包含右键删除的文件。

第2步：git rm file：在工作区删除文件并提交到暂存区，相当于两步骤合并，rm+git add。

第3步：git commit -m asdf：提交到分支。

第4步：git push origin master:master：将删除操作同步到远程仓库。

##### 显示HEAD文件列表

git ls-tree HEAD

##### 当前节点的祖宗节点如下：

^x: 尖头符号，形似箭头，表示要朝那个方向，始终是走一步，x 表示第几个岔路口，代表方向盘

~y: 波浪符号，表示要在该方向上走 y 步，始终沿着该方向，代表油门

自己: HEAD, HEAD^0 或 HEAD~0

父亲: HEAD^, HEAD~

母亲: HEAD^2

爷爷: HEAD^~, HEAD~2, HEAD^^

奶奶: HEAD^^2, HEAD~^2

姥爷: HEAD^2~, HEAD^2^

姥姥: HEAD^2^2

##### git help

##### git help -a

##### git help -g

先大体熟悉有哪些命令

##### git init

创建Git版本库时，Git自动创建master分支，且head指向master。

##### git config

##### git config --global user.name wanghonglei

##### git config --global user.email 2818@qq.com

##### git config -l

##### git config --local user.name wanghonglei

##### git config --local user.email 28q.com

##### git config --get user.name

##### git config --get-all user.name

参数分为全局和局部，可以用git config熟悉有哪些命令

##### git config core.ignorecase

简写，查询某配置

##### git config user.name wanghlanother

简写，更改某配置





### 远程仓库

#####  ssh key设置

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。

如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key： 

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

 你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。 

 如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。 

加密传输：数据接收方创建公钥和私钥。公钥加密后的文件发出去，只有私钥可以解密。

签名：数据发布方用私钥加密，大家可以用公钥确认是否私钥持有方发布的。

在这里用于确认上传代码人的身份，只有保存了公钥才能上传代码。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容

第3步：在右上角找到“Create a new repo”按钮，创建一个新的仓库：在Repository name填入仓库名其他默认



##### git remote add origin 2818qq.com:wanghonglei/some.git

将一个已有的本地仓库与之关联，origin是远程库的名字，可自定义。后面可将本地仓库推送到远端。这种关联无论成功与否都不返回信息。

##### git remote

##### git remote -v

显示所有关联的远程仓库

##### git remote show [remote]

显示远程仓库关联的详细信息

##### git remote rm name

删除与远程仓库的关联

##### git remote rename old_name new_name

重命名与远程仓库的命名





##### git push origin master:master

必须远端添加了公钥才可以push。

git push <远程主机名>  <本地分支名>:<远程分支名>

如果push冲突，可以先pull来来，手动合并解决冲突，再push。

##### git push origin master

如果本地分支名与远程分支名相同，则可以省略冒号

##### git push --force origin master:master

如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数

##### git push origin --delete master

删除远程主机分支可以使用 --delete 参数，以上命令表示删除 origin 主机的 master 分支： 





##### git fetch origin

获取远程origin仓库的所有branch的最新commit，并记录到.git/FETCH_HEAD文件

##### git fetch origin master

获取远程origin仓库的指定分支（此例是master）的最新commit，并记录到.git/FETCH_HEAD文件

##### git fetch origin master:local_branch_name

除了获取远端该分支（master）的最新commit，还在本地创建local_branch_name分支来保存其数据。

##### git log -p FETCH_HEAD

查看取回的FETCH_HEAD，是该branch在服务器上的最新状态，包括更新信息。 可以看到返回的信息包括更新的文件名，更新的作者和时间，以及更新的代码（19行红色[删除]和绿色[新增]部分）。  我们可以通过这些信息来判断是否产生冲突，以确定是否将更新merge到当前分支。  



##### git merge origin/branch

注意此处merge的是fetch过的远端版本。

##### git merge FETCH_HEAD（等同上面命令）

将远程origin仓库中的任何更新合并到当前分支

##### git fetch --all

将远程所有分支信息获取到本地。

##### git reset --hard origin/master

在git fetch --all的基础上，将获取到的远程origin仓库的master分支信息合并到本地，这样本地已删除的文件也能从远端下载下来。如果没有fetch或者fetch之后的修改，这里的命令对远端的数据是无效的。





##### git pull origin master:brantest

git pull <远程主机名>  <远程分支名>:<本地分支名>

将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并 

git pull 其实就是git fetch和git merge FETCH_HEAD两个命令的合并简化。不过有一点区别要注意，对于本地删除的文件，git pull是无效的

##### git pull origin master

如果远程分支是与当前分支合并，则冒号后面的部分可以省略 



##### git branch（git branch -l）

查看本地所有分支

##### git branch -r

查看远程所有分支

##### git branch -a 

查看本地和远程的所有分支

##### git branch dev

创建分支

##### git branch -d dev

删除本地分支

##### git branch -d -r dev

##### git push origin:dev

两条命令一起执行，第一条删除本地和远端分支，第二条将这个删除命令推送到远端服务器，使远端也执行删除。

##### git branch -m oldbranch newbranch

重命名本地分支。如果重命名远程分支，首先要删除远程分支，再push本地新分支到远程。

##### git switch(checkout) dev

##### git switch -c dev(git checkout -b dev)

创建并切换分支

##### git branch dev_local origin/dev

##### git switch(checkout) dev_local

##### （git checkout -b dev_local origin/dev）

clone远端origin的dev分支，并在本地取名dev_local，再切换到该分支。后面括号一步完成。

##### git clone -b <指定分支名> <远程仓库地址> 

clone的时候直接指定分支





#####  git branch --set-upstream-to=origin/master  master  

使本地分支master追踪到远端origin分支master上，当本地和远程分支名相同，可简写为git pull和git push。

##### git push -u origin master

如果第一次推送，加-u可以自动将本地master分支和远程master分支关联，相当于git branch --set-upstream-to命令。这种方式用于远程库没有分支时，先推送再关联。

##### git branch -v

可以查看本地分支的最新commit信息

##### git branch -vv

除了查看本地分支的最新commit信息，还可查看本地分支与远端分支的追踪详细信息。





### 提交合并

##### git add .

##### git add file1  file2

##### git commit -m anywords

##### git merge dev

合并某分支到当前分支







### 对比查看

##### git diff [file1 file2]

查看工作区与暂存区变化。新file（也就是只有工作区才有的file）diff追踪不到。

##### git diff --staged [file1 file2]（git diff --cached）

查看暂存区与当前版本变化

##### git diff HEAD [-- file1 file2]

查看工作区与当前版本变化

##### git diff FETCH_HEAD

查看本地工作区与FETCH_HEAD的区别

##### git diff master dev  [file1 file2]

 以master分支为参照，比较dev分支和master分支之间的差异。 都是版本库的。

#####  git diff fde17e9 4700e4a [file1 file2]

用commit id来进行不同分支的比较效果同上，同时也能进行版本库中历史版本间的比较。

##### git status

##### git log

##### git log --pretty=oneline

版本号是SHA1结果的16进制表示，git会反它们自动串成一条时间线

##### git log --oneline

版本号只显示前几位

##### git reflog

记录每一次命令



### 恢复

##### git checkout -- file

首先尝试从暂存区覆盖工作区文件，若暂存区无此文件，则从最新版本覆盖工作区文件。覆盖后无法恢复。

##### git reset HEAD [file1 file2]

恢复暂存区与最新版本一致，将工作区的add操作取消。

##### git reset --hard HEAD^

将当前分支版本回退到上个版本，HEAD^表示上个版本，依此类推HEAD^^ HEAD~100。

##### git reset --hard commitid

同上，直接使用commitid更直接

##### --soft --mixed --hard。如果没有给出，则默认是--mixed

##### 注意：git reset HEAD^实际是git reset --mixed HEAD^的缩写，这与git reset HEAD有效大区别，前者是将分支回退一个版本，后者是恢复暂存区与最新版本一致。

使用`--soft`参数将会仅仅重置`HEAD`到指定的版本，不会修改index和working tree 

使用`--mixed`参数与--soft的不同之处在于，--mixed修改了index，使其与第二个版本匹配。index中给定commit之后的修改被unstaged。 

使用`--hard`同时也会修改working tree，也就是当前的工作目录，如果我们执行`git reset --hard HEAD~`，那么最后一次提交的修改，包括本地文件的修改都会被清楚，彻底还原到上一次提交的状态且无法找回。所以在执行`reset --hard`之前一定要小心。









参考知乎：git pull与git fetch区别

https://zhuanlan.zhihu.com/p/123370920

##### 实用小贴士

内建的图形化 git：gitk

彩色的 git 输出：git config color.ui true

显示历史记录时，每个提交的信息只显示一行：git config format.pretty oneline

交互式添加文件到暂存区：git add -i
