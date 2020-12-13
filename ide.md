##### 关于jpynb导出为md文件

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



# chrome

- 标签页和窗口
space(shift+space)  #上下翻页  
Ctrl + n  #打开新窗口  
Ctrl + Shift + n  #稳身模式下打开新窗口  
Ctrl + t  #打开新的标签页，并跳转到该标签页  
Ctrl + Shift + t  #重新打开最后关闭的标签页，并跳转到该标签页  
Ctrl + w或ctrl+ f4  关闭当前标签页  
Ctrl + Shift + w 关闭所有打开的标签页和浏览器   
Ctrl+(tab/shift+tab/up/down）  
Alt + 左右  #浏览器历史前进后退  
Ctrl+1~8/9  #按数字跳转，9是最后一个   
Alt + Home 在当前标签页中打开主页   
- 功能快捷键 
alt+f  #打开菜单  
ctrl+f  #查找  
ctrl+g/ctrf+shift+g  #查找结果前后跳转  
ctrl+shift+o  #打开书签管理器  
ctrl+h  #打开历史记录在新标签页  
ctrl+j  #打开下载内容在新标签页  
ctrl+shift+delete  #清除历史记录窗口    
shift+esc  #打开chrome任务管理器  
- 地址栏  
ctrl+k/ctrl+e + tab  #开始搜索引擎搜索，用tab切换引擎  
ctrl+enter/alt+enter  #当前页搜索/新打开搜索    
ctrl+l/alt+d  #跳转到地址栏  
f6/shift+f6  #地址栏/tab/书签栏/页面之间循环切换  
- 网页快捷键  
ctrl+shift+j  #开发者工具  
ctrl+shift+i  #开发者工具的反馈表单  
ctrl+u  #显示html源码  
ctrl+d  #将当前页保存为标签  
ctrl+shift+d  #将所有打开的标签页以书签形式保存在新文件夹中  
space/shift+space/up/down  #上下翻页  
ctrl+加/减/0  #放大/缩小/还原  
ctrl+r/f5  #刷新网页，加上shift就忽略缓存内容  
ctrl+o  #使用chrome打开计算机中的文件  
f11  #开启或关闭全屏模式  
home/end  #转到网页头或尾  
alt+点击链接  #下载链接目标  
ctrl+点击链接  #后台打开链接  
shift+点击链接  #新窗口打开链接  
ctrl+shift+点埚链接  #打开链接并跳转  
- 暂不使用  
ctrl + shift + b  #显示隐藏书签栏  
alt+shift+t  #将焦点放在chrome工具栏中的第一项上  
alt + space + n  #最小化当前窗口  
alt + space + x  #最大化当前窗口  
f1  #帮助选项  
ctrl+shift+m  #账户登录界面  
