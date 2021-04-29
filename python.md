# 杂

##### 待处理

pip机制待学习，帮助了解包的发布

##### Python的.py与Cython的.pxd.pyx.pyd 文件格式之间的主要区别

https://cloud.tencent.com/developer/news/180987



### 安装目录

##### linux自带python目录

/usr/bin/python

/usr/lib/python3.6/site-packages

##### linux安装conda后的base

/home/username/conda/bin/python

/home/username/conda/bin/activate

/home/username/conda/lib/python3.7/site-packages

##### linux安装conda后的envs

/home/username/conda/envs/envname/bin/python

/home/username/conda/envs/envname/lib/python3.7/site-packages

##### win安装conda后的base

c:\programdata/anaconda3\python.exe

c:\programdata/anaconda3\lib\site-packages

##### win安装conda后的envs

c:\programdata/anaconda3\envs\envname\python.exe

c:\programdata/anaconda3\envs\envname\lib\site-packages





### 其他



python file.py -h可显示argparse中定义的帮助信息

##### python调用dos命令

一种是os.system('python some.py')，另一种是subprocess库的popen函数。注意文件路径最好是绝对路径，相对路径会因环境变量问题导致错误。另外一定要给路径加上引号，否则会有可能报错。

##### python调用shell命令常用4种方法，以及shell脚本使用Python脚本的参数。

https://www.jb51.net/article/186301.htm

一是os模块的system方法。二是os.popen()函数。三是commands模块。四是subprocess模块。

##### python获取自己位置的几种方法

进入python，可使用sys.executable

在linux下激活某conda环境，用which python可找到该环境python位置。

##### python -m执行方法

两篇文章说的不是太清楚。只说python -m file.py等价于python file.py

https://blog.csdn.net/opencv_fjc/article/details/106143566

https://www.cnblogs.com/xueweihan/p/5118222.html

https://www.zhihu.com/question/319387513/answer/652621252

https://www.icode9.com/content-1-470002.html

##### python -c执行方法





# 解释器

参考：https://docs.python.org/zh-cn/3/using/cmdline.html#using-on-general

python解释器：将安装python位置加入到搜路径（ /usr/local/bin/python3.96），执行python即可启动python解释器。

退出： Unix 里是 Control-D，Windows 里是 Control-Z ， quit() 通用。

启动解释器的另一种方式是 `python -c command [arg] ...`，这与 shell 的 [`-c`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-c) 选项类似，其中，*command* 需换成要执行的语句。由于 Python 语句经常包含空格等被 shell 特殊对待的字符，一般情况下，建议用单引号标注整个 *command*。 

Python 模块也可以当作脚本使用。输入：`python -m module [arg] ...`，会执行 *module* 的源文件，这跟在命令行把路径写全了一样。 





# 官方文档

python是通过module组织代码的，每一个module就是一个.py文件，但是modules是通过package来组织的。

模块module：就是点py文件

包package：是一个文件夹，必包含init.py（告诉python这个文件夹是一个包）。可以包含py文件或子文件夹。当import 某包名时，会执行一次该包下的init.py文件，这种方式实际上是导入了这个包名下的init.py文件。

库：其他语言说法，实现某功能的代码集合，在python中的形式就是模块和包。

要注意的一个重点概念是所有包都是模块，但并非所有模块都是包。 或者换句话说，包只是一种特殊的模块。 特别地，任何具有 `__path__` 属性的模块都会被当作是包。 

退出 Python 解释器再次进入时，会丢失之前定义的函数和变量。 





dir(模块名)，返回目标模块内的变量，包括（`__file__`,`__name__`,`__doc__`等）。如果在模块内执行dir()，返回所在模块本身的所有变量。在解释器中dir()，则返会解释器环境中的所有变量名。但是dir()不会列出内置函数和变量，这些可以通过以下方式列出`import builtins; dir(builtins)`。

`__name__`：以import运行的时候`__name__`等于文件名(不包含.py)，以脚本执行时永远等于`'__main__'`。在交互界面中，模块名.`__name__`返回的也是模块名称。但是在交互界面直接执行`__name__`返回的是`'__main__'`。

`'__main__'` 是顶层代码执行的作用域的名称。模块的 `__name__` 在通过标准输入、脚本文件或是交互式命令读入的时候会等于 `'__main__'`。模块可以通过检查自己的 `__name__` 来得知是否运行在 main 作用域中，这使得模块可以在作为脚本或是通过 `python -m` 运行时条件性地执行一些代码，而在被 import 时不会执行（也就是`if __name__ == "__main__":`）。

`__file__`：返回所在模块的完整路径（该路径包含模块名.py）。在交互界面，模块名.`__file__`返回同样结果。如果设置了 `__file__`，则也可以再设置 `__cached__` 属性，后者取值为编译版本代码（例如字节码文件）所在的路径。

`__doc__`返回模块中的第一段以三层引号注释的文本。在交互界面，模块名.`__doc__`返回同样结果。

`__path__`：包名.`__path__`返回包的路径。模块没有`__path__`，需要自已定义，模块定义`__path__`后会被视为包。如果一个模块具有 `__path__` 属性，它就是包。包的 `__path__` 属性会在导入其子包期间被使用。在导入机制内部，它的功能与`sys.path`基本相同，即在导入期间提供一个模块搜索位置列表。 但是，`__path__` 通常会比`sys.path`受到更多限制。

`__spec__`： `模块名.__spec__`或`包名.__spec__`，返回模块或包的说明，包括名称，位置等等。

`__package__`：模块的 `__package__` 属性必须设定。 其取值必须为一个字符串，但可以与 `__name__` 取相同的值。 当模块是包时，其 `__package__` 值应该设为其 `__name__` 值。 当模块不是包时，对于最高层级模块 `__package__` 应该设为空字符串，对于子模块则应该设为其父包名。`__package__` 预期与 `__spec__.parent` 具有相同的值。







# import本质

##### 第一步，检查sys.modules

首先会检查sys.modules文件（该文件只保存模块名和包名（包括中间路径），不会保存变量名），如果已在其中，则跳过，不会导入该包（这种方式保证解释器会话只导入一次模块，提高效率）。（如果想重新导入以便让修改过的模块生效，必须重启解释器；或在交互模式时使用`importlib.reload(modulename)`）。

##### 第二步，找到源码文件

没有导入过的包则会执行导入。此时会去搜索路径查找模块。一般找到的是源码文件。但如果是C语言的，源码是个假文件，实际导入的是另外存储的文件（可能是已编译的）。

##### 第三步，编译

解释器会检查同级目录中的`__pycache__`文件夹，然后对比编译版本与源码的修改日期，查看它是否已过期，是否要重新编译，此过程完全自动化。编译后会保存pyc文件。

注意：`python name.py`：以脚本的方式执行，不会检查`__pycache__`文件夹，只重新编译，且不会保存pyc文件，这时  `__name__` 是 `"__main__"` 。

注意：没有源码文件时也不会检查缓存。为了支持无源文件（仅编译）发行版本， 编译模块必须在源目录下，并且绝不能有源模块。比如C语言编写的模块。

##### 第四步，变量赋值

import xxx或import as xxx会给xxx变量赋值，也会覆盖xxx原本的变量，虽然包已导入无需再导入，但变量赋值必执行（dir()可查看已存在变量）。

##### 注意

 `from package import item` 时，import语句会首先检查item是不是init.py的变量，然后再检查目录中是否有item这个子包，如果有则导入这个包的init模块。最后才会检查是否有item模块(也就是.py文件)并导入。所以要避免包名，模块名以及init变量名的重名。(这段已测试，确实如此)

`import foo.bar.baz`时，Python 先尝试导入 `foo`，然后是 `foo.bar`，最后是 `foo.bar.baz`。 如果这些导入中的任何一个失败(比如某个包下面的init文件执行报错)，都会引发`ModuleNotFoundError`。

`import a.b.c`时，除c以外的前面每一项必须是包，c可以是包也可以是模块。但c若是包则不能使用c.modules引用c包中的模块，只能c.item引用c包init中定义的内容。





##### 搜索路径

首先查找内置模块进行导入，若未找到，再从sys.path变量中查找a.py文件。

sys.path会在解释器开始执行时被初始化成包含以下3项的列表：（1）脚本所在目录或未指定文件时的当前目录（如果在pycharm中，这个目录会受pythcarm工程目录的影响）（2）PATHONPATH环境变量的目录列表（与shell变量PATH语法一样，如果未设置PYTHONPATH环境变量，则会使用内置的默认路径）（3）与安装相关的默认值（比如 /usr/local/lib/python）。

最后还要注意一点，sys.path路径顺序可更改，若脚本所在目录位于标准库目录之前，因此若脚本目录模块名与标准库模块名冲突，则会先导入脚本模块。（但是经过测试，虽然更改了sys.path的顺序，但是无论是标准库还是三方库，都是优先于当前目录库导入的）

```python
sys.path
['','c:\\program\\anaconda3\\lib\\site-packages']  # ''代表当前工作目录
```

##### 添加搜索路径

例如创建`/home/wang/hello.py`内容如下`hello wanghl`。

(1)动态增加路径：临时生效，不会污染PYTHONPATH

```
sys.path.append('home/wang')
```

(2)修改PYTHON变量：永久生效，任何人启动python时，都会读取这个变量，甚至不同版本的python都会受影响。

```linux
vim ~/.bashrc
export PYTHONPATH=$PYTHONPATH:/home/wang/workspace
source ~/.bashrc # 或者 . ~/.bashrc 
```

(3)增加.pth文件：永久生效，最简单也最推荐。Python 在遍历已知的库文件目录过程中，如果遇到 `.pth` 文件，便会将其中的路径加入到 `sys.path` 中，于是 `.pth` 中所指定的路径就可以被 Python 运行环境找到了。

在 `/usr/local/lib/python3.5/site-packages` 下添加一个扩展名为 `.pth` 的配置文件（例如：`extras.pth`），内容为要添加的路径：`/home/wang`。





##### init

导包时，Python 搜索 `sys.path` 里的目录，查找包的子目录。 Python 只把含 `__init__.py` 文件的目录当成包， 这个包的名子就是文件名子（没有.py），导包时 `__init__.py` 会被隐式的执行。





##### 其他

import * 会导入所有不以下划线开头的变量。

 [`compileall`](https://docs.python.org/zh-cn/3/library/compileall.html#module-compileall) 模块可以为一个工程目录下的所有模块创建 .pyc 文件。 

 



# 案例

### project是一个文件夹，也就是工程，而不是一个包，他的init文件没用。

```text
project
│   __init__.py
│   filea.py
│   fileb.py
│   root_file.py
├───foldera
│   │   __init__.py
│   │   filea.py
│   │   fileb.py
│   │   root_file.py
│   │   foldera_fa
│   │   │   __init__.py
│   │   │   filea.py
├───folderb
│   │   __init__.py
│   │   filea.py
│   │   fileb.py
│   │   root_file.py
```



##### init.py

```python
rt_init = 'init_rt'
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
print('im fdainit')
fda_init = 'init_a'
from fileb import fibva
fibva = fibva * 10  # 50
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

##### foldera/foldera_fa/init.py

```python
print('im fdafdainit')
fdafda_va = 666
```

##### foldera/foldera_fa/filea.py

```python

```

##### folderb/init.py

```python
fdb_init = 'init_b'
fdb_init_v1 = 111
_fdb_init_v2 = 222
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
import project  # 会报错，这里的project是工程的根目录，而不是一个包，所以不能导入。
import foldera_fa  # 在交互解释器中会报错，因为默认当前目录是工程根目录，所以一定要从工程根目录中的包开始写，否则找不到该模块。可修改如下：
from foldera import foldera_fa  # 正确
import root_file  # 正确
from root_file import rtva,rtvb  # 正确
from root_filea import rtva as a  # 正确
```

只导入包（可调用包中的变量），不能调用其中模块，要导入到具体模块或变量才可以。

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

### init文件（特殊的module，相当于包本身(目录名)的模块）

注意：此处根目录project不是一个包（虽然有init文件），而是一个项目。所以不能从根目录开始导入，比如`from project import xxx`将会报错。

```python
"""下面这种方式会导入foldera/__init__.py"""
import foldera  # 此时会调用foldera下的init.py中的变量。
foldera.fibva  # 这个值为5*10=50，是init中import语句再乘以10得到的。
foldera.fda_init  # 值为“init_a”，是init中定义的变量。
foldera.fdartva  # 值为7，为from .root_file import fdartva导入的


"""按以下顺序导入，各执行一次init"""
import foldera  # 导入了foldera/__init__.py
打印im fdainit
from foldera import foldera_fa  # 导入了foldera/foldera_fa/init.py
打印im fdafdainit
"""按以下顺序导入，第一条导入已执行了两个init，第二条导入没有导入任何包"""
from foldera import foldera_fa  # 导入了foldera/__init__.py和foldera/foldera_fa/init.py
打印im fdainit
打印im fdafdainit
import foldera  # 未导入任何内容


"""第一次导入的fibva是50，来自foldera的init。第二次导入的fibva是5，来自根目录的fileb。
注意，此时第二次导入fibva进行了覆盖操作。首先导入命令会检查sys.modules文件，这里记录了两次导入的模块的全路径（foldera和fileb（路径是用点表示的folera.filea）），如果导入过则不会再导入(导入时是否编译是通过源码日期与pyc文件日期来判断的)。其次，第二次导入命令用fileb.fibva的值覆盖了变量fibva（此前这个变量的值是foldera.fibva赋予的）。
"""
from foldera import fibva
from fileb import fibva
```

##### import * (模糊导入，可用all来定义)

```python
"""导入非下划线开头的所有变量。下面导入两个变量fdb_init和fdb_init_v1，未导入下划线开头的_fdb_init_v2"""
from folderb import *
"""但是可以这样导入"""
from folderb import _fdb_init_v2
```

修改`folderb/__init__.py`内容如下：

```python
__all__ = ['fdb_init', '_fdb_init_v2']
fdb_init = 'init_b'
fdb_init_v1 = 111
_fdb_init_v2 = 222
```

```python
"""因为all的存在，此时导入的是all指定的变量fdb_init和_fdb_init_v2"""
from folderb import *
```



### 相对路径引用

python中的import分为绝对引用和相对引用两种。它们之间的差异在于，引用模块时定位被引用模块位置的方式不同

(a)绝对引用是通过.的连接，指定出最高级文件（夹），到目标文件的绝对路径。我们上面的所有用法都属于绝对引用。

(b)而相对引用是 指定待引用模块与当前文件的相对位置，`.`表示上一级文件

绝对引用类似这样`from folder.abcd import myclass`

相对引用类似这样`from .abcd import myclass`

在实际使用中，无论是绝对导入还是相对导入都要注意，如何导入与被调用位置有关。

以下面的文件结构为例

```text
folder1
    │  first1.py
    │  first2.py
    └─folder2
         |  second1.py
         |  second2.py
    └─folder3
         |  third1.py
         |  third2.py
```

下面分为两种情况

folder1是一个项目，运行这个项目需要在folder1文件夹中打开cmd，运行`python first1.py`

```python3
# first1.py
from first2 import sth          # OK
from folder2.second2 import sth # OK
from folder1.first2 import sth  # ERROR
from second2 import sth         # ERROR
from .first2 import sth         # ERROR

# second1.py
from first2 import sth          # OK
from folder2.second2 import sth # OK
from folder1.first2 import sth  # ERROR
from second2 import sth         # ERROR
from .second2 import sth        # OK
```

(注意first1引用first2 与 second1引用second2 的区别)

folder1是一个包，一般使用时，是在外面的文件夹中import这个包

```python3
# first1.py
from first2 import sth           # ERROR
from folder1.first2 import sth   # OK
from .first2 import sth          # OK
from . import first2             # OK
import .first2                   # ERROR

# second1.py
from first2 import sth               # ERROR
from folder1.first2 import sth       # OK
from .first2 import sth              # ERROR
from . import first2                 # ERROR
from .. import first2                # OK
from . import second2                # OK
from ..folder3 import third1         # OK
```

规律

(a)绝对引用就是从包的位置一直往下，写到目标文件位置

(b)相对引用，用`.`代替当前文件所在目录，用`..`代替再上一级目录，用点来回溯，之后往下写到目标文件位置。

(c)`.`只能放在`from`后，不能放`import`后。

相对引用的好处在于，代码中不需要出现`folder1`这个名称，因此当包的名称改变时，里面代码不需要做任何改变；或者有的用户要装两个版本的包，把其中一个版本的包重命名了，此时使用相对引用也不会出问题。

下面这段还没理解：

另外，以second1.py为例，如果其中有一些相对引用的代码，在folder1的上一层文件夹调用

```text
python folder1/folder2/second1.py
```

这时相当于在folder2文件夹中调用second1.py文件，会报错。但如果像下面这样就可以正常运行

```text
python -m folder1.folder2.second1
```





# 优质参考

**keyword传参很容易混乱。try方法。重写父类有时会看不出来。nan在df中。

##### 关于模块的机制（知乎）

https://zhuanlan.zhihu.com/p/33913131

##### 模块原理及导入（老python的经验，很全面很实用）

https://blog.csdn.net/shouhuxianjian/article/details/45111375

##### setuptools打包入门实操

https://www.jianshu.com/p/ea9973091fdf

##### python安装三方库的三种方式（帮助理解安装原理机制）（下载到本地用setup安装）

https://blog.csdn.net/weixin_41377182/article/details/105241255

##### setuptools英文文档（来自文档托管平台）

https://setuptools.readthedocs.io/en/latest/setuptools.html

##### 包/模块(三方包安装)

https://www.jianshu.com/p/68477d5625fc

##### 官方文档分发模块（遗留版本）（英文）

https://docs.python.org/zh-cn/3.8/distutils/setupscript.html#

##### 官方文档分发模块

https://docs.python.org/zh-cn/3.8/distributing/index.html

##### 包管理工具介绍

https://www.jianshu.com/p/e0ac8bc5ae1a









