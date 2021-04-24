# mmtracking安装

按照docs目录下的install.md文件安装即可，注意python要3.7（3.6有未知错误）。

为什么要使用镜像？因为服务器centos的gcc版本为4.8.5，而mmdetection要求gcc4.9。

为什么要使用镜像中的conda环境。因为自带的python为3.6，而mmtracking要求py3.y。

请使用docker镜像：vistart/mmdetection:latest，先安装conda，再新建环境指定py3.7

软件版本如下：

```
addict              2.4.0
attrs               20.3.0
certifi             2020.12.5
cycler              0.10.0
Cython              0.29.23
dotty-dict          1.3.0
flake8              3.9.1
flake8-import-order 0.18.1
importlib-metadata  4.0.1
iniconfig           1.1.1
kiwisolver          1.3.1
matplotlib          3.4.1
mccabe              0.6.1
mkl-fft             1.3.0
mkl-random          1.1.1
mkl-service         2.3.0
mmcls               0.10.0
mmcv-full           1.3.1               /home/whl/mmcv-master
mmdet               2.11.0              /home/whl/mmdetection-master
mmpycocotools       12.0.3
mmtrack             0.5.0               /home/whl/mmtracking-master
motmetrics          1.2.0
numpy               1.19.2
olefile             0.46
opencv-python       4.5.1.48
packaging           20.9
pandas              1.2.4
Pillow              8.2.0
pip                 21.0.1
pluggy              0.13.1
py                  1.10.0
py-cpuinfo          8.0.0
pycocotools         2.0.2
pycodestyle         2.7.0
pyflakes            2.3.1
pyparsing           2.4.7
pytest              6.2.3
pytest-benchmark    3.4.1
python-dateutil     2.8.1
pytz                2021.1
PyYAML              5.4.1
scipy               1.6.2
seaborn             0.11.1
setuptools          52.0.0.post20210125
setuptools-scm      6.0.1
six                 1.15.0
terminaltables      3.1.0
toml                0.10.2
torch               1.8.1
torchvision         0.9.1
typing-extensions   3.7.4.3
wheel               0.36.2
xmltodict           0.12.0
yapf                0.31.0
zipp                3.4.1
```

注意：dotty-dict有可能自动安装失败，可以手动下载工程手动安装，不要用pip安装。地址如下：

https://github.com/pawelzny/dotty_dict

##### 安装过程中会出现import mmcv报错，最后报错显示如下：

ImportError: libGL.so.1: cannot open shared object file: No such file or directory

看下面解决方案，这应该是docker一个通用问题。

https://blog.csdn.net/qq_35516745/article/details/103822597













# mmdet的docker安装过程简略

1、安装docker（省略）

2、找到镜像并下载

docker search mmdetection

docker image pull vistart/mmdetection:latest

3、启动一个容器

docker run \
-dit \
--gpus all \
--name v24mmd21pm19 \
--mount type=bind,source=/data/imgdata_vol/detect_data,target=/mnt/detect_data \
--mount type=bind,source=/data/checkpoints_vol/,target=/mnt/checkpoints \
--mount type=bind,source=/data/utils_vol,target=/mnt/utils \
-p 2244:22 \
vistart/mmdetection:latest

进入容器

docker exec -it mmdetec bash

创建软连接

ln -s /mnt/checkpoints/checkpoints/ /mmdetection/checkpoints

ln -s /mnt/detect_data/ /mmdetection/data

4、先卸载mmcv，然后pip3 install安装mmcv-full==1.1.3（不能用清华镜像，编译时间10分钟以上）

注意：mmcv-full==1.1.3仅兼容mmdet2.4版本。如果是mmdet2.5版本请安装mmcv-full==1.1.5。

5、在mmcv安装好的基础上，再升级mmdet（pip3list中已有一个mmdet2.2.0，不用管，卸载不掉）

pip3 install --upgrade mmdet -i https://pypi.tuna.tsinghua.edu.cn/simple

6、对容器换源（可略过，此镜像已换源），需要使用apt-get update更新一下换过的源

参考https://www.cnblogs.com/aaronthon/p/10002153.html

7、安装vim。apt-get install vim

8、推理示例

注意改下代码：vim /mmdetection/tools/test.py。将data_loader中的参数改为workers_per_gpu=1

python tools/test.py configs/ssd/ssd512_coco.py \
checkpoints/ssd512_coco_20200308-038c5591.pth \
--show-dir /mnt/utils/ssd512_coco_results

python tools/test.py configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
    /mnt/utils/ckpoints/hrsid_5epoch_trainvalsame_201022/epoch_5.pth \
    --show-dir /mnt/utils/newa20201026_results

python tools/test.py configs/res2net/mask_rcnn_r2_101_fpn_2x_coco.py \
checkpoints/mask_rcnn_r2_101_fpn_2x_coco-17f061e8.pth \
--show-dir /mnt/utils/mask_rcnn_r2_101_fpn_2x_coco_results

python tools/test.py configs/regnet/retinanet_regnetx-1.6GF_fpn_1x_coco.py \
checkpoints/retinanet_regnetx-1.6GF_fpn_1x_coco_20200517_191403-37009a9d.pth \
--show-dir /mnt/utils/retinanet_regnetx-1.6GF_fpn_1x_coco_results

9、训练示例

注意：训练会产生很多core.xxxxxx大文件，在下面两个文件夹中，会导致磁盘空间不足。直接删除空间没变化？

/var/lib/docker/overlay2/99411adf821f61e481afd8d986c02a2becf89ebc44324096b430f3ed6885df2a/merged/mmdetection

/var/lib/docker/overlay2/99411adf821f61e481afd8d986c02a2becf89ebc44324096b430f3ed6885df2a/diff/mmdetection

训练ssd512

vim /mmdetection/configs/ssd/ssd512_coco.py

将data中的参数改为workers_per_gpu=1,samples_per_gpu=2（根据GPU内存调整，不要溢出）

python tools/train.py  configs/ssd/ssd512_coco.py --work-dir /mnt/utils/ckpoints/ah201015

训练faster_rcnn_r50_fpn

vim /mmdetection/configs/\_base\_/datasets/coco_detection.py

将data中的参数改为workers_per_gpu=1,samples_per_gpu=1（根据GPU内存调整，这里1不会溢出）

python tools/train.py  configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/cb201022

训练cascade_rcnn_r50_fpn

python tools/train.py  configs/cascade_rcnn/cascade_rcnn_r50_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/aa201016

### 参数调整

调整类名

vim /mmdetection/mmdet/core/evaluation/class_names.py 

调整类名

vim /mmdetection/mmdet/datasets/coco.py 

调整类别数

vim /mmdetection/configs/_base_/models/faster_rcnn_r50_fpn.py 

vim /mmdetection/configs/_base_/models/cascade_rcnn_r50_fpn.py

vim /mmdetection/configs/_base_/models/retinanet_r50_fpn.py

调整尺寸，调整evaluation interval

vim /mmdetection/configs/_base_/datasets/coco_detection.py 

调整学习率，调整epoch

vim /mmdetection/configs/_base_/schedules/schedule_1x.py 

vim /mmdetection/configs/retinanet/retinanet_r50_fpn_1x_coco.py

调整checkpoint_config interval，调整log_config interval

vim /mmdetection/configs/_base_/default_runtime.py

##### x101主干网

SOTA(cascade_rcnn_x101_64x4d_fpn_1x_coco.py)(44.7)

python tools/train.py  configs/cascade_rcnn/cascade_rcnn_x101_64x4d_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_cascade_x101_20201022

SOTA(faster_rcnn_x101_64x4d_fpn_1x_coco.py)(44.2)

python tools/train.py  configs/faster_rcnn/faster_rcnn_x101_64x4d_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_faster_x101_20201022

SOTA(retinanet_x101_64x4d_fpn_1x_coco.py)(44.0)

python tools/train.py  configs/retinanet/retinanet_x101_64x4d_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_retinanet_x101_20201022

##### r50主干网

python tools/train.py  configs/cascade_rcnn/cascade_rcnn_r50_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_cascade_r50_20201023

python tools/train.py  configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_faster_r50_20201023

python tools/train.py  configs/retinanet/retinanet_r50_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_retinanet_r50_20201023

##### r101主干网

python tools/train.py  configs/cascade_rcnn/cascade_rcnn_r101_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_cascade_r101_20201023

python tools/train.py  configs/faster_rcnn/faster_rcnn_r101_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_faster_r101_20201023

python tools/train.py  configs/retinanet/retinanet_r101_fpn_1x_coco.py --work-dir /mnt/utils/ckpoints/rsod_retinanet_r101_20201023

##### 推理

python tools/test.py configs/cascade_rcnn/cascade_rcnn_r50_fpn_1x_coco.py /mnt/utils/ckpoints/hrsid_cascade_r50_20201024/epoch_9.pth --show-dir /mnt/utils/hrsid_cascade_r50

python tools/test.py configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py /mnt/checkpoints/checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth --show-dir /mnt/utils/asdf

# mmdetection教程

##### 涉及docker使用

https://blog.csdn.net/red_stone1/article/details/103717757

https://zhuanlan.zhihu.com/p/120829265

https://blog.csdn.net/qq_24282081/article/details/105197710

### mmdetection

mmdetection源码和文档

https://github.com/open-mmlab/mmdetection/

https://mmdetection.readthedocs.io/en/latest/

mmdetection学习材料

关于注册机制的知乎大神讲解

https://zhuanlan.zhihu.com/p/113775697

https://zhuanlan.zhihu.com/p/114688143

知乎较早的一个介绍，比较浅

https://zhuanlan.zhihu.com/p/101225733

也有关于注册机制的讲解

https://blog.csdn.net/zhangjipinggom/article/details/107630215

关于自定义数据集的，最后的几个链接不错，重点推荐

https://blog.csdn.net/duanyajun987/article/details/97659685

大专栏

https://www.dazhuanlan.com/2019/11/20/5dd4ae85e8732/?__cf_chl_jschl_tk__=356813d2fe39960112715a08ec22dc0d68640bcc-1601365130-0-Ac9hPOSFB2AJtweUd2Z32AT2ow_0yQbqAKi93cuiPF0p326FSzgHK4qNOa2KjTzhCQuS_vQts-rRAhXZlP0p3a5p0WFRgNQ7v5QEtbHYrsMe978r4eBhUvmDaTFHBggWNWdqeC7KlGv3pUh7a_5uM22FWwNukkAGZdmFq9UTY4XVR_kPSnpeS3NyArrUiao078g7d6rJiV1Csj6uGm8p5VG1uezs_otAFbd2RTVLGIalZXuXhBt8x0EfokR9uUX1y9goHBO7DpqHmILzKVfgub8qCRZdriihN0xSP9BB-b_giCGTMy3cnyOa0wkljnH8vA

https://zhuanlan.zhihu.com/c_1159526395804725248

https://www.freesion.com/article/5564134964/

https://www.zhihu.com/question/294578141?sort=created

https://blog.csdn.net/syysyf99/article/details/96574325

自定义数据训练

https://zhuanlan.zhihu.com/p/101983661

最小复刻版mini版mmdetection

https://github.com/hhaAndroid/mmdetection-mini

mmdetection魔改源码进行视频检测

https://www.bilibili.com/video/av796712872/

https://www.bilibili.com/video/av286735980

pycocotools源码

https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/coco.py

B站关于mmdetection的教程，里面有youget教程。

https://www.bilibili.com/video/BV1jV411U7zb?p=1

B站mmdetection扫肓教程

https://www.bilibili.com/video/BV1RC4y1h7TB/?spm_id_from=333.788.videocard.1

CSDN较新的系列教程，详细全面

https://blog.csdn.net/Skies_/article/details/106974243

https://blog.csdn.net/Skies_/article/details/108051029

https://blog.csdn.net/Skies_/article/details/108142131

https://blog.csdn.net/Skies_/article/details/108274366



