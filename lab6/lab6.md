**注:本章内容只是做了简单整理(也可能不会再整理了),看不懂还是私聊联系我吧，如果你有精力,欢迎和我一同维护本repo (BuTn:2020/11/18)**
## 计算机网络实验6
### 查看IP路由表

```(router) show ip route ```   

### 设置静态路由

```(router) ip route [net-id] [net-mask] [next jump ip]```  

[net-id] 目标网络地址  
[net-mask] 目标子网掩码  
[next jump ip] 下一跳网络地址  

### RIP动态路由相关

```(router) router rip```  
用途:开启IP路由协议(RIP)  

```(router) version 2```  
用途:RIP2版本  

```(router) network [net-id] (注:RIP协议不需要子网掩码)```  
用途:宣告网段    
[net-id] 网络地址，注意别带主机位,如果不了解net-id和host-id请翻书:-)  

### OSPF 动态路由相关

```(router)router ospf [process-id]```  
用途:启动OSPF    
[process-id]进程号(这里如果第一次输入错误的process-id,会导致router-id错误,使思科模拟器里的router-id项一直打叉,如果想拿满分,下面给出了解决办法:  
#### 解决OSPF router-id项一直打叉
比如题中给的OSPF process是1,而你第一次打成了2,就会导致这种情况发生,即使你后来在1上做了正确的配置,依旧会出现这样的情况,解决办法就是:
1.在enable模式下输入```show ip ospf 2```,查看ospf 2的router-id，并记录下来  
2.在config模式下输入```no router ospf 2```关掉ospf2进程  
3.进入ospf 1进程```router ospf 1```,配置router-id:```router-id + 刚刚记录的ospf2的router-id```完成后会提示你reload或者输入```clear ip ospf 2```来使配置生效    
~~4.还不会？那你私我吧~~  

```(router)network [net-id] [net-mask] area [area-id] ```  
用途:宣告网段,注意掩码和区域号  
[net-id] 网络号   
[net-mask] 子网掩码  
[area-id] 区域号  

### 重分发
#### RIP相关
1.```router rip```    
2.```redistribute static```   
用途: RIP中重分发静态路由     

```redistribute connected```   
用途:RIP中重分发直连路由   

#### RIP和OSPF
```redistribute ospf 2 metric 15```  
用途:可以引入的路由最多的条数  


```redistribute rip subnets```  
用途:将RIP发布到OSPF  

#### OSPF和静态
```redistribute static subnets```  
更多可以看[这篇文章](https://blog.51cto.com/zhaoyuqiang/1179811)