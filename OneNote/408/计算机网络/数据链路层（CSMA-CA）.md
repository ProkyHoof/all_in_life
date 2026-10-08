---
onenote-id: 0-83242a64a76e4de6ae6e2fb9e6edd4be!1-DBD29CD2C5C95FE5!sea300882f3834ff5a2589599c8b1c62f
---
# 无线局域网（WLAN）

WIFI：IEEE 802.11无线局域网  
BSS：基本服务集（Basic Service Set，BSS）  
一个BSS包含一个或多个无线站点和一个中央基站（Access Point，AP）

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82%EF%BC%88CSMA-CA%EF%BC%89%20image%20ae62e39ef6c2550f.png)  

# 无线LAN与有线LAN

在有线局域网中，当一个站发出一帧时，所有其他站都能接受到这个帧。  
在无线局域网中，由于无线电传输范围有限，无法向所有的站传输帧，也无法接受来自所有其他站的帧。  
在无线局域网中，相对于发送信号而言，接收到的信号可能很微弱，因此，在无线信道中进行冲突检测非常困难，硬件成本高。
 
# 隐藏站问题（Hidden Node Problem）

站B在站A和站C的信号覆盖范围内，可以接受站A和站C的数据，由于竞争者离的太远而导致无法检测到潜在的竞争者，这个问题称为隐藏问题。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82%EF%BC%88CSMA-CA%EF%BC%89%20image%20ab4609698077101b.png)  

# 暴露站问题（Exposed Node Problem）

站B向站A传输数据，站C向站D传输数据。当站C侦听到该范围内有数据传输，为了避免冲突，站C暂停向站D传输数据。不过站C的结论是错误的。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82%EF%BC%88CSMA-CA%EF%BC%89%20image%2083e1adf74c296d94.png)  

# 带碰撞避免的CSMA（CSMA with Collision Avoidance）

带碰撞避免的CSMA（CSMA with Collision Avoidance, CSMA/CA）  
节点在发送数据之前监听无线信道，如果信号强度超过一定阈值则认为当前有其他节点在该信道上发送数据，此时随机等一段时间再次监听。  
如果检测到信道空闲，需要等到一个帧间间隔（InterFrame Space，IFS）之后再发送数据，在等待的时候保持监听。
 
# 帧间间隔（InterFrame Space，IFS）

DIFS（Distributed InterFrame Space）分布式帧间间隔：

1. 用于普通数据帧之间的间隔。
2. 节点在发送数据之前，需要监听信道是否空闲，若信道空闲，则等待DIFS时间再发送

SFIS（Short InterFrame Space）短帧间间隔：

1. 用于控制帧（如ACk、RTS/CTS等）之间的间隔。
2. SIFS是最短的间隔，通常用于控制信道使用的帧。

EIFS（Extened InterFrame Space）扩展帧间间隔：

1. 主要用于错误帧，例如接收到错误数据的节点在发送ACK前需要等待更长时间。
 
# 信道预约

在发送数据帧之前，发送方首先广播一个RTS（Request to Send）帧这个RTS帧能够被其范围内的所有站点侦听到。  
任何一个站若监听到RTS帧，这些站必须保持沉默，等待足够长的时间，以便发送站接收CTS帧。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82%EF%BC%88CSMA-CA%EF%BC%89%20image%209d5cfb30b6bd46cc.png)

接收方收到RTS帧之后，发送一个CTS（Clear to Send）帧作为应答收到CTS之后帧开始进行数据传输。  
任何一个站监听到CTS帧，则这些站在接下来数据传输过程中必须保持沉默。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82%EF%BC%88CSMA-CA%EF%BC%89%20image%20aa8b22b5a70c0585.png)  

# 潜在的碰撞

带碰撞避免的CSMA（CSMA with Collision Avoidance，CSMA/CA）  
尽管有了预约信道来预防碰撞，但是如果多个发送方同时发送RTS帧，这些帧将发生部分冲突，从而丢失数据。发送方没有在期望的时间间隔内收到CTS帧，则判断发生冲突。发送方将等待一段随机时间后，再进行重试。
 
# 轮询访问

当链路中大部分主机都比较繁忙，多台主机同时发送数据频率高，如果采用随机访问的方式，发生冲突的概率会比较高，可以采用轮询访问。

![](OneNote/408/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82%EF%BC%88CSMA-CA%EF%BC%89%20image%206d44a3f5caf65191.png)