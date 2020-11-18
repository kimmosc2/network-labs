# 查看当前交换机状态

enable >show running-config 

config > interface vlan 1

# 进入vlan 1接口(config-if)

iconfig-if > ip address 192.168.2.20 255.255.255.0

# 配置ip地址和子网掩码

iconfig-if > no shutdown

# 开启接口

config > vlan 100

# 创建vlan100

config > no vlan 20

# 删除vlan20

enable > show vlan

# 查看vlan

config > interface range  fastEthernet 0/1-9

# 进入1-8端口组(range)

range > switchport access vlan 100

# 将这8个端口指定给vlan100

conf-if > switchport mode [ access | trunk ]

# 切换交换机端口模式,要在指定接口运行(非vlan接口)

(router) interface faseEthernet 0/0.100

# 切换到路由器的100子网

(router) encapsulation dot1Q 100

# 进行dot1Q封装，其中100是交换机的对应vlan名

(router) show ip route

# 查看ip路由表


### 静态路由

(router) ip route 192.168.2.0 255.255.255.0 192.168.5.2

# 静态路由(配置目标网段和下一跳)

### rip动态路由

(router) router rip
(router) version 2
(router) network 192.168.30.0 (rip不需要子网掩码)


### OSPF 动态路由

```(router)router ospf 2```
启动ospf，进程号为2

#### 广播

```(router)network 10.10.10.0 255.255.255.0 area 0 ```
注意掩码和区域号


router rip
redistribute static //RIP中重分发静态路由 
redistribute connected //RIP中重分发直连路由 
rip中引入静态协议

rip中引入ospf
redistribute ospf 2 metric 15
可以引入的路由最多的条数

ospf中引入rip
redistribute rip subnets