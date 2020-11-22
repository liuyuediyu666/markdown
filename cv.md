# 超分辨率（super-resolution）

比一般叉乘放大画面好很多，应用在监控、卫星图像、医学影像等。

相关算法有2014年（SRCNN）2016年（FSRCNN、ESPCN、VDSR、DRCN、RED）2017年（DRRN、lapSRN、SRDenseNet、SRGAN、EDSR）

参考连接：https://blog.csdn.net/aBlueMouse/article/details/78710553





# 过拟合

过拟合产生的原因有：训练集与真实数据分布不同，模型复杂程度高于实际问题，epoch过大学习到了噪声。

可能的训练技巧：图片增强如剪裁。BN。调整batchsize。relu及变体。dorpout。学习率衰减。权重初始化。Tfrecord实现多线程读取从而使GPU能够跑满。迁移学习时导出瓶颈层。





