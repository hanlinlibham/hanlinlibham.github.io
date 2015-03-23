---
layout: post
category: "hadoop"
title:  "win7 eclipse debug mapreduce 问题汇总"
tags: [hadoop]
---

如何构建调试环境就不说了，网上很多，说说遇到的问题和解决。

#### 1. 插件问题

使用目前最新的hadoop-2.6.0的插件，这个在plugin的github项目release目录下就有，不需要像网上说的要自己编译。地址自行搜索。
插件可能有个updater的错误，无所谓。

#### 2. 连接失败问题

就是提示Error:Call from pc/win7 ip to vmip failed on connection exception...

这里面包含了好几个问题。

1. 发现namenode没启动。因为之前format过几次，jps查看才知道namenode没出来。于是看log，大意是txid不一致，把tmp目录删了重新format解决。

2. ip问题。开始没注意，后来才看到，错误信息显示的是192.168.56.1 to 192.168.199.230，就是这插件默认用虚拟的host-

only网卡访问的，网段不一致自然不通了。之前是设置bridge模式。墙外搜了一圈，发现一个设置双网卡的方法，虚拟机的网卡1选host-only，再打开网卡2选项，选NAT模式。设置完成之后观察ip，这次是一致的网段了，但还是不通。又看了看帖子，说是core-site等配置文件使用localhost有找namenode不通的问题，尝试改成ip，居然连接成了。但也不是网上帖子说的有user什么的目录，就一个默认input，然后自己upload了2个文件进去，地址显示hdfs://ip:9000/input/file1.txt。貌似是对了，但是在vm hdfs目录下没找到。

#### 3. 调试程序空指针问题

用官方默认的例子[link](http://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html#Example:_WordCount_v1.0)，到最后一步出现空指针异常，单步debug没发现对象是空，到aboutyun看了看帖子，先添加了HADOOP_HOME 、 Path环境变量，然后在windows的hadoop/bin下添加了winutils.exe、hadoop.dll文件。空异常消失。

#### 4. LinkError

紧接着又出来这个：java.lang.UnsatisfiedLinkError: org.apache.hadoop.util.NativeCrc32.nativeComputeChunkedSumsByteArray(II[BI[BIILjava/lang/String;JZ)V

很明显，这是调用本地方法出错了。是dll文件版本不对的问题，换成2.6的dll，这里有[link](http://pan.baidu.com/s/1dcnZS)，

错误变了，java.lang.UnsatisfiedLinkError: org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Ljava/lang/String;I)Z。这样解决：拷贝源码文件org.apache.hadoop.io.nativeio.NativeIO到项目中，然后定位到access方法，直接修改为return true; 

这次全部成功了，在DFSLocation目录下出现了output，可以查看到结果了。


