# 待处理

##### setuptools的使用，如何发布py包

https://www.jianshu.com/p/ea9973091fdf

##### pip机制待学习，帮助了解包的发布







# 其他

##### ipynb转markdown

```python
jupyter nbconvert --to markdown --output-dir "C:\\users\\hayden\\desktop\\ipynb\\md_convert" "C:\users\hayden\desktop\ipynb\*.ipynb" 
```

##### python调用dos命令

一种是os.system('python some.py')，另一种是subprocess库的popen函数。注意文件路径最好是绝对路径，相对路径会因环境变量问题导致错误。另外一定要给路径加上引号，否则会有可能报错。

##### python调用shell命令常用4种方法，以及shell脚本使用Python脚本的参数。

https://www.jb51.net/article/186301.htm

一是os模块的system方法。二是os.popen()函数。三是commands模块。四是subprocess模块。

##### python获取自己位置的几种方法

进入python，可使用sys.executable

在linux下激活某conda环境，用which python可找到该环境python位置。











# 解释器

参考：https://docs.python.org/zh-cn/3/using/cmdline.html#using-on-general

python解释器：将安装python位置加入到搜路径（ /usr/local/bin/python3.96），执行python即可启动python解释器。

退出： Unix 里是 Control-D，Windows 里是 Control-Z ， quit() 通用。

启动解释器的另一种方式是 `python -c command [arg] ...`，这与 shell 的 [`-c`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-c) 选项类似，其中，*command* 需换成要执行的语句。由于 Python 语句经常包含空格等被 shell 特殊对待的字符，一般情况下，建议用单引号标注整个 *command*。 

Python 模块也可以当作脚本使用。输入：`python -m module [arg] ...`，会执行 *module* 的源文件，这跟在命令行把路径写全了一样。 





# 官方文档

模块module：就是点py文件

包package：包含点py文件的文件夹

库：其他语言说法，实现某功能的代码集合，在python中的形式就是模块和包。

要注意的一个重点概念是所有包都是模块，但并非所有模块都是包。 或者换句话说，包只是一种特殊的模块。 特别地，任何具有 `__path__` 属性的模块都会被当作是包。 

退出 Python 解释器再次进入时，会丢失之前定义的函数和变量。 





dir(模块名)，返回目标模块内的变量，包括（`__file__`,`__name__`,`__doc__`等）。如果在模块内执行dir()，返回所在模块本身的所有变量。在解释器中dir()，则返会解释器环境中的所有变量名。但是dir()不会列出内置函数和变量，这些可以通过以下方式列出`import builtins; dir(builtins)`。

`__name__`，以import运行的时候`__name__`等于文件名(不包含.py)，以脚本执行时永远等于`'__main__'`。在交互界面中，模块名.`__name__`返回的也是模块名称。但是在交互界面直接执行`__name__`返回的是`'__main__'`。

`__file__`，返回所在模块的完整路径（该路径包含模块名.py）。在交互界面，模块名.`__file__`返回同样结果。

`__doc__`返回模块中的第一段以三层引号注释的文本。在交互界面，模块名.`__doc__`返回同样结果。

`__path__`，包名.`__path__`返回包的路径。模块没有`__path__`，需要自已定义，模块定义`__path__`后会被视为包。







# import本质

##### 第一步，检查sys.modules

首先会检查sys.modules文件（该文件只保存模块名和包名（包括中间路径），不会保存变量名），如果已在其中，则跳过，不会导入该包（这种方式保证解释器会话只导入一次模块，提高效率）。（如果想重新导入以便让修改过的模块生效，必须重启解释器；或在交互模式时使用`importlib.reload(modulename)`）。

##### 第二步，找到源码文件

没有导入过的包则会执行导入。此时会去搜索路径查找模块。一般找到的是源码文件。但如果是C语言的，源码是个假文件，实际导入的是另外存储的文件（可能是已编译的）。

##### 第三步，编译

解释器会检查同级目录中的`__pycache__`文件夹，然后对比编译版本与源码的修改日期，查看它是否已过期，是否要重新编译，此过程完全自动化。编译后会保存pyc文件。

注意：`python name.py`：以脚本的方式执行，不会检查`__pycache__`文件夹，直接编译，且不会保存pyc文件，这时  `__name__` 是 `"__main__"` 。

注意：没有源码文件的也不会检查缓存。比如C语言编写的模块。

##### 第四步，变量赋值

会覆盖已存在（也就是冲突）的变量名（dir()可查看已存在变量）。

##### 注意

 `from package import item` 时，首先检查目录中是否有item这个包，如果有则导入这个包的init模块。其次，才会检查是否有item模块(也就是.py文件)并导入。所以要避免包名与模块名重名。

`import foo.bar.baz`时，Python 先尝试导入 `foo`，然后是 `foo.bar`，最后是 `foo.bar.baz`。 如果这些导入中的任何一个失败，都会引发`ModuleNotFoundError`。









##### 搜索路径

首先查找内置模块进行导入，若未找到，再从sys.path变量中查找a.py文件。

sys.path初始化时包含以下位置：（1）脚本所在目录或未指定文件时的当前目录（如果在pycharm中，这个目录会受pythcarm工程目录的影响）（2）PATHONPATH环境变量的目录列表（与shell变量PATH语法一样，如果未设置PYTHONPATH环境变量，则会使用内置的默认路径）（3）默认安装目录。

最后还要注意一点，sys.path路径顺序可更改，若脚本所在目录位于标准库目录之前，因此若脚本目录模块名与标准库模块名冲突，则会先导入脚本模块。（但是经过测试，虽然更改了sys.path的顺序，但是无论是标准库还是三方库，都是优先于当前目录库导入的）



##### init

导包时，Python 搜索 `sys.path` 里的目录，查找包的子目录。 Python 只把含 `__init__.py` 文件的目录当成包， 这个包的名子就是文件名子（没有.py），导包时 `__init__.py` 会被隐式的执行。





##### 其他

import * 会导入所有不以下划线开头的变量。

 [`compileall`](https://docs.python.org/zh-cn/3/library/compileall.html#module-compileall) 模块可以为一个工程目录下的所有模块创建 .pyc 文件。 

 













# 案例

### trymodule是一个文件夹，里面的目录如下

```text
trymodule
│   __init__.py
│   filea.py
│   fileb.py
│   root_file.py
├───foldera
│   │   __init__.py
│   │   filea.py
│   │   fileb.py
│   │   root_file.py
├───folderb
│   │   __init__.py
│   │   filea.py
│   │   fileb.py
│   │   root_file.py
```



##### init.py

```python

```

##### root_file.py

```python
rtva = 1
rtvb = 2
```

##### filea.py

```python
fiava = 3
fiavb = 4
```

##### fileb.py

```python
fibva = 5
fibvb = 6
```

##### foldera/init.py

```python

```

##### foldera/root_file.py

```python
fdartva = 7
fdartvb = 8
```

##### foldera/filea.py

```python
fdafiava = 9
fdafiavb = 10
```

##### foldera/fileb.py

```python
fdafibva = 11
fdafibvb = 12
```

##### folderb/init.py

```python

```

##### folderb/root_file.py

```python
fdbrtva = 13
fdbrtvb = 14
```

##### folderb/filea.py

```python
fdbfiava = 15
fdbfiavb = 16
```

##### folderb/fileb.py

```python
fdbfibva = 17
fdbfibvb = 18
```





### 模块的简单调用

常规导入

```python
import root_file
root_file.rtva
from root_file import rtva,rtvb
from root_filea import rtva as a
from root_filea import *
```

只导入包，不能随便使用其中模块，要导入到具体模块或变量。

```python
import foldera
foldera.filea  # 会报错
foldera.filea.fdafiava  # 会报错
from foldera import filea
filea.fdafiava  # 不会报错
from foldera.filea import fdafiava  # 不会报错
```

文件夹与文件之间可以用.也可以用from import格式，而文件与变量之间只能用from import格式。

```python
import foldera.filea.fdafiava  # 会报错
```

### init文件（特殊文件，相当于包本身(目录名)的模块）

导入`foldera`将隐式执行 `object/__init__.py` 和 `object/foldera/__init__.py`。 后续导入 `folderb`则仅执行`object/folderb/__init__.py`，因为上一步已经执行过`object/__init__.py` ，所以不会再次执行。 (注意，这里是工程根目录的init文件，好像不会被执行。)

```python
import foldera  # 此时会调用folder下的init.py中的变量。
foldera.varb  # varb值为200，varb是init中的import语句导入varb后，再乘以100得到的
foldera.varc  # varc是init中定义的变量
import foldera.foldera_filea
foldera.foldera_filea.varb  # 值为2，此varb不是彼varb
from foldera import varb
varb  # varb是init中的import语句导入varb后，再乘以100得到的，值为200
from foldera.foldera_filea import varb  # 虽然上面导入过varb但这里会重新导入并覆盖，此时值为2
varb
from foldera import varb  # 再次导入varb，又回覆盖上面导入的，值变为init中的200
"""导入命令检查已导入的模块时，是按照文件位置检查的，不同位置的相同变量名导入时不算重复导入，会相互覆盖。
并且，导入命令发现重复导入，只是不会再次进行编译，但仍然会对导入的变量赋值"""
"""再本质一些，import时，先按照该模块的文件路径去检查导入记录文件中是否有该模块路径，如果未记录，则import检查日期与pycache文件日期是否一致，如果日期不一致则重新编译，如果一致就不编译直接导入。但如果发现该路径文件已经导入过也就是在导入记录文件中，则不会再次编译而是直接对导入的变量进行赋值。这也就是说，如果两个模块有相同的变量名时，第一个模块导入该同名变量，第二个模块再导入该重名变量时会覆盖前面导入的值。如果第一个模块再次导入则会覆盖第二个变量导入的值，但经过两轮导和后，源代码不会再次触发编译，只会直接导入并赋值给变量名。"""
```



### 双下划线all限制import *

```python
"""当init文件中未定义__all__变量时，import * 无法导入下划线开头的变量名"""
from foldera import *  # 此时导入的是b和c，_e并未导入。
from foldera import _e  # 这样是可以的
```

##### 修改init.py内容如下，这样可以限制import *的行为

```python
from foldera.foldera_filea import varb
__all__ = ['varb', '_vare']
varc = 3
_vare = 4
```

##### 此时import * 只会导入all中指定的变量。

```python
from foldera import *  # 此时导入的是varb（值为2）和_vare，未导入varc
```



### 导入模块的搜索路径

```python
"""第一步，首先搜寻内置模块是否有该模块"""
"""第二步，若没有，则看下面目录有没有"""
sys.path
['','c:\\program\\anaconda3\\lib\\site-packages']  # ''代表当前工作目录
# 如保添加路径见下面链接
https://blog.csdn.net/liang19890820/article/details/76219560
    
```



### 相对路径引用

```
from foldera.foldera_filea import classa
from .foldera_filea import classa
```

























