2 网络堆栈 (network stack) 技术现状分析
====================================================

This section presents to the reader an analysis of the available protocols and architectures for network stacks. The goal is to provide the foundations from which to infer the conclusions and understand why `libp2p` has the requirements and architecture that it has.

第二章分析网络堆栈体系的协议和架构，旨在为读者提供 libp2p 背后的理论基础和理解 libp2p 协议要求和架构。

## 2.1 客户端-服务端模型

The client-server model indicates that both parties at the ends of the channel have different roles, that they support different services and/or have different capabilities, or in other words, that they speak different protocols.

客户端-服务端模型表明连接的两端作为不同的角色，他们都支持不同的服务、具备不同的特性，也就是他们使用不同的协议。

Building client-server applications has been the natural tendency for a number of reasons:

下述所列几点原因说明为什么 服务端-客户端 模型的应用是主流：

- The bandwidth inside a data center is considerably higher than that available for clients to connect to each other.
- 数据中心的带宽远大于客户端。相比客户端之间的连接，高带宽的数据中心可高效接受多客户端的连接。
- Data center resources are considerably cheaper, due to efficient usage and bulk stocking.
- 高利用率和大量资源累积，数据中心的资源性价比更高。
- It makes it easier for the developer and system admin to have fine grained control over the application.
- 开发者和系统管理员可细粒度控制应用程序。
- It reduces the number of heterogeneous systems to be handled (although the number is still considerable).
- 降低异构系统的数量（即使数量仍然很大）
- Systems like NAT make it really hard for client machines to find and talk with each other, forcing a developer to perform very clever hacks to traverse these obstacles.
- 客户端难以访问 NAT 网络结构的系统，这些系统需要开发者使用黑科技对 NAT 穿透访问。
- Protocols started to be designed with the assumption that a developer will create a client-server application from the start.
- 协议设计之初就假定程序员将会开发客户端-服务端应用。

We even learned how to hide all the complexity of a distributed system behind gateways on the Internet, using protocols that were designed to perform a point-to-point operation, such as HTTP, making it opaque for the application to see and understand the cascade of service calls made for each request.

`libp2p` offers a move towards dialer-listener interactions, from the client-server listener, where it is not implicit which of the entities, dialer or listener, has which capabilities or is enabled to perform which actions. Setting up a connection between two applications today is a multilayered problem to solve, and these connections should not have a purpose bias, and should instead support several other protocols to work on top of the established connection. In a client-server model, a server sending data without a prior request from the client is known as a push model, which typically adds more complexity; in a dialer-listener model in comparison, both entities can perform requests independently.

## 2.2 按解决方案对网络堆栈技术分类

Before diving into the `libp2p` protocols, it is important to understand the large diversity of protocols already in wide use and deployment that help maintain today's simple abstractions. For example, when one thinks about an HTTP connection, one might naively just think that HTTP/TCP/IP are the main protocols involved, but in reality many more protocols participate, depending on the usage, the networks involved, and so on. Protocols like DNS, DHCP, ARP, OSPF, Ethernet, 802.11 (Wi-Fi) and many others get involved. Looking inside ISPs' own networks would reveal dozens more.

Additionally, it's worth noting that the traditional 7-layer OSI model characterization does not fit `libp2p`. Instead, we categorize protocols based on their role, i.e. the problem they solve. The upper layers of the OSI model are geared towards point-to-point links between applications, whereas the `libp2p` protocols speak more towards various sizes of networks, with various properties, under various different security models. Different `libp2p` protocols can have the same role (in the OSI model, this would be "address the same layer"), meaning that multiple protocols can run simultaneously, all addressing one role (instead of one-protocol-per-layer in traditional OSI stacking). For example, bootstrap lists, mDNS, DHT discovery, and PEX are all forms of the role "Peer Discovery"; they can coexist and even synergize.

### 2.2.1 物理硬件连接

- Ethernet
- Wi-Fi
- Bluetooth
- USB

### 2.2.2 硬件寻址

- IPv4
- IPv6
- Hidden addressing, like SDP

### 2.2.3 节点或服务发现

- ARP
- DHCP
- DNS
- Onion

### 2.2.4 通过网络路由信息

- RIP(1, 2)
- OSPF
- BGP
- PPP
- Tor
- I2P
- cjdns

### 2.2.5 传输协议

- TCP
- UDP
- UDT
- QUIC
- WebRTC data channel

### 2.2.6 应用程序间服务通讯协议

- RMI
- Remoting
- RPC
- HTTP

## 2.3 当前网络堆栈技术瓶颈

Although we currently have a panoply of protocols available for our services to communicate, the abundance and variety of solutions creates its own problems. It is currently difficult for an application to be able to support and be available through several transports (e.g. the lack of TCP/UDP stack in browser applications).

There is also no 'presence linking', meaning that there isn't a notion for a peer to announce itself in several transports, so that other peers can guarantee that it is always the same peer.
