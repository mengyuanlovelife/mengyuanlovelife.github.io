---
layout: post
title: OpenWrt关闭IPV6
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
tags: [OpenWrt]
---
#### 前言
首先，我是IPV6的受害者，家里网络是没有IPV6地址的，机场也不支持IPV6，我开着飞机周游世界时，遇到的一些支持IPV6的网站就出现打不开的现象，像谷歌，GITHUB，EPIC······。所以，我要关闭有关IPV6的所有设置，这也是写这篇文章的原因。

#### WAN口设置

##### 在 **网络** > **网卡** 中，有个名为**WAN6**的接口，我们把他删除掉
![](/assets/images/openwrt/v6-1.nuexini)
##### 在**WAN接口**中，我们点击 **修改/编辑**，点击 **DHCP服务器 > IPv6设置**
![](/assets/images/openwrt/v6-2.nuexini)
##### RA 服务 & DHCPv6 服务 & NDP 代理 选择 **已禁用**
##### 然后 点击 **高级设置**
![](/assets/images/openwrt/v6-3.nuexini)
##### 把 **IPv6 分配长度** 选择 **已禁用**
##### 在**大雕**的版本中，把 **使用内置的 IPv6 管理** 取消勾选
![](/assets/images/openwrt/v6-4.nuexini)
##### 最后，点击 **保存** （这个保存指↓）
![](/assets/images/openwrt/v6-5.nuexini)

#### LAN口设置
##### 同 **WAN口设置** ，只是修改对象选择 **LAN口**
##### 修改完毕后，点击 **保存**

#### 保存并应用
##### 做完步骤1和步骤2后，还有最后一步，在 全局网络选项 中 IPv6 ULA 前缀 内容 清除
![](/assets/images/openwrt/v6-7.nuexini)
##### 点击保存并应用，即可完成操作
![](/assets/images/openwrt/v6-8.webp)

#### 防火墙设置
##### 在 **网络 > 防火墙** 中，选择 **通信规则**

![](/assets/images/openwrt/v6-9.nuexini)
##### 把所有为**入站IPv6** 或 **转发IPv6** 或 **出站IPv6** 的 **启用** 放弃勾选，不启用之后，点击**保存并应用**

#### DHCP/DNS设置
##### 在 **网络 > DHCP/DNS** 中，选择 **高级设置**
##### 在大雕的OpenWrt (lede)中，是有 **禁止解析IPv6 DNS记录** 的，但是在原版的OpenWrt中，是没有这个选项的
![](/assets/images/openwrt/v6-11.webp)
##### 下图为原版 **OpenWrt > 网络 > DHCP/DNS > 高级设置**
![](/assets/images/openwrt/v6-12.nuexini)

#### 下面需要用到SSH操作（如何开启SSH请自己解决）
- SSH连接路由器
- 输入第一条命令，按回车执行
```bash
uci set dhcp.@dnsmasq[0].filter_aaaa='1' #1为禁止，0启用

uci commit dhcp

/etc/init.d/odhcpd disable

echo 'net.ipv6.conf.all.disable_ipv6 = 1' >> /etc/sysctl.conf

sysctl -p /etc/sysctl.conf #所有接口禁用ipv6

echo 'net.ipv6.conf.eth0.disable_ipv6 = 1' >> /etc/sysctl.conf

sysctl -p /etc/sysctl.conf #禁用某一个指定接口的IPv6（例如：eh0）
```
#### 结尾
重启路由器