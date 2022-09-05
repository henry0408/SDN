
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
