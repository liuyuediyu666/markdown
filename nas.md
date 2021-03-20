# 学习

netflix    

openwrt    

梅林固件   

k2p    

斐讯天天链n1    

netgear    

linksys    

ap面版    

More Actions

就上车V2Ray了

gui客户端

ros软路由

网件

shr空间

gen8

反向代理

vps

智能路由器的力量之源：OpenWRT

国产播放器的大奶妈：FFmpeg

#### 一些网络知识需要学习

五层模型
https://zhuanlan.zhihu.com/p/84316213

OSI参考模型七层模型
https://www.cnblogs.com/qishui/p/5428938.html

冲突域和广播域的区分
https://blog.csdn.net/danchaofan1982/article/details/100150746

关于通信：时钟信号、时钟频率、时钟同步、发送时钟、接收时钟、串行通信、并行通信、异步通信、I2C总线、SCL线、同源时钟、同相位时钟、同时钟域时钟。





# 推荐

##### 推荐1

nas群杨浪内网传透：开放注册1天，45元/月（免费1月），无限流量，无连接数限制，最大3M-4M。不会用的可私聊杨浪设置。

http://nps.iokle.com:8080/login/index

已注册：avater，udiwqj_66

##### 推荐2

大公网买了10年的域名。

##### 推荐3

内网穿透工具——ZeroTier One的使用

https://www.jianshu.com/p/eefddb256ad7

##### 推荐4（群友分享，暂不知ssr如何用）

ssr://MTAxLjMyLjIxLjIwNjo1MDAwOm9yaWdpbjphZXMtMjU2LWNmYjpwbGFpbjphVzlyYkdVdWFHcw

##### 推荐5（nginx）

有三大功能，正向代理，反向代理，用于搭建基于域名的虚拟主机。











# 问答

问：为什么建议在路由器做DDNS，群晖本身也能做DDNS呀。

答：路由器一般坏不了，群晖手痒升级一下也许就变砖头了。术业有专攻，群晖主要是文件共享服务器。当然下载也强，打通ip之后再装tr+utorrent+qbtorrent，几十T老电影剧集就可以日夜不停的拖了。

另一答：路由器和群晖做DDNS都一样。实现功能不一样。如果是用域名绑定到路由那么你路由上映射的所有端口和主机都可以享用，建义在路由做DDNS。

远程唤醒：远程唤醒需要在路由器里面设置ddns解析，从群晖里ddns是无法唤醒的。远程唤醒需要白群晖，黑的不行。软路由固件里都带远程唤星，填进去群晖的mac地址就行了，应该是这样。

另另一答：买个蒲公英路由器做vpn比较简单。





# 路由

### 软路由

知乎搜优质：软路由是什么

目前比较成熟和主流的方案是使用 英特尔赛扬 J1900 处理器，如果你的要求不是特别高，那么这颗 CPU 足以满足一个普通家庭的全部需求。除了 J1900 ，英特尔凌动 N2600 也是个不错的选择，搭载这两款 CPU 的路由器价格也相对便宜。

这两套方案虽然经典但也比较陈旧了，如果你没有预算上的压力，未来想要拓展更高级的功能（比如虚拟化），那么推荐大家选择 英特尔赛扬 3215U，它的制程更加优秀，可以提供更好的虚拟化支持，也是绝大多数软路由玩家最终的选择。

### 内网穿透

一款轻量级、高性能、功能强大的内网穿透代理服务器（来自微信nas群，杨浪）

http://124.156.159.172:8080/login/index

https://github.com/ehang-io/nps

### VPS

搬瓦工

其他vps

https://www.zhihu.com/topic/20088499/hot





### 路由方案参考

网件R7000--700
网件R8500
蒲公英X5
网件RAX40 AX3000M--1000
华硕AC68U等--700
华硕RT-AC68U等--1000

如果题主有多个设备同时访问NAS、同时传输大文件的需求，还可以考虑选择带有“链路聚合”功能的路由，前提是NAS支持“链路聚合”

如果有条件喜欢折腾：买千兆网口软路由，可以装插件，实现动态域名解析、frp穿透、远程唤醒、翻qiang等等。

------------------------------------------------------------------------------------

搭配一个lede的软路由，用frp做外网访问，用ss你懂的

如果喜欢华硕的，RT-AC68U/RT-AC66U-B1好点，可刷梅林，本来的固件也不错，和
R7000差不多同级别吧。

家用路由器只选择网件或者华硕。总的来说，网件配置高，性价比高，固件不好用，一般都刷梅林，很稳， 100平方内的房子信号都很好。华硕相对不讲性价比，本来的固件就很好。

如果不喜欢刷刷机，买 网件7000p好点

路由器，建议选择华硕或者网件的路由器，找到好刷机的那种，能在路由器端安装小插件。家里目前型号是GT-AC5300，支持链路聚合，给nas两个网口都插上后，网速叠加那种

------------------------------------------------------------------------------------

不想折腾又有钱的直接买网件R7000或都华硕AU68 的路由，起码要600以上的，没钱的就买腾达AC9。没钱又不怕折腾的买个星际蜗牛双千兆网卡的，300以下做个软路由，再买个8口千兆交换机100以下，性能绝对比1000以上的路由器都好，留着小米一代做AP就可以了。

图中拿性能较强的AC-88U做为主路由+WiFi，我刚查了一下华硕官网，AC-88U支持聚合链路，



ESXI+ROS+LEDE软路由设置简述，ROS简要设置上网，LEDE设为旁路作为网关和DNS，设置简介明了。

B站上面的教程

https://www.bilibili.com/video/av71109287



知乎上关于软路由不错的

https://www.zhihu.com/question/292856961/answer/979736231?utm_medium=social&utm_oi=724742881306234880&utm_source=wechat_session&s_r=0

### 王晓明有道云

主路由品牌：

斐讯n1

edgerouter x

N3865U

i3 7200U

软路由一般是作为旁路或者与AP搭配，这又增加了不少投入。

即使选择了N3865U，必须要上虚拟环境，玩双路由，所以至少需要8G或以上内存，16G或以上硬盘

I211千兆网卡   135

82583 88

82574 175

正常布置AC POE交换机即可，然后购买支持WIFI6的AP设备。

1，AC路由器指的是带AC功能的路由器。

2，目前Tplink等厂商均推出了WIFI 6的AP设备，但是价格普遍偏高。

如果你想要布置WIFI6的网络，那么你可以正常布置路由、AC、POE交换机，然后购置WIFI6 AP设备即可。

关闭路由器的ipv6模式

4.手动配置路由器的dns服务器地址

5.还没想出来，溜了先

https://item.m.jd.com/product/26366944253.html?wxa_abtest=a&utm_source=iosapp&utm_medium=appshare&utm_campaign=t_335139774&utm_term=CopyURL&ad_od=share







### 路由器刷固件，翻墙代理屏蔽广告等相关操作郭世纪

GitHub - coolsnowwolf/openwrt: OpenWrt Stable Version
https://github.com/coolsnowwolf/openwrt
coolsnowwolf · GitHub
https://github.com/coolsnowwolf
[OpenWrt Wiki] 欢迎访问 OpenWrt 项目
https://openwrt.org/zh/start







# 群晖

Synology群晖型号对比：DS920 +，DS420 +，DS720 +，DS220+

https://360nas.com/archives/820.html

群晖经典教程

https://www.cnblogs.com/hester/p/4988755.html







# 视频

### 视频网站

免费电影网站

https://www.80s.tw/

### 爬视频

推荐一个you-get，是一个python包，下载视频神器，B站教程

https://www.bilibili.com/video/BV1jV411U7zb?p=4

p站多线程下载视频（python代码）

https://blog.csdn.net/weixin_44879856/article/details/105885950

安利一个下载b站、youtube等网站视频的工具

https://blog.csdn.net/wongnoubo/article/details/89199059

超好用的下载器——IDM

https://zhuanlan.zhihu.com/p/76970353?from_voters_page=true

### 播放器

kodi播放器

potplater

### 刮削器

https://blog.csdn.net/qq_20090265/article/details/109769288

豆瓣刮削

















​      