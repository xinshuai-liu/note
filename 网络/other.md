1. mac地址
2.1 为什么需要 MAC 地址，不能只用 IP 地址吗
    IP地址（Layer 3）用于网络间路由，MAC地址（Layer 2）用于同一局域网内设备寻址

2.2 如何通过命令行查看本机 MAC 地址
    ipconfig /all
    ifconfig | grep ether

2.3 ARP 协议的作用是什么？它与 MAC 地址的关系？
    ARP（Address Resolution Protocol）用于将IP地址解析为MAC地址
    过程:
        主机A广播ARP请求：“谁的IP是 192.168.1.2？”
        主机B回复：“我的MAC是 00:1A:2B:3C:4D:5E。”
        主机A缓存此映射，后续通信直接使用MAC地址。









