ipython官网，里面有jupyter相关文档。

https://ipython.readthedocs.io/en/stable/index.html#

### 显示帮助信息

``````
jupyter
jupyter -h
jupyter notebook --help
jupyter notebook --help-all
jupyter kernel --help-all

jupyter --version
jupyter notebook list
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

### 关于jpynb导出为md文件

一种是linux下执行命令（jupyter nbconvert --to md notebook.ipynb），一种是用jupyter notebook可以导出md











# jupyter

- 非编辑模式下：  
  B 向下新建 A 向上新建   
  X 剪切 V 粘贴 C 复制   
  Shift+Ctrl+-切割 Shift+M合并(先选中，可以用Shift+箭头)  
  F 查找替换  
  Ctrl + F 在cell内搜索，或全局搜索  
  设置标题大小，数字键1-6  
- 模式： Code-y MarkDown-m Raw-r
- jupyter notebook配置默认启动路径  
  打开Anaconda Prompt，输入jupyter notebook --generate-config，获得jupyter_notebook_config.py文件的路径  
  打开jupyter_notebook_config.py文件，找到##The directory to use for notebooks and kernels.，设置c.NotebookApp.notebook_dir = '设置路径'  
  右击jupyter notebook图标，点击属性，找到目标（T），将路径最后的%USERPROFILE%删掉。

- 编缉模式下  
  Ctrl  + Enter     运行当前Cell，选中当前Cell  
  Shift + Enter     运行当前Cell，选中下一个Cell  
  Alt   + Enter     运行当前Cell，创建新的Cell并进入编辑模式  
  Ctrl + /          批量注释与取消注释  
  Tab               代码提示  
  Shift + Tab       查看函数帮助文档（点击加号可以看详细内容）  
  pageup/pagedown  光标移动到cell头cell尾  
  home/end(Alt + left/right)  光标移动到行首/尾  
  按住Alt拖动鼠标              多行编辑、矩形选框  
  按住Ctrl在多个位置点击鼠标    多处同时编辑  
- 魔法命令规律  
  单个百分号表示对这一行有效，放在单行行首  
  两个百分号表示对这一个Cell有效，放在Cell最开头，单独一行  
- 统计程序运行时间  
  %%time  
  import time  
  for i in range(3):  
    》》%time time.sleep(0.1)  
  for j in range(2):  
    》》%time time.sleep(0.2)  
- matplotlib绘图，一个notebook中只需要运行一次，则之后用matplotlib库作图不需要plt.show()即可把图展示出来。  
  %matplotlib inline  
- 运行py文件，就相当于把文件中的代码复制过来跑一遍。文件中导入的库、定义过的变量、函数都会进入到notebook的环境中，这和import不同。  
  %run hello.py  
- 调用系统命令，在前面加一个！在linux系统中，则可以使用!ls或!wget等命令。也可以用%%bash运行整个Cell的shell命令。  
  !pwd  
  !dir  
- 导入模块自动更新。对自己模块修改后重新import是无效的，而每次reload非常麻烦，所以jupyter提供了一个自动更新修改的方式。在笔记本开头运行下面两条命令  
  %load_ext autoreload  
  %autoreload 2  
- 列出全局变量  
  %who      列出所有变量  
  %who_ls   以列表形式列出所有变量  
  %whos     展示所有变量更详细的信息  
  %who list  也可以只列出某种类型的变量  
  %who function  也可以只列出某种类型的变量  
  %who int  也可以只列出某种类型的变量  
- 不常用  
  %lsmagic                展示所有魔法命令  
  %timeit                 运行100000次测试运行时间（比%time更加准确，避免了单次运行的偶然性）  
  %qtconsole              调出新的ipython窗口，和当前notebook之间变量可以共享  
  %prun  %%prun           展示每一步代码的运行时间  
  %load hello.py          将hello.py这个文件中的代码导入这个Cell  
  %pycat hello.py         查看hello.py文件内容  
  %%writefile hello.py    将当前Cell中代码写入hello.py文件中  
- 还有一个%store，可以在两个notebook之间传递变量。  
  在一个notebook中运行  
  a = 1  
  %store a  
  在另一个notebook中运行  
  %store -r a  
- link  
  https://blog.csdn.net/Marybabana/article/details/88765581  



- 