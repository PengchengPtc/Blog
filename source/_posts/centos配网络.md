---
title: centos配网络
date: 2021-05-03 17:58:20
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Linux
tags:
	- Linux
---

## 配置静态ip

```bash
$ vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

修改为


```bash
BOOTPROTO="static" #dhcp改为static 
ONBOOT="yes" #开机启用本配置 
IPADDR=192.168.100.10 #静态IP（网段为：192.168.100.0） 
GATEWAY=192.168.100.2 #默认网关(虚拟机网关) 
NETMASK=255.255.255.0 #子网掩码 
DNS1=114.114.114.114 #DNS 配置
```

重启网卡

```bash
$ service network restart
```

测试

```bash
$ ping www.baidu.com
```

虚拟机的网关要和主机一致