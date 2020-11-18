ipython官网，里面有jupyter相关文档。

https://ipython.readthedocs.io/en/stable/index.html#

### 显示帮助信息

``````
jupyter notebook --help
``````

### 在conda环境中安装jupyter kernel，这样就可以在jupyter中使用这个环境了。还可以有个图标放在launcher页面。

```
conda activate 环境名  # 激活将要安装jupyter kernel的环境
pip install ipykernel  # 安装jupyter kernel
python -m ipykernel install --name 环境名 --display-name 显示名  # 显示名称可选，是在jupyter的launcher中显示的名称
```

### 显示可用的jupyter kernels

``````
jupyter kernelspec list
``````

### jupyter配置文件：设置默认的启动路径和启动方式lab或notebook

``````
jupyter notebook --generate-config  # 若没有jupyter_notebook_config.py则会生成，若有则用默认值覆盖（询问确认的时候会显示该文件的路径）
``````

路径设置：修改以上文件中的c.NotebookApp.notebook_dir = '我想要的路径'。

启动方式设置：修改以上文件中的c.NotebookApp.default_url = '/lab'，如果改回以notebook启动，则使用'/tree'替换'/lab'。

### 在服务器上启动jupyter

用whl账号登录linux服务器，在conda的base环境下，cd到/home/whl目录下，执行下列命令。  

jupyter lab --ip 0.0.0.0 --port 8888 （在xshell中启动，xshell断掉就停了）  

nohup jupyter lab --ip 0.0.0.0 --port 8888 & （后台启动，不会受到xsell关闭的影响）  