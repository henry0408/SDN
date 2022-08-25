# Lab3

SDN结构：

![image](https://user-images.githubusercontent.com/58734009/186706020-dfe5d68c-beca-4cb1-88cc-164b5f619b4f.png)

## 1. 利用WireShark在Mininet抓包
step1. 启动wireshark

![image](https://user-images.githubusercontent.com/58734009/186704651-67b9e021-7abc-4669-9e4a-d5cc1810490d.png)

![image](https://user-images.githubusercontent.com/58734009/186704995-901f3cd0-12d2-4ffe-9f1a-11e8ab8174b6.png)


step2. Ctrl+C退出并建立拓扑

![image](https://user-images.githubusercontent.com/58734009/186705231-d2f4def3-108e-402d-a5cb-bddbf4467d9d.png)

此时wireshark主界面会看到所有network结构

![image](https://user-images.githubusercontent.com/58734009/186705310-07bd6200-83d2-42b2-ba61-e115d95b6465.png)

step3. 启动wireshark在any中抓包

搜索openflow_v1

![image](https://user-images.githubusercontent.com/58734009/186705714-97fa19fb-3fa9-4cd3-94f8-6f551d25b308.png)

step4. 回到mininet，pingall之后查看wireshark抓到的openflow包

![image](https://user-images.githubusercontent.com/58734009/186705857-6104864f-4bc6-4513-832e-2ec073c5aa4b.png)

![image](https://user-images.githubusercontent.com/58734009/186705909-790d63e3-53ec-4e50-9008-8e58bf873821.png)


## 2. 不同的拓扑结构

### 1). Single
$ sudo mn --topo=single,4

表示one switch, four hosts

![image](https://user-images.githubusercontent.com/58734009/186706529-d56b54a8-5242-48f8-a850-c4dca4c0463a.png)


### 2). Linear
$ sudo mn --topo=linear,3

表示one host connects to one switch

![image](https://user-images.githubusercontent.com/58734009/186706638-424615c0-c106-4524-a1e8-6ebd9c45fc05.png)

### 3). Tree
$ sudo mn - -topo=tree,2,2

two levels deep (or two levels of switches) and a fanout of two Mininet split.

![image](https://user-images.githubusercontent.com/58734009/186706772-30b9c187-461d-460b-a39a-eefec0f8bb7a.png)

## 3. 固定host的MAC和IP地址
创建mininet时默认会为每个主机分配一个mac地址，但是每次创建mininet这个mac地址都会随之改变，这样一来调试难度就大了。--mac的作用就是保证mac简单、易读，一般都尽量小。对比可以看出：

![image](https://user-images.githubusercontent.com/58734009/186707111-12cfe62f-7e34-4047-b3e9-75b8113a7fcc.png)
![image](https://user-images.githubusercontent.com/58734009/186707152-92c1114e-c8ba-4f78-8792-cf8615e1bc0f.png)

## 4. 链接向上/向下 Link Down/Up
对于容错测试fault tolerance，启动和关闭链接会很有帮助

### 1). 当我们 sudo mn –mac后
查看s1 ifconfig

![image](https://user-images.githubusercontent.com/58734009/186710022-34902dac-43c5-4615-ad8b-c5a8abfa383d.png)

查看h1 ifconfig

![image](https://user-images.githubusercontent.com/58734009/186710109-ab01f645-a950-4344-ac8e-d3645bf29515.png)

### 2). Link Down
Disable s1 and h1 link: link s1 h1 down,
之后查看s1 ifconfig：

![image](https://user-images.githubusercontent.com/58734009/186710263-1a192ae7-738f-458c-b067-e883335ba32d.png)

再查看h1 ifconfig

![image](https://user-images.githubusercontent.com/58734009/186710361-4ccabbd9-46fb-4ba6-a5e1-6327f12539ad.png)

### 3). Link Up
Bring the link s1 h1 back up. 

This generates an OpenFlow port status change notification产生端口状态更改通知

之后h1 ifconfig和s1 ifconfig 都会回到初始连接状态




