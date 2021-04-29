# xshell

ssh whl@192.168.1.23：登录服务器

exit：退出登录  

sz 文件路径：将文件输出到本地电脑桌面

Ctrl+D：退出

在IDE中双击窗口标签，复制一个链接到新窗口，无需输密码。

type 'help' to learn how to use xshell prompt



Ctrl +s 在Xshell终端上是屏幕锁死

Ctrl+q 退出锁死



# CV

##### 超分辨率（super-resolution）

比一般叉乘放大画面好很多，应用在监控、卫星图像、医学影像等。

相关算法有2014年（SRCNN）2016年（FSRCNN、ESPCN、VDSR、DRCN、RED）2017年（DRRN、lapSRN、SRDenseNet、SRGAN、EDSR）

参考连接：https://blog.csdn.net/aBlueMouse/article/details/78710553



##### 华为vega

https://github.com/huawei-noah/vega

https://www.noahlab.com.hk/opensource/vega/



##### 过拟合

过拟合产生的原因有：训练集与真实数据分布不同，模型复杂程度高于实际问题，epoch过大学习到了噪声。

可能的训练技巧：图片增强如剪裁。BN。调整batchsize。relu及变体。dorpout。学习率衰减。权重初始化。Tfrecord实现多线程读取从而使GPU能够跑满。迁移学习时导出瓶颈层。





##### 应用场景（可能的）

电梯电动车识别。

高空抛物识别。

人流量监控。

垃圾分类。 

防跳桥系统。

文明养犬系统。

地铁安检透视。

智能升级视频清晰度,super resolution深度学习提升分辨率。

自动售卖机统计。

文本识别聊天记录，感兴趣内容自动报警。

自动去水印



##### 其他


gpt2Chinese的创始人居然在南京，

你想成为AI大神，去把paperwithcode上某一方向的论文看完，然后把其中的代码落地调试，在这个领域你就是大神。在中国的难题是你需要结合具体的行业落地而且产生经济效益，用某一个点引起病毒传播，这样你就火了。但中国的教育文化基因是极度不鼓励营销，中国的创业者科学家和技术人员对于营销没什么有效的方法论，

尤其是Caltech101和ImageNet数据库   检索量挺大的







# knowledge_graph

推荐一个东南大学知识图谱的课程（李一繁）

https://github.com/npubird/KnowledgeGraphCourse



# computer_science

遗传算法

粒子群算法

蚁群算法

模拟退火算法

小波

傅里叶

爬山算法

用牛顿法，求6的开方

##### 计算机操作系统、计算机网络

https://github.com/CyC2018/CS-Notes

##### 孤立森林

https://zhuanlan.zhihu.com/p/74508141











# hadoop

##### 向hadoop集群上传文件  

hadoop fs -mkdir /whl # 新建文件夹  

从本地拖到Xsheel窗口  

hadoop fs -put uber-raw-data-sep14.csv /whl/ # 执行上传命令  

hadoop fs -rm -r -skipTrash /path_to_file/file_name  # 执行删除文件或文件夹  





# hardware

硬盘笼

30系列显卡是公版最好吗？

不可能啊，目前华硕猛禽最好，供电默频算封顶的了。

##### CPU知识，关于老化等

下面是抄知乎博主老狼的文章，知乎已关注

http://www.360doc.com/content/18/0904/11/59057945_783757304.shtml

##### 隔壁网渠道价格2020年的

隔壁网可淘宝交易。价格如下：（隔壁网家的群晖是国行，总代是世平。）

DS920+（3800元）DS420+（3300元）

银河4T800，8T1150，10T氦气1660。酷狼4T750，8T1300，10T氦气1800。

隔壁网客服对氦气盘评价：银河盘吵点但稳定，酷狼静音但贵。硬盘3年换新5年保修。银河氦气就是个低温效果，漏气死。硬盘是很怕热的，尽量通风要好。





# html





# mathematics

0-1标准化与标准差标准化的区别？一个是映射到0-1区间，一个是映射到中心为0的区间，没太大区别，都是改变截距和按比例缩放。并没有改变点之间的距离分布，网上大部分说的有误。

盒须图的上下须长度是怎么确定的？以最外边的点为界，但不超过1.5倍IQR。

卡方检验。。



# pmml







# tensorboard

使用tensorboard查看linux服务器上的记录

先在linux服务器工程目录下执行：tensorboard --logdir=tf_log_path --host=0.0.0.0 --port 6006

然后在浏览器输入网址：http://172.16.2.119:6006

https://blog.csdn.net/ichglauben/article/details/88389403

https://baijiahao.baidu.com/s?id=1650159391593079141&wfr=spider&for=pc





# yaml

用于github工程中的配置文件，比json文件更好用

yaml语言，阮一峰

http://www.ruanyifeng.com/blog/2016/07/yaml.html







# you-get

VIP会员用cooki解决，可百度一下。因为下VIP会出现下载的视频不完整。
音视频合并可用格式工厂

第一步 pip install you-get

第二步 you-get -i url(这是视频地址)

第三步 you-get --format=dash-flv720(这个是你想要的清晰度文件) -o path(这是输出路径，省略的话下载到当前路径) url(这是视频地址)

注意1：you-get支持哪些网站可以百度一下，有个列表

注意2：有些视频下不完整，是因为VIP会员视频的问题。可百度一下，可充会员用cooki解决

注意3：视频和音频是分开的，可以用格式工厂合并一下











