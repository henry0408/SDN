
# Lab4

## 1. 新建拓扑并查看所有nodes
![image](https://user-images.githubusercontent.com/58734009/189399528-041742be-3a18-4e42-93c5-242e56c0f4ed.png)

```sudo mn --topo=single,4```

![image](https://user-images.githubusercontent.com/58734009/189399775-4d40e0b6-bef9-42a8-9900-e775b31507f3.png)

Show all the nodes: ```dump```

![image](https://user-images.githubusercontent.com/58734009/189400080-e8b035cd-af20-4a32-a55d-5c8de5e166e9.png)


## 2. 将目录直接映射到HTTP请求 Direct mapping of a directory to HTTP requests
### 1）先打开wireshark

### 2) 接着输入两条命令:通过python 开通一个简易的 web server，通过 h1 向 h4送出請求

```h4 python –m SimpleHTTPServer 80 &```
```mininet h1 wget 10.0.0.4```

```h4 kill %python```


或者：通过 h2 向 h1 送出請求，之後關閉 web serve
  mininet> h1 python -m SimpleHTTPServer 80 &
  mininet> h2 wget -O - h1
  ...
  mininet> h1 kill %python
