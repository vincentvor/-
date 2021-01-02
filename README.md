# -
设置雷电安卓模拟器 如何 用Fiddler代理抓包
# 使用雷电模拟器代理抓包

## 工具

代理： FIddler  Proxifier CCproxy

模拟器：雷电模拟器

难点在于：怎么在手机里设置代理

## 前言

想抓安卓APP的包分析接口然后爬虫爬数据

但是我尝试了以下几种方式，都TM成功不了

1.真实手机+360免费WIFI+Xposed忽略SSL证书错误

最开始电脑配置不行，安不了模拟器，想着用手机凑合下

手机连到WIFI上后，通过WIFI自带的HTTP代理，设置到电脑的FIddler端口。

可以是可以，但是，FIddler解密Https需要设备安装上Fiddler自带的证书，可是手机总会提示证书链配置不完整总之就是SSL校验错误（傻逼SSL）

然后我找，用Xposed框架有个可以忽略SSL的插件，可是Xposed框架必须Root后才能安装，我华为，没法Root，于是用VirtualXposed框架，可以了，但是某些应用会闪退。

2.模拟器+CCproxy+Proxifier+Fiddler

模拟器网络设置为直连模式，别用桥接，否则你会被搞死的。

首先比如Fiddler设置一个端口是8000

CCproxy用二级代理，二级代理设置为FIddler（HTTP代理），然后比如它自己的代理，socks是1080，Http是808.

为什么用CCproxy作为中转跳板？

因为：

1.Fiddler的全局代理覆盖不到模拟器的进程；

2.Proxifier的全局代理可以覆盖到模拟器的进程；

3.proxifier不支持http代理，只支持socks5，socks4和https

懂了吧。。。哎。。。。

然后现在正在测试。。



然后安卓模拟器已经root，所以随便玩 安装一个Xposed





网络桥接模式，我试了无线，有限，手机USB共享网络，包括WIndows的防火墙端口也打开了，可是就是没法在模拟器内访问到电脑的端口。。倒是可以ping通。
