---
layout: post
title: OpenWrt设置PPPOE拨号
categories: 网络技术与技巧
banner:
  image: ./assets/images/banners/emoji.jpg
  opacity: 0.618
  background: "#000"
  height: "50vh"
  min_height: "50vh"
  heading_style: "font-size: 2.45em; font-weight: bold; "
  subheading_style: "color: gold"
sitemap: true
tags: [PPPOE拨号]
---
#### 前言
##### 设置前请先确定你的光猫是否支持桥接，是否支持获取带宽账号密码，宽带账号密码可以咨询安装光猫的师傅或者营业厅，本文教程演示支持OpenWrt 和 Lede，市面上第三方软路由只是界面不同，但是操作步骤是一样的，大家可以参考下面的教程进行PPPOE拨号设置。

#### 操作步骤

##### 1.进入 OpenWrt或Lede 软路由系统界面，填写用户名和密码进行登录，大部分的登录账号：root，密码：password，个别密码为空。
![](/assets/images/openwrt/bh-1.webp)
##### 2.进入系统界面后，选择打开网络 -> 接口，进入接口总览页面。
![](/assets/images/openwrt/bh-2.webp)
##### 3.进入接口总览选项后，点击WAN接口后面的修改，进行编辑。
![](/assets/images/openwrt/bh-3.webp)
##### 4.进入WAN口编辑后，点击DHCP客户端，选择 PPPoE拨号。
![](/assets/images/openwrt/bh-4.webp)
##### 5.选择完成后，点击确定切换 PPPoe协议，一定要记得点击，如下图：
![](/assets/images/openwrt/bh-5.webp)
##### 6.然后就能看到填写宽带账号密码的地方，填好宽带账号密码，然后保存应用，等待1分钟就会联网。
![](/assets/images/openwrt/bh-6.webp)