# libp2p 规范
<h1 align="center">
  <img src="https://raw.githubusercontent.com/libp2p/libp2p/a13997787e57d40d6315b422afbe1ceb62f45511/logo/libp2p-logo.png" alt="libp2p logo"/>
</h1>

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io)
[![](https://img.shields.io/badge/project-libp2p-blue.svg?style=flat-square)](http://github.com/libp2p/libp2p)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)

> `libp2p` 是一种模块化、可扩展的网络协议栈，旨在解决点到点应用程序面临的网络挑战；目前被用于 IPFS 底层网络库。

作者:

- [Juan Benet](https://github.com/jbenet)
- [David Dias](https://github.com/diasdavid)

评审:

- `N/A`

## 概述
规范描述了 IPFS 网络协议。网络层为任意两个 IPFS 节点间提供端到端传输（可靠和不可靠传输）

该文档作为 `libp2p` 规范的实现基准。

## 规格完成状态 ![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square)

## 文档结构
`libp2p` 规格意见征求稿 (RFC ) 通过目录章节的格式组织编写，具体目录结构如下文，每章节可在独立的文件中找到。

## 目录

- [1 介绍](1-introduction.md)
  - [1.1 动因](1-introduction.md#11-motivation)
  - [1.2 目标](1-introduction.md#12-goals)
- [2 分析网络堆栈 (network stack) 的最新技术](2-state-of-the-art.md)
  - [2.1 客户端-服务端模型](2-state-of-the-art.md#21-the-client-server-model)
  - [2.2 按解决方案对网络堆栈协议分类](2-state-of-the-art.md#22-categorizing-the-network-stack-protocols-by-solutions)
  - [2.3 当前缺陷](2-state-of-the-art.md#23-current-shortcomings)
- [3 规格基础要求](3-requirements.md)
  - [3.1 传输透明](3-requirements.md#34-transport-agnostic)
  - [3.2 多路复用 Multi-multiplexing](3-requirements.md#35-multi-multiplexing)
  - [3.3 加密](3-requirements.md#33-encryption)
  - [3.4 NAT 穿透](3-requirements.md#31-nat-traversal)
  - [3.5 中继](3-requirements.md#32-relay)
  - [3.6 容许多种类型的网络拓扑结构](3-requirements.md#36-enable-several-network-topologies)
  - [3.7 资源发现](3-requirements.md#37-resource-discovery)
  - [3.8 消息通信](3-requirements.md#38-messaging)
  - [3.9 命名](3-requirements.md#38-naming)
- [4 架构](4-architecture.md)
  - [4.1 节点路由](4-architecture.md#41-peer-routing)
  - [4.2 集群 Swarm](4-architecture.md#42-swarm)
  - [4.3 分布式记录存储](4-architecture.md#43-distributed-record-store)
  - [4.4 发现](4-architecture.md#44-discovery)
  - [4.5 消息传递](4-architecture.md#45-messaging)
    - [4.5.1 发布订阅 PubSub](4-architecture.md#451-pubsub)
  - [4.6 命名](4-architecture.md#46-naming)
    - [4.6.1 IPRS](4-architecture.md#461-iprs)
    - [4.6.2 IPNS](4-architecture.md#462-ipns)
- [5 数据结构](5-datastructures.md)
- [6 接口](6-interfaces.md)
  - [6.1 libp2p](6-interfaces.md#61-libp2p)
  - [6.1 传输](6-interfaces.md)
  - [6.2 节点路由](6-interfaces.md)
  - [6.3 Swarm](6-interfaces.md#63-swarm)
    - [6.3.1 传输]
    - [6.3.2 连接]
    - [6,3,3 流复用 Stream Muxing]
  - [6.4 分布式记录存储]
  - [6.5 节点发现](6-interfaces.md#65-peer-discovery)
  - [6.6 libp2p interface and UX](6-interfaces.md#66-libp2p-interface-and-ux)
- [7 特性](7-properties.md)
  - [7.1 通信模型 - 流](7-properties.md#71-communication-model---streams)
  - [7.2 端口 - 入口约束](7-properties.md#72-ports---constrained-entrypoints)
  - [7.3 传输协议](7-properties.md#73-transport-protocols)
  - [7.4 无 IP 网络 (Non-IP)](7-properties.md#74-non-ip-networks)
  - [7.5 通信协议](7-properties.md#75-on-the-wire)
    - [7.5.1 协议-多路复用](7-properties.md#751-protocol-multiplexing)
    - [7.5.2 多数据流 - 自描述的协议流](7-properties.md#752-multistream---self-describing-protocol-stream)
    - [7.5.3 多数据流-选择器 - 自描述型的协议流选择器 self-describing protocol stream selector](7-properties.md#753-multistream-selector---self-describing-protocol-stream-selector)
    - [7.5.4 Stream Multiplexing 多路复用流](7-properties.md#754-stream-multiplexing)
    - [7.5.5 可移植编码](7-properties.md#755-portable-encodings)
    - [7.5.6 通信安全](7-properties.md#756-secure-communications)
    - [7.5.7 Protocol Multicodecs](7-properties.md#757-protocol-multicodecs)
- [8 实现](8-implementations.md)
- [9 引用](9-references.md)

## 尚未合并到主干规格的分模块规格

- [Relay  中继层](/relay)
- [PubSub  发布订阅](/pubsub)
