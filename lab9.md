# P4 tutorial

## 0. 教程部分
1. 一个非常好的SDN，OPenFlow和P4的整体简介：
https://developer.aliyun.com/article/651037

2. P4 学习笔记（一）- 导论：https://zhuanlan.zhihu.com/p/346371311

3. P4 学习笔记（二）- 基础语法和 Parser：https://zhuanlan.zhihu.com/p/346936899

4. P4 学习笔记（三）- 控制逻辑与完整的工作流：https://zhuanlan.zhihu.com/p/347282455


<注>如何改变VM分辨率：

![image](https://user-images.githubusercontent.com/58734009/194343297-6ab246f9-1e06-45c9-9e0e-c97a03ea44b7.png)

如何改变P4 VM分辨率：

![0f8adfd8c6834db6926d81ddb0d5111](https://user-images.githubusercontent.com/58734009/194344472-c9772e9c-053e-431f-a4f5-8abadd9674b3.jpg)

如何保存emacs IDE的文件：ctrl+X之后ctrl+S

操作总结：https://blog.csdn.net/jasenwan88/article/details/7690364

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
除非您想查看该源代码，否则建议使用普通的账户登录

![image](https://user-images.githubusercontent.com/58734009/194339115-17d9aeb9-56ab-4977-a623-fb28a4efc185.png)


# 2. Warming Up testing for P4

### 1) Open the ‘basic’ folder in the shell; it could be found at tutorials/exercises/basic.

Input the ‘make run’ command to run the network with basic topo.

![image](https://user-images.githubusercontent.com/58734009/194344889-6cf1c065-47e4-4205-8a48-73b19639ada1.png)

<注>b4c-bm2-ss --p4v 16 --p4runtime-files build/basic.p4.p4info.txt -o build/basic.json basic.p4: 显示了已用于设置此网络的文件.

![image](https://user-images.githubusercontent.com/58734009/194347695-880173ea-deec-4b1a-a4b0-6b02a45dfb63.png)

### 2) 输入dump或net查看topo
![image](https://user-images.githubusercontent.com/58734009/194347979-a4cf60d3-52a3-4257-b6af-897961f8d1f1.png)

![image](https://user-images.githubusercontent.com/58734009/194348033-57d96a57-add8-48e6-8d0f-ddd7a1a3c9f9.png)

<注>此时尝试ping会失败，because each switch is programmed according to ‘basic.p4'，然而‘basic.p4’ is incomplete, dropping all packets on arrival.

### 3）leave 'xterm': mininet> exit

### 4) stop mininet: 
* $ make stop
* $ make clean


# 3. View and complete basic.p4:

![image](https://user-images.githubusercontent.com/58734009/194349778-467d0b70-98a4-4291-b6c2-919f5dd81d03.png)

# 4. P4 Architecture
Basic structure:\
![image](https://user-images.githubusercontent.com/58734009/194351209-fb8bc925-6182-40a6-80ac-21c7a7c8c2c6.png)

这是一个基本的P4体系结构，P4只支持基本功能。P4的体系结构可以有所不同，更复杂，并在现实世界中支持更多的功能。

The role and function of each part:
* ‘Parser’: produces a parsed representation of all relevant headers.生成所有相关头的解析表示
* ‘Ingress’: defines some match-action pipelines; matches, and then executes the action.定义一些匹配操作管道；匹配，然后执行该操作。
* ‘Switching logic’: implements the logic designed; the buffer could be set here.实现了所设计的逻辑；缓冲区可以在这里设置。
* ‘Egress’: defines some match-action pipelines; matches, and then executes the action "出口"：定义了一些匹配操作管道；匹配，然后执行该操作
* ‘Deparser’: Reverse Operation of ‘Parser.’ Reassembling packets.重新组装数据包


所以大佬们开始琢磨，能不能从更底层入手，搞一个 Protocol Independent Switch Architecture (PISA) 出来，就把计算机网络里 packet 的转发最基础的过程高度抽象化，变成上面这个图的样子，从左到右，分别是：

* Parser：先看看包里面都有啥，每一个 bit 都是什么；
* Ingress：一堆 Match-Action 的流水线，看看哪些 bits 组成的 fields 有没有我们想要的，比如目标 IP 是不是 8.8.8.8，是的话就改写一下 header 让包能被转发到它该去的地方；
* Switching Logic：还要有个地方实现我们想要的逻辑，或者为了高性能，放一个 buffer，存放刚被上一个环节处理完，准备给下一个环节处理的包[3]；
* Egress：又来一堆 Match-Action 的流水线，比如改写源 MAC 地址，同时提供更多对网络包的操作空间；
* Deparser：最后把我们改写好的 headers 重新写回网络包，然后送它出去。

# 5. P4 five different language components

P4 achieves the architecture by using ***five different language components***:\ 
Headers, Parsers, Controls, Table, Actions.\
We will study to use these components and finally complete the ‘basic.p4’ file.


接下来就说一下 P4 的语法。P4 是一种静态语言，有点类似 C。一个代码文件基本上都长成下面这个样子：\
![image](https://user-images.githubusercontent.com/58734009/195591814-0689c3e7-6cf2-4b6a-b5be-f2524085138c.png)

* Libraries：一开始要 include 一些库文件，省的造轮子；
* Declarations：定义一下基本的数据结构，也支持 typedef；
* Parse packet headers：这个 Parser 的地方会放一些解析 headers 的代码；
* Control flow：这个地方基本是最重要的逻辑部分了，这里会通过我们定义的 Match-Action functions 按照修改网络包里的内容（这里只写了 Ingress 这一步，其实还会有 Egress，等到下面 main 的时候会提到）；
* Assemble：然后就是在 Deparser 的地方会把我们前面改好的部分重新组装成为一个新的 packet，转发出去；
* main()：这就是我们的 main 函数了，这里其实就是把我们刚刚写的所有的部分，按照正确的顺序排列好，一个一个的调用，所有的步骤都已经罗列出来了：
* 大体的结构可以分成三段式：Parser -> Match-Action Pipeline -> Deparser

## 1) P4 Programming Headers

Header definitions describe packet formats and provide names for the fields within the packet. 描述了包的格式，并为包内的字段提供了名称
The language allows customized header names and fields of arbitrary length, although many header definitions use widely known protocol names and fields widths.\
该语言允许自定义任意长度的头名称和字段，尽管许多头定义使用众为人知的协议名称和字段宽度。

Our lab only focuses on ipv4 addresses, so we don’t need to identify ipv6 formats (but you can try to add it if you can). Figure below shows the ‘Headers’ of this lab.

![image](https://user-images.githubusercontent.com/58734009/194354096-e2bd82e3-3e68-434b-b222-6ec286810c5d.png)

Some keywords (with explanations) used in ‘Headers.’

|Types |Examples |Notes |
| ---- | ---- | ---- |
| bit | bit<N> | unsigned integers of width N |
| typedef | typedef bit<48> macAddr_t; | To support giving convenient names to commonly-used types, P4 provides type definitions. 为了支持为常用的类型提供方便的名称，P4提供了类型定义。With the declaration of the example, the types bit<48> and macAddr_t are synonyms同义词 that are treated as equivalent by the type checker. |
| headers | header ethernet_t { ***} | P4 provides a built-in type for representing headers, using syntax that resembles the C struct. |
| struct | Struct headers {***} | For instantiation实例化 |


## 2) P4 programming Parsers
Parser maps the bits in the actual packet into typed representations. 解析器将实际数据包中的位映射到类型化的表示形式中
  
The role of the parser is to identify the headers present in each incoming packet correctly. 解析器的作用是正确识别每个传入数据包中存在的头

The parser produces a parsed representation of all relevant headers for each packet, which is then passed to the first control block. The sequence of control blocks in turn further processes the packet.  解析器为每个数据包生成所有相关头的解析表示，然后将其传递给第一个控制块。控制块的顺序依次进一步处理数据包。
  
Some key commands in the "Parsers":

|transition |Transit the packet to another state |
  | ---- | ---- |
|extract |Extract a piece of target headers |
|accept |Accept the package and stop the transition |
  
We need to set up the state of ‘parse_ethernet’ and ‘parse_ipv4’ in this lab:\
We firstly transit the package to state ‘parse_ethernet,’ \
then extract the ethernet piece, \
transit the package to the state ‘parse_ipv4’, \
and finally accept the package.

![image](https://user-images.githubusercontent.com/58734009/195543319-6e885ed9-0ca7-414d-bd6a-466542ccf542.png)

![image](https://user-images.githubusercontent.com/58734009/195543361-ff10b8f4-3e72-470e-a1ed-f3b2cb31dac0.png)
