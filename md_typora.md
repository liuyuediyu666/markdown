markdown公式很好的一篇

https://www.zybuluo.com/codeep/note/163962

markdown加入表情

https://www.webfx.com/tools/emoji-cheat-sheet/



### 其他

创建目录（可以任何地方插入，但一定要顶格写）：[toc]





### 快捷键

基于typora的，与印象笔记等其他软件快捷键有区别

| 快捷键                                | 功能                         |
| ------------------------------------- | ---------------------------- |
| ctrl + t                              | 插入表格                     |
| ctrl + 1,2,3,4,5,6                    | 设置标题                     |
| tab或shift tab                        | 行缩进，对短横线的行标有效。 |
| 短横线 + 空格                         | 行标，对行标缩进请使用tab    |
| ___                                   | 段落线                       |
| ctrl + shift + [（ctrl + ]或[可缩进） | 有序列表                     |
| ctrl + shift + ]                      | 无序列表                     |
| 行尾两个空格                          | 分行                         |
| 单层反单引号                          | 小代码块                     |
| 三层反单引号 (ctrl + shift + k)       | 大代码块                     |
| ctrl + shift + m                      | 公式块                       |
| ctrl + shift + (-/=)                  | 窗口缩放                     |
| ctrl + shift + (l/1/2/3)              | 左侧边栏设置                 |
| ctrl + b (双星括号)                   | 粗体                         |
| ctrl + u                              | 下划线                       |
| ctrl + i (单星括号)                   | 斜体                         |
|                                       |                              |
|                                       |                              |







### 链接

##### 行内式键接

（第1个方括号是链接名，第2个圆括号是链接地址，尾部双引号可加标题）

[eg of baidu](https://www.baidu.com/)

##### 参考式键接

(第1个方括号是链接名，第2个方括号是链接变量，变量定义可放在任何位置，可放在文档最后)（尾部双引号可加标题）

[eg remote baidu][id3]

[id3]:https://www.baidu.com/ "可选"

##### 参考式图片

(以!号开始，第1个方括号是链接名，第2个方括号是链接变量，变量定义可放在任何位置。参考式格式为标题时不再居中，而是左对齐)

![asdfgh][content1]

![qwerty][content2]

```python
"""参考式图片的变量写义格式如下：[content1]:data:image/png;base64,iVBORw0KGgoAA......"""
"""参考式图片的变量值需要转化为base64格式"""
import base64
with open('ab.png','rb') as f:
    img = f.read()
img64 = base64.b64encode(img)
"""也可以再转回来保存为图片"""
img=base64.b64decode(img64)
with open('abb.png','wb') as f:
    f.write(img)
```





### 绘图

##### flow流程图

定义元素：标签=>元素类型: 描述文字:>url链接（点击元素时可跳转（可选））(第1个冒号后必须有空格)

连接两个元素：-> 

条件类型判断：如示例中的cond(yes)和cond(no) 。

每个元素可以设置分支走向，默认向下（bottom），也可以用left指向左边或者用right指向右边，如示例中sub1(right)。 

```
flowchat
st=>start: 开始
e=>end: 结束
op1=>operation: 操作执行
sub1=>subroutine: 子分支
cond=>condition: 条件
io=>inputoutput: 输入输出
st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```

```flow
flowchat
st=>start: Start
e=>end: End
op1=>operation: Operation
sub1=>subroutine: Subroutine
cond=>condition: yes or no ?
io=>inputoutput: proceess something...
st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```

##### graph图表

1、graph关键字

graph TB表示流程图从上到下开始，TB表示设置该图起始的方向，方向的定义如下：

TB（ top bottom）表示从上到下

BT（bottom top）表示从下到上

RL（right left）表示从右到左

LR（left right）表示从左到右

2、节点形状

大写字母表示节点，name表示节点的名字，主要形状如下：

文本节点 B[bname]

圆角节点 C(cname)

圆形节点 D((dname))

非对称节点 E>ename]

菱形节点 F{fname}

```
graph TD
B[bname]
C(cname)
D((dname))
E>ename]
F{fname}
```

```mermaid
graph TD
B[bname]
C(cname)
D((dname))
E>ename]
F{fname}
```

3、连线

节点间的连接线可以设置多种形状，而且可以在连接线中加入文字text：

箭头连接 A1–>B1

开放连接 A2—B2

标签连接 A3-- text —B3 或者 A3—|text|B3

箭头标签连接 A4–text–>B4 或者 A4–>|text|B4

虚线开放连接 A5.-B5 或者 A5-.-B5 或者 A5…-B5

虚线箭头连接 A6.->B6 或者 A6-.->B6

标签虚线连接 A7-.text.-B7

标签虚线箭头连接 A8-.text.->B8

粗线开放连接 A9===B9

粗线箭头连接 A10==>B10

标签粗线开放连接 `A11==text===B11`

标签粗线箭头连接`A12==text==>B12`

```
graph TD
A1==TEXT===B1
A2-->|text|B2
A3..-B3	
```

```mermaid
graph TD
A1==TEXT===B1
A2-->|text|B2
A3..-B3	
```

4、示例

```
graph LR
A[方形] -->B(圆角)
B --> C{条件a}
C -->|a=1| D[结果1]
C -->|a=2| E[结果2]
F[横向流程图]
```

```mermaid
graph LR
A[方形] -->B(圆角)
B --> C{条件a}
C -->|a=1| D[结果1]
C -->|a=2| E[结果2]
F[横向流程图]
```

```
graph TD
A[方形] -->B(圆角)
B --> C{条件a}
C -->|a=1| D[结果1]
C -->|a=2| E[结果2]
F[竖向流程图]
```

```mermaid
graph TD
A[方形] -->B(圆角)
B --> C{条件a}
C -->|a=1| D[结果1]
C -->|a=2| E[结果2]
F[竖向流程图]
```



##### gantt甘特图--mermaid 

关键词说明：
title—标题
dateFormat—日期格式
section—模块
Completed—已经完成
Active—当前正在进行
Future—后续待处理
crit—关键阶段 

```
gantt
　　　dateFormat　YYYY-MM-DD
　　　title Adding GANTT diagram functionality to mermaid
　　　section A section
　　　Completed task　　:done, des1, 2014-01-06,2014-01-08
　　　Active task 　　　　:active, des2, 2014-01-09, 3d
　　　future task 　　　　:　　　  des3, after des2, 5d
　　　future task2　　　　:　　　  des4, after des3, 5d
　　　section Critical tasks
　　　Completed task in the critical line　:crit, done, 2014-01-06,24h
　　　Implement parser and json　　　　　　:crit, done, after des1, 2d
　　　Create tests for parser　　　　　　　:crit, active, 3d
　　　Future task in critical line　　　　　:crit, 5d
　　　Create tests for renderer　　　　　　:2d
　　　Add to ,mermaid　　　　　　　　　　　:1d
```

```mermaid
gantt
　　　dateFormat　YYYY-MM-DD
　　　title Adding GANTT diagram functionality to mermaid
　　　section A section
　　　Completed task　　:done, des1, 2014-01-06,2014-01-08
　　　Active task 　　　　:active, des2, 2014-01-09, 3d
　　　future task 　　　　:　　　  des3, after des2, 5d
　　　future task2　　　　:　　　  des4, after des3, 5d
　　　section Critical tasks
　　　Completed task in the critical line　:crit, done, 2014-01-06,24h
　　　Implement parser and json　　　　　　:crit, done, after des1, 2d
　　　Create tests for parser　　　　　　　:crit, active, 3d
　　　Future task in critical line　　　　　:crit, 5d
　　　Create tests for renderer　　　　　　:2d
　　　Add to ,mermaid　　　　　　　　　　　:1d
```

















































[content1]:data:image/png;base64,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



[content2]:data:image/png;base64,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

