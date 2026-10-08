---
onenote-id: 0-8b2b26a2cbd74fe3b981ec5b4e30cce4!1-DBD29CD2C5C95FE5!sea300882f3834ff5a2589599c8b1c62f
---
# ICMP

ICMP（Internet Control Message Protocol，网络控制消息协议）  
当路由器正在处理一个数据包的过程中有意外事情发生时，可通过ICMP向发送方报告。  
场景举例：  
目标主机不可达：客户端访问服务器超时，却不知到底是目的主机挂掉还是路由锻链？  
TTL超时：数据包在网络环路中陷入“无限转发”？  
路径探测：如何知道数据包经过了哪些中间路由？
 
# ping

发送ECHO（回显）到目的地址，判断目的地址的设备是否还“活着”，如果目的地址回复ECHO REPLY（回显应答），说明还“活着”。
 
# traceroute

给目标发送一系列的数据包，分别将TTL设置为1，2，3，。。。，这些数据包的TTL数值沿着路径在后续的路由器上到达0，这些路由器各自送回一个超时消息给主机，利用这种技巧，可以确定沿途路由器的IP地址。
 
# 源IP地址
 
# DHCP协议

DHCP（Dynamic Host Configuration Protocol）动态主机配置协议。
 
# ARP协议

ARP（Address Resolution Protocol）地址解析协议  
背景：以太网中，网络层用IP地址找到目标主机，但链路层需要MAC地址才能发送帧。  
作用：在同一局域网内，通过ARP将基于目的IP地址找到对应的MAC地址。
 
# 网关

网关（Gateway）：是指连接不用网络、负责转发数据包的网络设备或路由器接口，它是网络边界的出入口。
 
# NAT

NAT（Network Address Transtation）网络地址转换。  
公网IPv4地址有限，而内部网络设备却日益增多，导致IPv4地址枯竭。  
NAT在数据包经过路由器时，修改其源（或目的）IP地址和/或端口号，并维护一个映射表。
 
# 发射数据

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ICMP_DHCP_ARP_NAT_IPv6%EF%BC%89%20image%20b1bf05e8fbf33af3.png)  
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ICMP_DHCP_ARP_NAT_IPv6%EF%BC%89%20image%20ead47be382e17d13.png)  

# IPv6地址

IPv6地址的长度为16字节（128bit），通常以8段十六进制表示，每段16bit。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ICMP_DHCP_ARP_NAT_IPv6%EF%BC%89%20image%2001ff17f3d0e187db.png)  

# IPv4和IPv6

去掉了首部长度字节，IPv6首部长度固定。  
去掉了上层协议字段，IPv6中的下一个首部字段指明了IP头后面跟的是什么。  
去掉了所有与分段有关的字段，IPv6采用了不同的分段方法。  
IPv6不允许在中间路由器上进行分片和重新组装，这种操作只能在源和目的上执行。  
去掉了校验和字段，因为计算校验和极大降低性能，通过数据链路层和传输层进行校验。