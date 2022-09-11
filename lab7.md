# lab7 ONOS

## 1. ONOS安装
从https://wiki.onosproject.org/display/ONOS/Basic+ONOS+Tutorial 下载.ovs文件，双击用VM Virtual Box打开

## 2. ONOS cluster setup
### 1) 双击‘Setup ONOS Cluster’
![image](https://user-images.githubusercontent.com/58734009/189521767-97d783d9-9b4d-4130-ab29-7daa0977dc49.png)

![image](https://user-images.githubusercontent.com/58734009/189521790-90390d47-8fe5-4399-85f8-a08ab6cf9151.png)

### 2）双击'ONOS CLI'
![image](https://user-images.githubusercontent.com/58734009/189521825-8aaba395-5207-46e1-8134-4ea2ce6951fd.png)

![image](https://user-images.githubusercontent.com/58734009/189521849-973cf21c-9f5b-4f3d-a81a-7456997afa13.png)

```onos>```表示你在ONOS command line

```mininet>```表示你在mininet

### 3) 双击Spine Leaf Topology
![image](https://user-images.githubusercontent.com/58734009/189522905-87d145f1-2cb5-47cd-87d4-3033aa56de95.png)

![image](https://user-images.githubusercontent.com/58734009/189522918-23ccb820-c97a-4996-a51c-faac3d899978.png)

## 3. Reactive Forwarding
这是一个应用程序，它为到达控制器的每个数据包安装flow；必须在使用“ping”命令之前load。请按照以下步骤进行检查：

* 在mininet中输入：```mininet>h11 ping h41```

  ![image](https://user-images.githubusercontent.com/58734009/189523016-3cedf3ca-ec2d-41f5-b0b2-17d5641d8a88.png)

  ping失败了，因为我们没有加载reactive forwarding application。

* check the list of loaded application：```onos>apps -a -s```

  ![image](https://user-images.githubusercontent.com/58734009/189523056-d3e72204-ba1c-46f1-8853-caf31e802eef.png)

* 加载reactive forwarding application: ```onos>app activate org.onosproject.fwd```

  ![image](https://user-images.githubusercontent.com/58734009/189523130-5a369e58-7a4f-4786-8aa2-87875c239f38.png)

* 再次尝试ping：```mininet>h11 ping h41```

  ![image](https://user-images.githubusercontent.com/58734009/189523354-60553e0c-3208-4962-864e-e896ff2781f8.png)
 
* 关闭reactive forwarding application: ```onos> app deactivate org.onosproject.fwd```

* see a list of ONOS CLI commands: ```onos> help onos```

  ![image](https://user-images.githubusercontent.com/58734009/189523514-c6ef954c-f027-4c7d-a373-9bb9162f53ba.png)

## 4. Devices Command

### 1)  List the device currently known in the system
输入```onos> devices```

![image](https://user-images.githubusercontent.com/58734009/189523898-33342e81-3a8f-4ee6-8635-de37be2cc21c.png)

从设备列表中，我们有以下主要属性—: 设备id和一个指示设备当前是否已启动的布尔值。其他属性还包括设备的类型以及它与ONOS实例之间的角色关系。

## 5. Links Command
list the links detected by ONOS: ```onos> links```

![image](https://user-images.githubusercontent.com/58734009/189524212-82f59499-1889-469a-a8f9-8589d3d9a510.png)

显示了source device-port pair to destination device port pair的 discovered links

‘type’ 表示 whether the link is a direct connection between two devices or not.

## 6. Host command
```onos>hosts```



