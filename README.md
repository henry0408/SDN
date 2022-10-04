# Software-Defined-Networks
ELEC5517 Software Defined Network

笔记整理：

# Lecture1
## 1. What is SDN

A new architecture that makes network more programmable than in the past

## 2. SDN key principles

Centralized control, Open interfaces, Flow-based routing

## 3. What is OpenFlow

The most widely adopted protocol. 不是SDN，但is an important SDN technology

## 4. OS for SDN network
![image](https://user-images.githubusercontent.com/58734009/193587147-534aad65-cecc-4486-88e2-fe414e9d135f.png)

![image](https://user-images.githubusercontent.com/58734009/193587246-1b9cfb1f-0114-41b7-948d-142a652c4f4f.png)

![image](https://user-images.githubusercontent.com/58734009/193860490-dd29f1c5-fb94-4db4-be94-02d129f52104.png)

5. SDN basic concept
- Separate Control Plane and Data Plane entities
Network intelligence and state are logically centralized. 
The underlying network infrastructure is abstracted from the applications. 
底层的网络基础设施是从应用程序中抽象出来的。
-Execute or run Control plane software on general purpose hardware
Decouple from specific networking hardware. 
Use commodity servers and switches.
- Have programmable data planes
Maintain, control and program data plane state from a central entity
- An architecture to control not just a networking device but an entire network
