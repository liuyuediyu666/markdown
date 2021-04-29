docker cp   filename id:/home

docker commit ???





### 一些报错处理：

##### 启动容器或其他操作时会报错

https://blog.csdn.net/weixin_42273374/article/details/82223640



### 本地保存和加载镜像

```shell
docker save imagename | gzip > savename.tar.gz
docker load -i savename.tar.gz
```





# 安装

如果已有安装好的，需要先卸载旧的docker，以及相关的依赖。

```
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### 使用repository方法安装

#### 设置 REPOSITORY

换源，使用网易的镜像。vim /etc/docker/daemon.json.rpmsave

将文件内容改为以下内容：{"registry-mirrors" : ["http://hub-mirror.c.163.com"]}

安装`yum-utils` package(提供 `yum-config-manager` 工具)并且设置**stable**  repository

```
$ sudo yum install -y yum-utils( device-mapper-persistent-data lvm2)这两个包官网未要求安装

官方源
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
阿里云源
$ sudo yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
清华大学源
$ sudo yum-config-manager \
    --add-repo \
    https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/centos/docker-ce.repo
```

#### 安装 DOCKER ENGINE-community

1. 安装最新版本docker engine和containerd

```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

 If prompted to accept the GPG key, verify that the fingerprint matches `060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35`, and if so, accept it. 

docker 已安装但未启动，docker组已创建，但没有用户加入到docker组中。

2. 启动docker

   ```
   $ sudo systemctl start docker
   ```

3.  验证docker enging正确安装，执行`hello-world` image. 

   ```
   $ sudo docker run hello-world
   ```

   以下命令下载一个测试image并反回一个container。但container执行，他打印一条信息并退出。

#### 安装 nvidia-container-runtime

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.repo | sudo tee /etc/yum.repos.d/nvidia-docker.repo
yum install -y nvidia-container-runtime
```









## docker常用命令

##### 1.常用

systemctl start docker 启动docker

systemctl stop docker 启动docker

systemctl restart docker 重启docker

docker info 查看相关信息

docker version 查看相关信息

docker --version 查看相关信息

docker system df 镜像容器总数统计及占用的空间





#### 2.image

docker images 镜像列表

docker image rm [image name] 删除

docker image pull library/hello-world

docker search mmdetection





#### 3.container

docker ps -a  容器列表

docker container ls --all 容器列表

docker container kill [container ID] 停止容器

docker rm [-f强制删除运行态的容器] [container ID] 删除一个处于终止状态的容器 

docker container rm  [-f强制删除运行态的容器] [container ID] 删除一个处于终止状态的容器 

docker container prune 删除所有已停止的容器

docker container stop [container ID or NAMES] 终止一个运行态的容器

docker container start [container ID or NAMES] 启动一个终止态的容器

docker container restart [container ID or NAMES] 终止一个运行态的容器，然后再重新启动它。 



docker run -dit --gpus all --name detecta -p 2222:22 registry.cn-shanghai.aliyuncs.com/tcc-public/mmdetection:pytorch1.4-cuda10.1-py3

docker run  --rm：这个参数是说容器退出后随之将其删除

docker run -d  后台运行容器

docker container logs [container ID or NAMES] 打印后台运行容器的日志

docker exec -it [container ID or NAMES] bash 进入后台运行的容器。如果从这个 stdin 中 exit不会导致容器的停止。推荐exec方法。

docker commit --author wanghl --message updatammcv mm_d1 vi/mmdet:whl





#### 4.volume

docker volume create myfirst

docker volume ls

docker volume inspect myfirst

docker volume rm myfirst

docker cp 宿主机文件 容器名称:容器目录（docker cp VOCdevkit mm_prj:/mmdetection/data/）







挂载目录

```python
$ docker run -d -P \
    --name web \
    # -v my-vol:/wepapp \
    --mount source=my-vol,target=/webapp \
    training/webapp \
    python app.py
```

```python
$ docker run -d -P \
    --name web \
    # -v /src/webapp:/opt/webapp:ro \
    --mount type=bind,source=/src/webapp,target=/opt/webapp,readonly \
    training/webapp \
    python app.py
```

```python
$ docker run --rm -it \
   # -v $HOME/.bash_history:/root/.bash_history \
   --mount type=bind,source=$HOME/.bash_history,target=/root/.bash_history \
   ubuntu:17.10 \
   bash
```





conda update -n base -c defaults conda

conda install pytorch==1.6.0  -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/linux-64/

```
conda install pytorch cudatoolkit=10.1 torchvision -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/linux-64/
```



docker容器占用空间特别大解决办法overlay

https://blog.csdn.net/weixin_32820767/article/details/81196250





# docker参考材料

朱江分享教程

https://www.qikqiak.com/k8s-book/

docker中文（FAQ部分不错）

https://www.docker.org.cn/index.html

docker官网（详细）

https://docs.docker.com/

docker官方blog（关于版本改进）

https://www.docker.com/blog/

docker github

https://github.com/docker

**docker研究生分享**

https://tianchi.aliyun.com/competition/entrance/231759/tab/174?spm=5176.12586973.0.0.243239e1Es9bI6

上面链接一直看到第三步。pull一个image下来

然后创建docker容器

docker run -ti --gpus all --name [your name] -p 2222:22 registry.cn-shanghai.aliyuncs.com/tcc-public/pytorch bash

-p是把创建的docker容器挂在某个端口，这个指令里面是2222:22，如果以后要开多个容器，你可以改成2223 2224都可以

以下是阿里云提供的镜像，你进去之后要更新 apt-get update一下。

registry.cn-shanghai.aliyuncs.com/tcc-public/mmdetection:pytorch1.4-cuda10.1-py3

**docker search全网最细mmdetection使用**

https://zhuanlan.zhihu.com/p/101263456?from_voters_page=true

**docker hub**

https://www.cnblogs.com/csnd/p/12061837.html

**其他**

老哥分享（可作为入门了解）

http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html

中文

http://www.dockerinfo.net/document

根文件系统（有助于理解docker的原理）

https://www.cnblogs.com/kelamoyujuzhen/p/11541495.html

docker中的gpu注册报错问题

https://blog.csdn.net/BigData_Mining/article/details/104991349