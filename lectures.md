# Lecture 1
## 1. What is SDN?
A new architecture that makes networks more programmable than in the past.

Key principles: Centralised control, Open interfaces, Flow-based routing.

Important SDN technology: OpenFlow is the most widely adopted protocol. OpenFlow是最广泛采用的协议
![image](https://user-images.githubusercontent.com/58734009/184665275-f4423e7c-87bd-4b01-a818-c9391d7fdfe5.png)

## 2. Basic Concept of SDN
  1. Separate Control plane and Data plane entities
  2. Execute or run Control plane software on general purpose hardware.
  3. Have programmable data planes.
  4. An architecture to control not just a networking device but an entire network.

# Lecture 2 
## 1. What is Openflow?
OpenFlow is communication interface between the control and data plane of an SDN architecture.

* Allow separation of control and data planes. -允许控制平面和数据平面的分离
* Centralization of control. –控制
* Flow based control.–基于流的控制
* Takes advantage routing tables in Ethernet switches and routers.–利用了以太网交换机和路由器中的路由表

Allows direct access to and manipulation of the forwarding plane of network devices such as switches and routers, both physical and virtual.
允许直接访问和操作网络设备的转发平面，如交换机和路由器，包括物理的和虚拟的。

Think of as a protocol used in switching devices and controllers interface. 可以看作是一个用于交换设备和控制器接口的协议。
