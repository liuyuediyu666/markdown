### 基本概念

##### 工作区（Working Directory）

##### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。 



##### 一页显示不完时：q退出，h进入帮助页面。



##### git help

##### git help -a

##### git help -g

先大体熟悉有哪些命令



##### git clone existsadress

只能clone整个仓库



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



##### git add .

##### git add file1  file2

##### git diff [file1 file2]

查看工作区与缓存区变化。新file（也就是只有工作区才有的file）diff追踪不到。

##### git checkout -- file

首先尝试从缓存区覆盖工作区文件，若缓存区无此文件，则从版本库覆盖工作区文件。覆盖后无法恢复。





##### git commit -m anywords

##### git diff --staged [file1 file2]（git diff --cached）

查看缓存区与版本库变化

##### git diff HEAD [-- file1 file2]

查看工作区与版本库变化

 

##### git status

##### git log

##### git log --pretty=oneline

版本号是SHA1结果的16进制表示，git会反它们自动串成一条时间线

##### git log --oneline

版本号只显示前几位



##### git reset --hard HEAD^

HEAD^表示上个版本，依此类推HEAD^^ HEAD~100。

##### git reset --hard commitid

`--hard`参数有啥意义？这个后面再讲，现在你先放心使用。



##### git reflog

记录每一次命令



##### git reset HEAD [file1 file2]

把暂存区的修改回退到工作区，也就是恢复暂存区与版本库一致，将add操作取消，此时







##### rm [file1 file2]

此时可从缓存区恢复到工作目录，git checkout -- file

从来没有被添加到版本库就被删除的文件，是无法恢复的！ 

##### git add [file1 file2]

此时可从版本库恢复到缓存区，git reset HEAD file

##### git rm [file1 file2]

在工作区删除文件，并提交到缓存区，相当于上面两步骤合并，rm+git add

##### git commit -m asdf

最终从版本库删除文件





##### git branch dev

##### git branch

##### git switch(checkout) dev

##### git switch -c dev(git checkout -b dev)

创建变切换分支

##### git merge dev

合并某分支到当前分支

##### git branch -d dev

删除分支

#####  git diff master dev  [file1 file2]

 以master分支为参照，比较dev分支和master分支之间的差异。 都是版本库的。

#####  git diff fde17e9 4700e4a [file1 file2]

用commit id来进行不同分支的比较效果同上，同时也能进行版本库中历史版本间的比较。









### 远程仓库

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

将一个已有的本地仓库与之关联，origin是远程库的名字，可自定义。后面可将本地仓库推送到远端



##### git push -u origin master

必须远端添加了公钥才可以推送。第一次推送加-u，将本地master分支和远程master分支关联。 在以后的推送或者拉取时就可以简化命令。 现在GitHub页面中看到远程库的内容已经和本地一模一样。



##### git push origin master

从现在起只要本地作了提交，就可以通过这个命令同步，真正的分布式版本库！



##### git remote

##### git remote -v







