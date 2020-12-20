##### 在project中进行safe delete后如何恢复

右建点击projict中对应的文件夹，local history，how history，revert selection

##### pycharm最大标签数设置，默认10。

File --> Settings -->Editor -->General --> Editor Tabs --> Tab limit 然后输入你想打开的文件最大数量





# pycharm远端调试

### linux配置用户启动脚本

​	vi ~/.bash_profile

​	# 添加当前用户的启动配置,启动anaconda 环境

​	source /home/workflow/conda/bin/activate jk

### 配置pycharm远程调试

以项目方式打开本地文件夹，然后进入File>>Settings，打开Settings窗口，左侧菜单列表进行下几个配置：

##### （1）配置解释器（Project>>Project Interpreter）

右侧窗口Project Interpreter框最右侧有个齿轮，点击齿轮选择Add（选择show all可打开列表，进行删除等操作），选择Add会弹出Add Python Interpreter窗口。

在Add Python Interpreter窗口左侧列表选择SSH Interpreter。

在右侧选Nwe server configuration， 配置服务器Host地址（172.16.2.119）、端口号Port（一般22）、用户名Username（可以用root）、密码password。

注意：在右侧选Existing server configuration可在下拉列表中选择存在的服务器，必免上一步重复新建。

填好点击Next进入下一步，

interpreter框填写远程服务器上的解释器路径（~/conda/env/whl/bin/python）

注意：路径不清楚的可以进入对应的conda环境执行which python获取，也可进入python用sys.executable查看

sync folders框填写同步文件夹映射关系，本地到远端（project root到/tmp/project）（可以选择多个 ，但不知道有什么意义）

其他根据需要勾选一下，点击finish结束配置

注意：有时配置多个远程解释器会导致显示不出来package列表（也可能是重复配置远程解释器导致的），可以删掉重复的，或删掉所有重新来进行尝试。

##### （2）远端部署（Build,Execution,Deployment>>Deployment）

在左侧选择已存在的远程服务器，或者点加号新建。这里的列表会在上一步配置的时候更新，所以直接选吧。

在选择的服务器对应右边窗口设置Connection和Mappings两个标签页。前者会在解释器配置的时候同步过来，后者要重新配置一下映射。 Mappings配置完以后，其实是相当于配置了一个ftp工具可以连接到服务器上，然后就可以直接在本地计算机查看到远程服务器上Deployment path on server “name”所指定路径下的文件了，并且它与你现在本地的工程目录Project root是连接的，可以实现互传功能。

查看远程服务器上文件：Tools>>Deployment>>Browse Remote Host

同步远端文件：Tools>>Deployment>>Upload to或Download from

完成后点击Apply，就可以通过Run来测试代码啦！

##### （3）配置控制台（Build,Execution,Deployment>>Console>>Python Console）

右侧Python interpreter框的下拉列表选择已经存在的解释器，在第一步配置的解释器会加到此列表。





# 快捷键

- ctr+左键点击，跳转到调用的函数来源，如果本身就是来源，则可以显示被调用例表。
- ctrl R 当前页搜索。
- ctrl shift R 全局搜索。
- ALT + SHIFT + E  
在console中执行光标选中的命令，若未选中内容，则执行光标所在行的命令，光标自动跳到下一行。  
- CTRL + SHIFT + M  
MATCH BRACE  
- CTRL + P  
当光标位于函数括号内，快速显示函数参数  
- SHIFT + ENTER  
直接另起一行，无论光标在什么位置，直接另起一行  
- CTRL + Q  
当光标放到函数或实例上，这个操作能显示其所有可用的参数。  
- CTRL + F（CTRL + R）  
批量查找（批量替换）  
- TAB（SHIFT + TAB）  
批量缩进（批量反缩进）  
- CTRL + C  
如果未选择任何内容，此时CTRL + C会复制该行内容。  
- CTRL + [或]（CTRL + SHIFT + [或]）  
移动到代码块的结束或开始（选择代码块的结束或开始）
- ALT + 左/右  
切换标签页
- CTRL + /  
批量注释
- SHIFT + 鼠标滚轮  
横向滚屏  
- ALT + SHIFT + 拖动鼠标  
选择矩形文本  (等价，按住鼠标中键+拖动鼠标）  
- SHIFT + DELETE  
直接删除一行
- CTRL + 加号  
展开代码块
- CTRL + 减号  
收起代码块
- CTRL + D  
直接复制一行
- 右键单击.py。可以复制路径，还可以用浏览器打开	
- 左边栏查看structure	
- 使用#  TODO  
要做的事情，可以在TODO标签中直接跳转  
- 断点设置个点，右键debug执行	
- ctrl+shift+F10,执行命令  
- shift+f9是debug  
- ctrl+shift+F12，最大化编辑窗口  
- 按住shift+上下键是滚屏，光标不动。  
- Bookmark功能，在光标所在行建立书签。添加ctrl+F11，删除F11，查看所有shift+F11  
- 右键点击想批量替换的变量,选择refactor,然后在窗口中输入新的并替换  
- ctrl+f查找,然后选择regex项,就可以通过正则表达示查找想要的  
- 选定一行，同时按下ctrl +shift ，通过上下键，可移动选下的行  
- 其他  
CTRL+Y          DELETE LINE  
CTRL+DEL        DELETE TO WORD END  
CTRL+BACKSPACE  DELETE TO WORD START  
CTRL+SHIFT+J    JOIN LINES  
CTRL+Q          帮助文档  
CTRL+W          EXTEND SELECT  
CTRL+SHIFT+W    SHRINK SELECT  
- link  
https://blog.csdn.net/gzmfxy/article/details/78700522  
https://www.cnblogs.com/zhangpengshou/p/3555767.html  
https://www.cnblogs.com/littleseven/p/5599019.html  





