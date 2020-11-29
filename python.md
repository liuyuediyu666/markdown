##### python调用dos命令

一种是os.system('python some.py')，另一种是subprocess库的popen函数。注意文件路径最好是绝对路径，相对路径会因环境变量问题导致错误。另外一定要给路径加上引号，否则会有可能报错。

##### python调用shell命令常用4种方法，以及shell脚本使用Python脚本的参数。

https://www.jb51.net/article/186301.htm

一是os模块的system方法。二是os.popen()函数。三是commands模块。四是subprocess模块。



# python基础

python是通过module组织代码的，每一个module就是一个.py文件，但是modules是通过package来组织的。

package：是一个包含init.py的文件夹，里面可包含subpackage和module。在import这个包时，会执行一次init.py文件（重复import不会执行）。我们在导入一个包时，实际上是导入了它的init.py文件。这样我们可以在init.py文件中批量导入我们所需要的模块，而不再需要一个一个的导入。

init.py：该文件包含了包的属性和方法。并告诉python这个文件夹是一个package。不建议在init中写python模块（可另外创建模块写），尽量保证init.py足够轻。

all：init.py中的all是用来定义模糊导入中的*，比如all = ['pack1','pack2','fun1','cls1']，当from package import *时，会导入all中的包、函数、类等等。

module：是package中的一个.py文件。init.py本身也是一个module，这个module的名子就是所在文件夹的名子（包名子）。

当尝试from package import something时，import语句会首先检查something是不是init.py的变量。然后检查是不是subpackage，再检查是不是module，最后抛出ImportError。

当执行import module时，解释器会根据下面的搜索路径，搜索module1.py文件。1) 当前工作目录。2) PYTHONPATH中的目录。3) Python安装目录 (/usr/local/lib/python)。事实上，模块搜索是在保存在sys.path这个全局变量中的目录列表中进行搜索。sys.path会在解释器开始执行时被初始化成包含上面3项的列表。

当导入模块时，解释器按照sys.path列表中的目录顺序来查找导入文件（import sys，print（sys.path）可以看一下列表）

常见的import形式

```text
import package
import module
from package import module/subpackage (as XXX)
from package.subpackage import module/subpackage (as XXX)
from module import function
from package import *
错误写法：import module.function
```

同一个main_package下的各个subpackage相互调用。如sub_package1中的module1.py想调用sub_package1的module2.py、sub_package1的module2.py中的function1函数和sub_package2的module2.py

```text
from . import module2.py
from .module2.py import function1
from ..sub_package2 import module2.py
总结：“. ”是导入本package中的module，“.. ”是导入与package同级的packge中的module
```

if name == 'main'：只有在命令行运行时生效

##### setuptools的使用，如何发布py包

https://www.jianshu.com/p/ea9973091fdf

##### pip机制待学习，帮助了解包的发布















# reference

##### python官方文档（中英文）

https://docs.python.org/3.7/  
https://docs.python.org/zh-cn/3.7/  

##### python官方文档（标准库）

https://docs.python.org/zh-cn/3/library/

##### 这个也是python官方文档？

http://www.pythondoc.com/pythontutorial3/index.html

##### python源代码的github仓库  

https://github.com/python/cpython  

##### git和停用词（个人教程goto456）

https://github.com/goto456  
https://github.com/goto456/stopwords  
https://github.com/goto456/simple-git  


##### sklearn官方网站

https://scikit-learn.org/stable/index.html

##### torch官方网站

https://pytorch.org/

##### keras官网

https://keras.io/

##### mmdetection官方工程和文档

https://github.com/open-mmlab/mmdetection/  
https://mmdetection.readthedocs.io/en/latest/  

##### mmcv官方工程和文档

https://github.com/open-mmlab/mmcv  
http://mmcv.readthedocs.io/en/latest

##### jieba官方工程

https://github.com/fxsjy/jieba

##### 廖雪峰github

https://github.com/michaelliao

##### CSDN一个博主，python方面文章全面

https://blog.csdn.net/brucewong0516

