---
title: "1. 介绍"
anchor: "1_Introduction"
weight: 100
rank: "h1"
---

本文档描述了如何使用TLS（详见《[TLS13](https://www.rfc-editor.org/info/rfc8446)》）来加固QUIC（详见《[QUIC传输](../RFC9000_Chinese_Translation)》）的安全。

TLS 1.3比起之前的版本，在延迟方面为连接的建立提供了重要的性能提升。在没有数据包丢包的情况下，绝大多数新连接都能够在单次往返时间内得到建立和加固；当在相同客户端和服务器间进行后续连接时，客户端通常可以立即发送应用数据，也就是，使用零往返启动来进行连接。

本文档描述了TLS作为QUIC的安全组件时是如何工作的。
