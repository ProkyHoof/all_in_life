---
onenote-id: 0-bb293ffdbc9749a98a35db4669e4c2ab!1-DBD29CD2C5C95FE5!sea300882f3834ff5a2589599c8b1c62f
---
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%204a7754e092b073c0.png)  
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20fc97b123631d0d6c.png)  

# IP数据报格式

IP数据报包含首部和数据部分

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%206bc4cfaaef0359f1.png)  
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%2008ac5b9a0c09a814.png)

版本：规定了数据报的IP协议版本，通过版本号，路由器能确定如何解释IP数据报的剩余部分。
 
首部长度：表示IP数据报首部长度（以4字节为单位）。该字段取值范围5-15（0101 - 1111），大多数IP数据  
报不包含选项，所以一般IP数据报首部是20字节。
 
服务类型：前6位用来表示数据报的服务类型，后2位用来携带拥塞通知信息，配合TCP实现端到端拥塞管理。
 
数据报长度：整个IP数据报（头部 + 数据）的长度，单位字节。IP数据报理论最大长度是65535字节，但很少有超过1500字节的。
 
标识：唯一标识一个原始数据报，用于分片与重组。当一个大的数据报被分片后，各分片都带相同的标识值，以便目的端正确重组。
 
标志  
第一位：保留位，必须为0。  
第二位：DF（Don't Fragment，不分片），置1为不分片。  
第三位：MF（More Fragments，后续还有分片），除最后一片外的所有分片，MF = 1；最后一片MF = 0。
 
片偏移量：当前分片在原始数据报中的位置，单位为8字节。重组时，目的端根据偏移值吧各片按正确顺序拼回原始数据。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%201b32f0a04bfe85b4.png)

除了数据报中最后一个分片外，其他所有分片必须是8字节的倍数。
 
生存时间：用于限制数据报生存时间的计数器，最初是以秒计数，最大生存时间为255s。现在是跳计数器，每经过一个路由器，计数器减1，当减到0时，数据报被丢弃。这样做的意义在于防止循环转发导致数据报在网络中“无线存活”。
 
上层协议：该字段当一个IP数据报到达最终目的地时才会有用。该字段的值指示了IP数据报应该交给哪个特定的传输层协议。例如，1 = ICMP，6 = TCP，17 = UDP等。
 
首部校验和：用来校验数据报的首部，不包括数据部分，接收端验证头部字传输过程中是否出错，若不匹配则丢弃数据报。
 
选项：提供额外功能，如安全级别、安全路由记录、时间戳等，一般不用。
 
# IP地址

IP地址（Internet Protocol Address）是网络中每台设备的唯一标识符，类似于一个“门牌号”，它由32位二进制数组成，网络中每一台主机和路由器都有一个IP地址，一个IP地址并不是指向一台主机，而是一个网络接口。  
绝大多数主机都在一个网络中，所以只有一个IP地址，而路由器有多个接口，所以有多个IP地址。
 
# IP地址-点分十进制表示法
 
# IP地址分类

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20241bbe4e4ec55b97.png)  

# IP地址分类-A类

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20a54b8ed091c3b6d7.png)  

# IP地址分类-B类

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%200bf3b4ba6ad06778.png)  

# IP地址分类-C类

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20b2d64b371c3068f3.png)  
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%201230edd411f9be44.png)  

# 特殊IP地址

1. 在本网络中表示网络地址、本机地址，在路由表中表示默认路由。
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%200f6c37e8c54d523f.png)3. 通常在LAN中进行广播，使用该地址表示网络中的所有主机（路由器不转发）。
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%200617ba8c426ca977.png)5. 在发送方不知道主机号的情况下，用于本地无按键的回环测试，称为回环地址。
![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20a0c648891d497ef6.png)
 ![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%203c5bb36dad15ad34.png)  

# 私有地址

有一部分地址保留用于内部网络，称为私有地址。这部分地址不会被公共互联网分配，不会与公共地址重复。这些地址无法在公共互联网使用，因为路由器不对目标地址是私有地址的分组进行转发。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%2034aafd4345ea7015.png)  

# 子网划分

子网划分：将一个地址块划分成几部分，将一个大的网络分割成多个小的子网，供多个内部网络使用，但对于外部世界仍然像单个网络一样。这样可以更好地管理和利用地址空间，避免浪费。  
通过分割子网，可以限制广播域的范围，减少网络中的广播流量，提升效率。  
通过将不同的部门或区域划分到不同的子网，可以更好地控制流量，减少潜在的安全风险。
 
# 子网掩码

网络中的主机被分配IP地址的同时，还会指定子网掩码。  
通过将IP地址和子网掩码两者进行按位与操作，可以得到IP地址所属的网络地址（网络号）。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20cd98e893623ab7fe.png)  

# CIDR

无分类域间路由选择（Classless Inter-Domain Routing，CIDR）  
CIDR是一种新的IP地址划分方法，是一种更灵活的IP地址分配与路由方法，它打破了传统的A、B、C类IP地址的限制。CIDR使用一个斜杆后跟网络前缀长度（即网络部分的位数）来表示IP地址和子网的关系。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%BD%91%E7%BB%9C%E5%B1%82%EF%BC%88ip%E6%95%B0%E6%8D%AE%E6%8A%A5_ip%E5%9C%B0%E5%9D%80_CIDR%EF%BC%89%20image%20c33c6a98c94b8fd4.png)