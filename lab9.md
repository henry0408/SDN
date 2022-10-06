# P4 tutorial

Programming Protocol-independent Packet Processors编程协议无关的包处理器（P4）是一种特定于网络设备的领域语言，指定数据平面设备（交换机、nic、路由器、过滤器等）处理数据包

This lab:  first two components of the P4 language: 
* Headers
* Parsers

## 1. 官方教程
https://github.com/p4lang/tutorials

![image](https://user-images.githubusercontent.com/58734009/194260467-ce81db56-04a3-4bc6-96b4-5cb2630eace3.png)

这些练习在一些关键代码上是空缺的，可以根据提示进行填充。其中每个练习的答案都在solution文件夹里，可以在自己填充好后进行对照。


# 1.安装
1) step 1. Download the virtual machine by the link:\
https://drive.google.com/file/d/1ZkE5ynJrASMC54h0aqDwaCOA0I4i48AC/view?usp=sharing

2) step 2. Select and import target virtual machine\
![image](https://user-images.githubusercontent.com/58734009/194266967-ede47623-55f7-4dce-8dd7-ae2a8a97bd98.png)


3) 步骤3：此虚拟机有两个用户帐户。正常的是用户id“p4”，密码为“p4”。\
另一个具有一个主目录，其中包含用于构建已安装的二进制文件的P4开发工具的源代码source code，其用户id为“vagrant”，密码为“vagrant”。\
除非您想查看该源代码，否则建议使用普通的源代码。\

# 2. Warming Up testing for P4
Open the ‘basic’ folder in the shell; it could be found at tutorials/exercises/basic.

Input the ‘make run’ command to run the network with basic topo.

<注>红色的方框突出显示了已用于设置此网络的文件.

