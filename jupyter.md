# 官方文档

jupyter

https://github.com/jupyter/jupyter

https://jupyter.org/

org中的documentation

https://jupyterlab.readthedocs.io/en/stable/index.html

https://jupyter-notebook.readthedocs.io/en/stable/index.html

ipython

https://ipython.org/

https://ipython.readthedocs.io/en/stable/index.html#

##### 显示帮助信息

```
jupyter
jupyter -h
jupyter notebook --help
jupyter notebook --help-all
jupyter kernel --help-all
jupyter --version
```









# 常用

### ipynb转markdown

一种是linux下执行命令（jupyter nbconvert --to md notebook.ipynb），一种是在jupyter notebook交互界面可以导出md。

```python
jupyter nbconvert --to markdown --output-dir "C:\\users\\hayden\\desktop\\ipynb\\md_convert" "C:\users\hayden\desktop\ipynb\*.ipynb" 
```

### pandas.dataframe显示

jupyter lab中，如果输出的dataframe太大，可以右键选择enable scrolling for outputs

### jupyter交互界面显示图片3方法

```python
"""使用pillow"""
from PIL import Image as img
img.open('abcd.jpg')
"""使用opencv，要配合matplotlib"""
import cv2
from matplotlib import pyplot as plt
img1 = cv2.imread('abcd.jpg')
img2 = img1[:,:,::-1] # 必须为 ::-1
plt.imshow(img2)
"""使用ipython。IPython.display.display在打开jupyter时默认导入"""
from IPython.display import Image
Image('abcd.jpg')
```



# jupyter notebook主题更换（对lab无效）

pip install jupyterthemes

jt -l  # 查看主题列表

jt -t chesterish  # 转换主题

jt -r  # 恢复原始主题



# win10相关

##### 快捷方式打开指定目录

可以找到jupyter notebook快捷方式所在文件夹，复制到桌面，然后通过改配置文件参数，能控制这个桌面快捷方式的行为，打开目录，打开lab等。

##### 配置文件位置

配置文件在这里C:\Users\hayden\\.jupyter

##### 快捷方式打开时，如何指定浏览器

在配置文件中添加以下三行语句

```python
import webbrowser webbrowser.register('chrome',None,webbrowser.GenericBrowser(u'C:\Program Files (x86)\Google\Chrome\Application\chrome.exe')) 
c.NotebookApp.browser = 'chrome'
```







# jupyter远程访问

### 参考资料，待学习

https://zhuanlan.zhihu.com/p/166425946

### 生成密码保存备用

from notebook.auth import passwd 

passwd() （下面密码是12345）

'argon2:$argon2id$v=19$m=10240,t=10,p=8$fHzsipzyiQN1HpHaNAApxg$xYa76axEUgfMEw7sLMo1wg'

### 安装（目前是root登录且base环境安装的。是否需要root登录？以及是否需要base环境安装？待研究。）

pip install jupyter（这个安装的是jupyter notebook）

pip install jupyterlab (没有空格，不是jupyter lab，否则安装的是另外两个包jupyter和lab)

如果不安装jupyterlab，则只能使用notebook远程访问，不能使用lab远程访问

### 参数配置

##### 生成及保存的位置

jupyter notebook --generate-config（ ~/.jupyter/jupyter_notebook_config.py ）

jupyter lab --generate-config（ ~/.jupyter/jupyter_lab_config.py ）

虽然使用jupyter lab --generate-config生成的配置文件是jupyter_lab_config.py，但实际jupyter lab启动服务的时候，使用的是jupyter_notebook_config.py这个配置文件。所以jupyter_lab_config.py文件似乎并没什么用。

##### 配置文件解读

```
c.NotebookApp.allow_remote_access = True  # 允许外部访问，默认值False
c.NotebookApp.allow_root = True  # 允许使用root用户启动服务，这样启动时就不用加 --allow-root了。
c.NotebookApp.ip = '*'  # 等号右边的‘localhost’（仅仅运行本地访问），修改为‘*’，表示允许所有IP皆可访问。官方文档建议修改成‘*’，但可能还是无法访问，可以修改成'0.0.0.0'或'0.0.0.1'或者服务器IP。
c.NotebookApp.notebook_dir = "/"  # 指定默认的启动路径，否则会在当前路径下启动。
c.NotebookApp.open_browser = False  # 禁止自动打开浏览器（因为服务器上就没有浏览器）
c.NotebookApp.password = "sha1:0d46e59c26c6:caab7b48941bee0095bdcf0747cd2a5a22a27581"  # 设置密码
注意，当设置c.NotebookApp.password = ''时表示无密码，需要token=后面一串字符登录。(使用jupyter notebook list命令可获得已启服务的token)
c.NotebookApp.port = 7788  # 设置固定的notebook服务监听的IP端口，保证不和其他已经启用的端口号冲突。
c.NotebookApp.default_url = '/lab'  # 设置启动方式('/tree'或'/lab')，使用'/lab'的前提要安装jupyterlab。
```

```
# 这是jupyter_lab_config.py的配置，目前没什么用。jupyter lab启动也不用。
c.ServerApp.allow_remote_access = True
c.ServerApp.ip='*'
c.ServerApp.root_dir = "/home/whl/jupyterlab/"
c.ServerApp.open_browser = False
c.ServerApp.port = 7788
c.ServerApp.password = "sha1:0d46e59c26c6:caab7b48941bee0095bdcf0747cd2a5a22a27581" 
```



### 启动（最好在base环境下启动，其他环境下启动的影响未测试。）

linux系统中，某用户通过jupyter notebook创建的远程服务，其他用户使用jupyter notebook list是查不到的，即使root用户也无法查看到其他普通用户启动的jupyter notebook服务。所以要注意linux系统的登录用户是谁，然后再启动。

##### 启动时的参数，可以覆盖配置文件中的参数

jupyter notebook --allow-root --ip 0.0.0.0 --config jupyter_notebook_config_2.py --notebook-dir /your_path

nohup jupyter lab  &

##### 启动时到底是notebook还是lab？

当配置文件中未设置c.NotebookApp.default_url = '/lab' 时，默认的就是'/tree'，jupyter notebook启动的是notebook，jupyter lab启动的是lab。

当配置文件中设置c.NotebookApp.default_url = '/lab'时，jupyter notebook和jupyter lab均启动的是lab。

当然，在远程浏览器访问时，输入的url也可以控制，也就是http://172.16.2.119:8888/lab和http://172.16.2.119:8877/tree的区别。不用在意是用jupyter notebook还是用jupyter lab启动的，都一样的效果。

##### 查看正在run的服务(看有几个后台任务)

jupyter notebook list

Jupyter notebook stop someport  # 通过端口号关闭后台服务。只对无密码（有token）的服务有效，对于有密码的服务不起作用，请使用kill -9 PID停掉服务。(有密码时报错如下tornado.httpclient.HTTPError: HTTP 403: Forbidden)

##### 后台运行

nohup jupyter notebook &

##### 报错500处理

使用远程浏览器登录报错：Jupyter: 500 internal server error

这是由于ipython或者jupyter notebook某些包与Python版本不兼容的问题, 全更新了就好.

pip install -upgrade "ipython[all]"  # 注意引号和方括号都得有





# kernel设置

##### 将conda的某个环境加入到jupyter的launcher页面（还可以设置launcher图标）

```
jupyter kernelspec list  # 前题要启动conda环境，并且该环境下安装了ipykernel（无需安装jupyter）。则可查看目前已有的kernel。在任何环境中都可查到所有环境的kernel。但是注意，非root用户查不到root用户安装的kernel。
conda activate 环境名  # 激活将要安装jupyter kernel的环境
pip install ipykernel  # 安装jupyter kernel
python -m ipykernel install --name 环境名 --display-name 显示名  # 显示名称可选，是在jupyter的launcher中显示的名称
```



# 网上关 于放行Linux防火墙的端口，未研究，与linux有关。

截止到第（3）步，Jupyter Notebook的设置已经接近尾声。

但工作还没有做完。虽然我们开启了访问的端口，但Jupyter Notebook毕竟仅是Linux的一个应用程序，仅仅是它许可开放某个端口，这还不够。

Linux还得有个“外交部”——防火墙，只有它许可开放，那才是真的开放。

因此，下面的工作就是设置防火墙的端口开放。倘若开放某个端口（如9999），使用如下命令

> jpnb@centos-7 .jupyter]$ **sudo firewall-cmd --zone=public --add-port=9999/tcp --permanent**
> [sudo] jpnb 的密码：****
> Success

如果我们开放的不是9999，则修改上述端口号即可。

同样，有了新设置，我们还需要重新启动防火墙，使之生效。使用下面的命令，即可达到重启防火墙的功效：

> [jpnb@centos-7 .jupyter]$ **sudo systemctl restart firewalld**





# jupyter操作

##### 非编辑模式下：  

单元格操作：b, a, c, x, v, shift+ctrl+-, shift+m

标题字号：数字键1-6 

搜索：ctrl+f，在cell内搜索，或全局搜索 

模式切换： Code-y MarkDown-m Raw-r

##### 编缉模式下：

ctrl+鼠标左键，多光标同步操作。

ctrl+enter，运行当前Cell，选中当前Cell

shift+enter，运行当前Cell，选中下一个Cell

alt+enter，运行当前Cell，创建下一个Cell并进入编辑

##### 魔法命令：

%对单行有效，放在单行行首。

%%对Cell有效，放在Cell最开头，单独一行。

%time，统计单行运行时间。

%%time，统计单元格运行时间。有时导致代码不执行、空跑，且不报错，很多未知错误，对结果没把握不要用。



%matplotlib inline，matplotlib绘图，一个notebook中只需要运行一次，则之后用matplotlib库作图不需要plt.show()即可把图展示出来。



##### 未整理的

- jupyter notebook配置默认启动路径  
  打开Anaconda Prompt，输入jupyter notebook --generate-config，获得jupyter_notebook_config.py文件的路径  
  打开jupyter_notebook_config.py文件，找到##The directory to use for notebooks and kernels.，设置c.NotebookApp.notebook_dir = '设置路径'  
  右击jupyter notebook图标，点击属性，找到目标（T），将路径最后的%USERPROFILE%删掉。
- 编缉模式下  
  Ctrl + /          批量注释与取消注释  
  Tab               代码提示  
  Shift + Tab       查看函数帮助文档（点击加号可以看详细内容）  
  pageup/pagedown  光标移动到cell头cell尾  
  home/end(Alt + left/right)  光标移动到行首/尾  
  按住Alt拖动鼠标              多行编辑、矩形选框  
  按住Ctrl在多个位置点击鼠标    多处同时编辑  
- 魔法命令规律 
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


