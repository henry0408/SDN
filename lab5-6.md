
# Lab 5 and Lab 6

## 1. Miniedit: 一个Mininet的GUI
启动方法：
```
sudo python ./mininet/examples/miniedit.py
```

![image](https://user-images.githubusercontent.com/58734009/188486859-6e344461-c3b3-45e7-932d-c2bd945a4d30.png)

在File --> Open可以打开之前保存的.mn文件（e.g. lab5.mn）

### Miniedit Tools介绍
1. Host: 
![image](https://user-images.githubusercontent.com/58734009/188486999-47d9a579-3098-419f-a938-835db7775d9f.png)

2. Switch (OpenFlow-enabled):
![image](https://user-images.githubusercontent.com/58734009/188487461-5cfad6c9-5ff7-485c-9bc6-d77af258983c.png)

3. Legacy Switch tool (不需要controller，尽量不要用)
![image](https://user-images.githubusercontent.com/58734009/188487686-5abc31e5-6360-4c13-82fb-0201efac11b5.png)

4. Legacy Router （基本的路由器，不需要controller即可独立运行，just a host with IP forwarding enabled）
![image](https://user-images.githubusercontent.com/58734009/188488049-623afec4-1996-4d33-a9ec-83c324daaad4.png)

5. Controller
![image](https://user-images.githubusercontent.com/58734009/188488142-e5df0caa-059a-4ef3-9556-f8d4e8372b00.png)

以上工具可以右键来配置属性

## 2. Network Scenario 1:
![image](https://user-images.githubusercontent.com/58734009/188488365-8933244c-d918-4453-9a19-116b83c7ee9d.png)

注意如果使用多个controller，确保端口号Port不同

开启CLI (Command Line Interferece) Opention:

![image](https://user-images.githubusercontent.com/58734009/188488845-8236f25d-3d23-4e44-a332-fc4aa283d339.png)

导出既可以save as .mn file，也可以export as .py file

点击Run即可运行，并且在Terminal可以看到CLI：

![image](https://user-images.githubusercontent.com/58734009/188489135-2bce5dd1-1718-4cc9-993f-f36ab464a8f1.png)

## 3. Open vSwitch Configuration
![image](https://user-images.githubusercontent.com/58734009/188490170-44904a52-54e4-49ce-89c7-d4d57ddc80aa.png)

点击Run --> Show OVS Summary以显示交换机配置的列表。这是一种验证Switches是否正在侦听正确的controller的方法。在运行“显示OVS摘要”之前，请检查网络模拟中的交换机配置，并验证所有配置都正确设置。

![image](https://user-images.githubusercontent.com/58734009/188605720-2c6c5432-52f4-47db-b21a-380eb0098212.png)

![image](https://user-images.githubusercontent.com/58734009/188605829-8cc6b59b-4511-466e-abbd-fcadc2e0dfda.png)


## 4. Checking Switch Flow Tables
为了查看一些交换机的Flow Table，需要打开连接host computer的terminal window
方法：Run --> Root Terminal

  * 先输入：su mininet进入到mininet
  * 接着输入：sudo ovs-ofctl dump-flows s1 查看s1的flow table

![image](https://user-images.githubusercontent.com/58734009/188608951-074e36fc-c982-4333-83aa-d2ade08f62ab.png)

## 5. Generating and Monitoring Network Traffic生成和监控网络流量

### 用Wireshark来生成和监控网络流量

* 右键点击h1和h2的图标打开xterm window

  ![image](https://user-images.githubusercontent.com/58734009/188609788-f5a68fb5-f61b-44b3-8a5f-4a7e1e6dfa82.png)

* 在h1的terminal中输入```wireshark &```来打开wireshark，在h2的terminal中输入tcpdump来打开packet trace
  
  ![image](https://user-images.githubusercontent.com/58734009/188610712-f2ce32be-b4f5-40ef-a5e2-0b13da741df5.png)

* 在主terminal中输入```h1 ping h2```，即可在Wireshark中看到成功发送的ICMP数据包并收到回复

  ![image](https://user-images.githubusercontent.com/58734009/188614672-24bef8f6-f145-4a12-9065-615a463e7fe7.png)

## 6. Simulating Broken Link模拟断开链路
鼠标右键选择蓝色的link，点击Link Down，会发现蓝色实现变成了虚线。请确保此时为run mode

一旦链路关闭，h2不会接受到更多流量(no more traffic)，并且ping命令会提示从h1发送的数据包没有被响应。为了恢复，右键点击Up Link

都连接的情况下在terminal中像之前一样输入```sudo ovs-ofctl dump-flows s1```会看到 flows installed for ICMP packets and ARP packets

![image](https://user-images.githubusercontent.com/58734009/188622985-00130994-ae1e-45be-b4b0-88c9bb3583f7.png)

## 7. Stop Simulation
* 退出Host h1和h2的Wireshark和tcpdump
* 用Ctrl+C退出主terminal的ping command
* 用exit退出Mininet CLI
* 最后点击MiniEdit的Stop

## 8. Link Options
在MiniEdit没有运行时，右键点击蓝色link，选择properties，即可add delay, loss, speedup etc. of the link

![image](https://user-images.githubusercontent.com/58734009/188624715-eb08b309-b4ed-40d9-ba83-1b83fcb51962.png)

![image](https://user-images.githubusercontent.com/58734009/188624595-d13090ad-0f48-417a-86b7-bdd7e0b83a4d.png)

##  9. Running a saved Mininet Custom Topology Script 运行一个保存的Mininet自定义拓扑脚本
* 首先将保存的.py文件变为可执行文件：```sudo chmod 777 lab5.py```
* 接着输入```sudo ./lab5.py```



