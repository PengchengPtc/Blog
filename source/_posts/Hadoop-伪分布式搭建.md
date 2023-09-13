---
title: Hadoop_伪分布式搭建
date: 2021-01-25 09:28:35
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Hadoop
tags:
	- Hadoop
---

### 准备工作：

使用Hadoop，要关闭防火墙。

### 安装jdk：Java虚拟机

凡是Java开发的程序，必须运行在Java虚拟机上面。Hadoop就是Java开发的。

解压命令：

```bash
-C是指定目录，~表示的是当前目录，演示的是root目录
tar zxvf 文件名 -C ~
```

创建软连接：把刚解压的文件重新定义一个名字。l

```bash
ln -s jdk1.8.0_171/ jdk
```

配置环境变量：如果不配，敲Java命令，没法调用jdk

```bash
vi /etc/profile
```

拉到最低：做以下配置

```bash
//指定路径  //指定架包
export JAVA_HOME=/root/jdk
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:.
```

source一下，使得环境变量生效

```bash
source /etc/profile
```

输入Java，会有Java指令

查看Java版本:

```bash
java -version
```

确定oppenssl version,openssh-server是否安装，设置免密钥。一般centos7是默认安装的。

```bash
openssl version
```

如果没有安装：解压，创建软连接，再配置环境变量。

```bash
yum -y install openssl
```

### 安装Hadoop：

解压

```bash
-C是指定目录，~表示的是当前目录，演示的是root目录
tar zxvf 文件名 -C ~
tar zxvf hadoop-2.7.3.tar.gz  -C ~
```

创建软链接

```bash
ln -s hadoop-2.7.3 hadoop
```

然后配置环境变量：去配置Java的环境变量里面去加：

```shell
export HADOOP_HOME=/root/hadoop
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
```

使环境变量生效：

```bash
source /etc/profile
```

输入hdfs查看是否Hadoop是否安装好。

### 修改Hadoop的配置：进入目录进行配置，要看你安装的目录。

```bash
cd /root/hadoop/etc/hadoop
```

```bash
## 查看里面全部是配置文件
ls
```

配置Javahome:因为Hadoop是运行在Java虚拟机上的。

```bash
vi hadoop-env.sh
```

[![sbZVr8.png](https://s3.ax1x.com/2021/01/24/sbZVr8.png)](https://imgchr.com/i/sbZVr8)

$JAVA_HONE改为 /root/jdk

### 伪分布模式：

配置主机名映射：

1.配置主机名：vi  /etc/hosts 结尾加上

[![sqd3id.png](https://s3.ax1x.com/2021/01/25/sqd3id.png)](https://imgchr.com/i/sqd3id)

```bash
192.168.126.10 PTC1
```

2,通过ssh-key生成一个RSA的密钥对：配药匙

```bash
ssh-keygen -t rsa -P ''
```

3.公钥追加到~ssh/authorized_keys文件中:把药匙给你的机器名

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub PTC1
```

yes，并输入root密码。

### 测试免密钥是否成功

```bash
ssh PTC1
```

[![sqdwdg.png](https://s3.ax1x.com/2021/01/25/sqdwdg.png)](https://imgchr.com/i/sqdwdg)

退出：

```bash
exit
```

### 安装：

配置hdfs-site.xml

```bash
### 路径
cd /root/hadoop/etc/hadoop
```

```bash
vi hdfs-site.xml
```

### configuration标签里面配：数据冗余是指数据在存储器中的不必要的多次重复存储。

```xml
<!--表示数据块的冗余度,默认是：3-->
<configuration>
	<property>
	    <name>dfs.replication</name>
	    <value>1</value>
	</property>
</configuration>
```

### 配置core-site.xml

```xml
<configuration>
	<!--配置NameNode地址。9000是RPC通信端口-->
	<property>
	    <name>fs.defaultFS</name>
	    <value>hdfs://192.168.171.101:8020</value>
	</property>
	<property>
	<!--HDFS数据库保存在Linux的哪个目录，默认值时linux的tmp目录-->
	    <name>hadoop.tmp.dir</name>
	    <value>/root/hadoop/tmp</value>
	</property>
</configuration>
```

配置mapred-site.xml:默认没有：cp mapred-site.xml.template mapred-site.xml(复制一个)

```xml
<!--MR运行的框架-->
<configuration>
	<property>
	    <name>mapreduce.framework.name</name>
	    <value>yarn</value>
	</property>
</configuration>
```

配置 yarn-site.xml

```xml
<configuration>
	<!--Yarn的主节点RM的位置-->
	<property>
	    <name>yarn.resourcemanager.hostname</name>
	    <value>192.168.171.101</value>
	</property>
	
	<!--MapReduce运行方式：shuffle洗牌-->
	<property>
	    <name>yarn.nodemanager.aux-services</name>
	    <value>mapreduce_shuffle</value>
	</property>
</configuration>
```

格式化:只能一次

```bash
 $ hdfs namenode -format
```

[![sqdWeU.png](https://s3.ax1x.com/2021/01/25/sqdWeU.png)](https://imgchr.com/i/sqdWeU)

```bash
$ start-all.sh
```

访问 ip:50070

出现hadoop，说明ok



## 踩坑一：vi hadoop-env.sh 这里要改成 JAVA_HOME 的绝对路径

## 踩坑二： 如果无法访问，但是本机  curl 可以访问，说明是防火墙没有关闭

centos7上面不可用 iptables

用的`firewalld`

```bash
# 查看防火墙状态
systemctl status firewalld
# 关闭防火墙
systemctl stop firewalld
# 禁止开机启动
systemctl disable firewalld
```





