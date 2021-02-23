### 关于环境

##### cuda

Successfully opened dynamic library libcudart.so.10.1
Successfully opened dynamic library libcublas.so.10
Successfully opened dynamic library libcufft.so.10
Successfully opened dynamic library libcurand.so.10
Successfully opened dynamic library libcusolver.so.10
Successfully opened dynamic library libcusparse.so.10
Successfully opened dynamic library libcudnn.so.7

##### 版本和依赖

tensorflow版本2.4.0

autokeras版本1.0.12

##### 缓存位置

autokeras缓存文件地址在/home/username/.keras

### 代码

##### 参数调整

单机单卡使用(注释掉下面的)：`os.environ['CUDA_VISIBLE_DEVICES'] = '0' # 使用 GPU 0`

单机多卡使用(注释掉上面的)：`distribution_strategy=tf.distribute.MirroredStrategy(['/gpu:0', '/gpu:1'])`

暂不支持多机多卡

##### 代码正文

```python
import numpy as np
import tensorflow as tf
from tensorflow.keras.datasets import cifar10
from tensorflow.python.keras.utils.data_utils import Sequence
import autokeras as ak
import os
# os.environ['CUDA_VISIBLE_DEVICES'] = '1' # 使用 GPU 0


(x_train, y_train), (x_test, y_test) = cifar10.load_data()
print(x_train.shape)  # (50000, 28, 28)
print(y_train.shape)  # (50000,)
print(y_train[:3])    # array([7, 2, 1], dtype=uint8)

# 初始化对象
clf = ak.ImageClassifier(
    num_classes=None,  # 数据集的类别数，如果不指定会进行自动推断
    multi_label=False,  # 是否是多类别预测任务
    loss=None,  # keras的损失函数，基于类别数默认为binary_crossentropy或者categorical_crossentropy
    metrics=None,  # 可以是keras的评价指标列表，默认为accuracy
    project_name="image_classifier",  # AutoModel的名称，默认为image_classifier
    max_trials=5,  # 最大实验次数
    directory=None,  # 存储搜索结果的文件夹，如果为None则为设置为AutoModel的名称
    objective="val_loss",  # 模型的目标，val_accuracy和val_loss
    tuner='bayesian',  # 超参调优 greedy, bayesian, hyperband, random，如果不指定会先根据这个任务先选一个跑大多数模型
    overwrite=True,  # 是否覆盖已有project_name的文件夹
    seed=None,  # 随机种子
    max_model_size=None,  # 模型参数超过该模型则舍弃
    distribution_strategy=tf.distribute.MirroredStrategy(['/gpu:0', '/gpu:1']),
)

clf.fit(
    x=x_train,
    y=y_train,
    epochs=8, # epoch
    callbacks=None,
    validation_split=0.2,
    validation_data=None,
)

print('++++++++evaluate+++++++++++')
# Evaluate the best model with testing data.
print(clf.evaluate(x_test, y_test))
```

##### 备注

1、模型这里使用的cifar10数据集会自动下载，也可手动下载放在缓存目录/home/username/.keras/datasets

2、模型会使用一些预训练参数，若自动下载缓慢可手动下载放在缓存目录/home/username/.keras/models。下载地址(需要通过代码下载)：https://keras.io/api/applications/

3、clf.fit中的参数validation_split将数据划分后，每个trail只使用训练集训练，结束后使用验证集验正。最后模型确定之后会用全量数据fit一遍。对于测试集，是在fit.evaluate评估的时候使用。

4、模型保存相关见官网。





