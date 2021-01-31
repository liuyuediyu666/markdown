conda文档：https://docs.conda.io/en/latest/

创建环境的命令参数需了解一下

conda create -n open-mmlab python=3.7 -y

anaconda原理，文件结构，安装包位置，主要命令



启动conda环境的同时，激活其中一个环境。

source /home/workflow/conda/bin/activate 环境名称



##### 关于如何直接拷贝移植conda环境

https://blog.csdn.net/qq_41554005/article/details/89052435



# conda源的管理

查看目前的源

conda config --show channels

清除源，恢复默认

conda config --remove-key channels

添加源

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/ 

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/ 

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/ 

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/ 

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/ 

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge  

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/



### 一个问题处理技巧，未验证。

如果出现conda uninstall失败的情况，可以直接在site-packages目录下，将该包的安装目录及其对应的distinfo或egginfo目录直接删除，也可达到卸载包的效果。



# conda

conda # 可以输出常用命令

conda --help  

conda info  # 列出conda当前一些基本信息

conda info -e  # 查看已有conda环境

conda info --help

conda create --help

conda create -n whlenv python=3.6  # 创建环境并指定python版本

conda remove  -n whlenv --all  # 删除某环境

conda install -c 

conda install -c conda-forge jupyterlab

conda --version或conda -V   #查看版本

conda activate whl  #激活环境

conda list  # 查看当前环境下已安装的包

conda deactivate  # 反激活环境

##### 重命名环境(conda 其实没有重命名指令，是通过clone完成的，分两步)

conda create -n newenv --clone oldenv  # 先clone一份新的环境

conda remove -n oldenv  # 再删除旧的环境

##### 在linux下需要用source命领激活conda才能启动conda命令

启动conda地址(source /home/conda/bin/activate)

### clone一个conda环境，将目录/conda/envs/下的whl/克隆到另一个服务器
cd /home/workflow/conda/envs   # 进入目录

zip -r whl200831.zip whl/ 压缩文件夹   # 压缩该环境文件

scp whl200831.zip root@automlgpu6:/home/workflow/conda/envs   # scp是跨服务器copy，后面是服务器地址及目录

然后cd到另一个服务器的/home/workflow/conda/envs目录，解压上面的压缩包，解压目录名就是该环境名称。

注意解压后的环境下的一个文件vim /conda/envs/dz2/bin/pip，第一行的路径应指向/conda/envs/dz2/bin/python，改过来即可。





# pip

vim ~/.pip/pip.config  # 这是pip配置文件

pip install pk -i https://pypi.tuna.tsinghua.edu.cn/simple --default-time=100

pip install --upgrade pk --ignore-installed pk



pip show autokeras  # 显示包信息



### pip安装包与conda环境，具体细节待研究。

pip -V可以查看当前pip版本的pip路径。如果路径与当前激活的conda环境不一致，会导致pip安装过的包不在当前conda环境中，也就不能使用。这时可以deactivate和activate重新激活一下conda环境。再使用pip -V查看pip所属环境应该就正常了。





