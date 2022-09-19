# lab8

Basic ONOS tutorial: https://wiki.onosproject.org/display/ONOS/Basic+ONOS+Tutorial

REST APIs: https://wiki.onosproject.org/display/ONOS/Appendix+B%3A+REST+API#AppendixB:RESTAPI-Host

## 1.启动ONOS CLI之后输入
![image](https://user-images.githubusercontent.com/58734009/190889981-507b60f7-117a-4534-8ea7-b523566cda02.png)

## 2.打开ONOS GUI，User为onos，密码为rocks
![image](https://user-images.githubusercontent.com/58734009/190890022-62e55c6d-e500-43f1-a70d-46886a6df7c3.png)

![image](https://user-images.githubusercontent.com/58734009/190890033-d6defad3-1bbf-453a-8b87-293683c3672e.png)

启动Spine Leaf Topology之后会显示：

![image](https://user-images.githubusercontent.com/58734009/190890326-0b12aa66-4e97-44d4-bbe0-29e345f2b406.png)

## 3. GUI cheatsheet
点击键盘“/”键

![image](https://user-images.githubusercontent.com/58734009/190890393-2dc0692d-849a-43f8-b5ea-bf2d62b83e83.png)

## 4. 让主机在网络中互相对话

运行pingall

![image](https://user-images.githubusercontent.com/58734009/190890459-cc042007-6291-4bc4-8c75-01282e339667.png)

会发现界面里没有变化，此时在browser window中type "h": （不pingall点击h也可以看到所有hosts）

![image](https://user-images.githubusercontent.com/58734009/190890490-27baa128-49b3-42f5-a65f-47ce7463f341.png)

## 5. switch details
点击任何一个switch，右侧会出现它的information

![image](https://user-images.githubusercontent.com/58734009/190890551-05409caf-dae0-4ae7-b8cd-2c022b87836a.png)

注意，显示有8个port，但只能看到7个的原因是OpenFlow switches have virtual ports that are hard to show on a GUI.

## 6. Instance
GUI可以显示哪个ONOS实例是active的，点击键盘"i"键，可以出现 (再按一次隐藏)：

![image](https://user-images.githubusercontent.com/58734009/190890731-00e7f114-c850-4f78-b9a0-662648f61041.png)

请注意，开关的图形改变了颜色，这表明哪个开关是由哪个实例控制的。这对于一眼看出哪些开关是由哪些ONOs实例控制的是很有用的。
（上面的图说明6个switch都由172.17.0.3这个instance控制）

## 7. Install Intent
要使用GUI安装即时主机， 首先选择两个host（鼠标点中一个接着按住shift选中第二个）。Let’s pick 10.0.0.20 and 10.0.0.9. 接着 a pane will appear on the right hand 
side of the screen as shown here.

![image](https://user-images.githubusercontent.com/58734009/190891129-8ddc904a-70b1-4d35-a0da-a0f0258d75b9.png)

* Click on ‘Create Host-to-Host Flow’,这会提供一个host to host intent，并且path会照亮

![image](https://user-images.githubusercontent.com/58734009/190891163-b7fb7f15-1d49-4d6d-9d15-5304d8900a12.png)

![image](https://user-images.githubusercontent.com/58734009/190891185-e1fd29a1-f86b-484e-8044-075c37460efa.png)

* You can check that the intent was installed via the ONOS CLI.
![image](https://user-images.githubusercontent.com/58734009/190891258-338041e7-7b25-4515-bebe-6e9fe2e0522d.png)

## 8. Show all traffic 
* mininet>h24 ping h42
![image](https://user-images.githubusercontent.com/58734009/190891651-9cf90e1d-84d3-4cd4-bbc1-e1537af590e5.png)

* 在browser中，点击键盘"a"可以显示any traffic that is running on the network

![image](https://user-images.githubusercontent.com/58734009/190891514-da1a5e4c-e935-4d03-ae1d-9376e969ff99.png)

## 9. 改变ONOS nodes assign的switch数量

上面的图可以看到，所有的switch都被分配给第二个ONOS node，而其他的两个ONOS nodes没有master的switch.

ONOS GUI（以及 CLI）允许用户强制重新平衡主控权(force mastership re-balancing )，其中网络设备将在 ONOS 集群中的所有节点之间大致平均分配。 要从 GUI 执行此操作，请按 E 键。

balance之后变成：

![image](https://user-images.githubusercontent.com/58734009/191028987-defa49ff-e817-40c7-b8c3-1cb9e5c6091b.png)


# 10. Display the node labels
Press the L key to cycle between friendly lables, device ids and no labels

* friendly labels:
  ![image](https://user-images.githubusercontent.com/58734009/191029322-804935dc-412a-4215-8ea1-0738f04428ab.png)

* devices ids
  ![image](https://user-images.githubusercontent.com/58734009/191029369-e23131f1-98de-492b-9478-8546a40371f0.png)

# 11. ONOS REST APIs
* 打开新的web browser, 输入the following URL: ```http://<ONOS IP>:8181/onos/v1/docs```

  ![f2effb5a029c289cf9d6202105b7b99](https://user-images.githubusercontent.com/58734009/191032121-08250748-99e3-468e-b6fa-b2a8174320d1.png)

  用户名密码分别为：onos, rocks

* ONOS uses Swagger to generate the REST API documentation:

  ![image](https://user-images.githubusercontent.com/58734009/191032242-c6c4308a-a899-4798-9ac1-ca268754afc8.png)

# 12. ONOS Core API summary

## 1. Device
![image](https://user-images.githubusercontent.com/58734009/191032640-f0a9a16d-8f32-4279-b516-219dbbb8ea7c.png)

GET /devices 列出所有基础设施设备Lists all infrastructure devices.\
GET /devices/{deviceId} 列出特定基础设施设备的详细信息Lists details of a specific infrastructure device\
GET /devices/{deviceId}/ports 列出特定基础设施设备的端口Lists ports of a specific infrastructure device.\
POST /devices 在清单中创建一个新的基础设施设备（未来）Creates a new infrastructure device into inventory (future).\
PUT /devices/{deviceId} 更新设备 - 属性、可用性、主控权Updates a device - attributes, availability, mastership.\
DELETE /devices/{deviceId} 从清单中删除基础设施设备Deletes an infrastructure device from inventory.

选中GET/Device并点击Try it all button：

![image](https://user-images.githubusercontent.com/58734009/191033998-0d26cf30-613c-43d9-baa3-72c12b5a859d.png)

ONOS API返回的响应将返回具有关联属性的所有设备的列表：

![image](https://user-images.githubusercontent.com/58734009/191035827-35061b8a-7511-4af8-8c00-a027e0e080e6.png)


## 2. Hosts
![image](https://user-images.githubusercontent.com/58734009/191035944-04aa65bd-297f-414a-823c-c092fef38a61.png)

GET /hosts 列出所有终端站主机Lists all end-stations hosts\
GET /hosts/{hostId} 列出由主机 ID 指定的特定终端主机的详细信息Lists details of a specific end-station host specified by the host ID\
GET /hosts/{mac}/{vlan} 列出由主机 MAC 地址和 VLAN Id 指定的特定终端站主机的详细信息Lists details of a specific end-station host specified by the host MAC address and VLan Id.\
POST /hosts 在清单中创建一个新的终端站主机（未来）Creates a new end-station host into inventory (future)\
PUT /hosts/{hostId} 更新终端主机 - 属性，例如IP，位置Updates an end-station host - attributes, e.g. IP, location.\
DELETE /hosts/{hostId} 从清单中删除终端站主机Deletes an end-station host from inventory.

选中POST /hosts, 输入以下内容（可以直接点击右侧黄色框的example，快速填入），并点击try it out:

![image](https://user-images.githubusercontent.com/58734009/191037231-e0b59770-4c14-4c00-9853-da1890986211.png)


![image](https://user-images.githubusercontent.com/58734009/191037157-68ea6186-9ae9-40fc-9bb8-7567b833c75c.png)

回到ONOS GUI，我们可以看到一个新的device添加到了network：

![image](https://user-images.githubusercontent.com/58734009/191037594-55fd0044-37ab-424c-a6e9-cae6aaf836b8.png)




