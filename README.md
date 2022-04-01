# learn-Apollo_6.0

对Apollo6.0的学习记录

## 1、环境配置

### 1.1、双系统

硬件条件：

- 笔记本电脑：小新 pro 14
  
  <img src='./figs/README/小新.png' style='zoom:30%;' />

- 显示器：飞利浦，三头供电，双向type-c口通信

软件条件：

- 已安装：windows 11 家庭版
- 待安装：ubuntu 20.04.4 LTS

系统安装就是正常流程，下载镜像、启动盘制作、磁盘分区、重启关secure boot、重启进boot loader安装、ubuntu grub引导设置；详细可以参见[这个链接](https://blog.csdn.net/qq_31347869/article/details/123357179)；

小新pro 14这个电脑不知道为什么，显卡or屏幕对ubuntu支持的不好，18.04和20.04都会闪屏；同时因为驱动问题，自带的触控板和键盘会失效；但实测连接外接显示器，然后把显示器设置调整为：

<img src='./figs/README/飞利浦.png' style='zoom:40%;' />

显示是正常的；过程适当参考[这个链接](https://blog.csdn.net/u012258905/article/details/121092545)。

### 1.2、Apollo6.0安装
