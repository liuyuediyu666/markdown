创建环境的命令参数需了解一下

conda create -n open-mmlab python=3.7 -y

anaconda原理，文件结构，安装包位置，主要命令

# conda

conda # 可以输出常用命令

conda --help  

conda info  # 列出conda当前一些基本信息

conda info -e  # 查看已有conda环境

conda info --help

conda create --help

conda create -n whlenv

conda install -c 

conda install -c conda-forge jupyterlab

conda --version或conda -V   #查看版本

conda activate whl  #激活环境

conda list  # 查看当前环境下已安装的包

conda deactivate  # 反激活环境

##### 在linux下需要用source命领激活conda才能启动conda命令

启动conda地址(source /home/conda/bin/activate)

### clone一个conda环境，将目录/conda/envs/下的whl/克隆到另一个服务器
cd /home/workflow/conda/envs   # 进入目录

zip -r whl200831.zip whl/ 压缩文件夹   # 压缩该环境文件

scp whl200831.zip root@automlgpu6:/home/workflow/conda/envs   # scp是跨服务器copy，后面是服务器地址及目录

然后cd到另一个服务器的/home/workflow/conda/envs目录，解压上面的压缩包

确认对应环境中的/home/workflow/conda/bin/pip文件中最上面路径指向/home/workflow/conda/bin/python  





# pip

vim ~/.pip/pip.config  # 这是pip配置文件

pip install pk -i https://pypi.tuna.tsinghua.edu.cn/simple --default-time=100

pip install --upgrade pk --ignore-installed pk

