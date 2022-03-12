---
title: "3. 协议概述"
anchor: "3_Protocol_Overview"
weight: 300
rank: "h1"
---

QUIC（详见《[QUIC传输]()》）负责数据包的可信度和完整性保护。为此它使用了衍生自TLS握手（详见《[TLS13]()》）的密钥，但如[图3]()所示，TLS握手和警告消息由QUIC传输层直接传递，而不是在QUIC传输层的基础上使用TLS记录来传递（TCP是这么做的），也就是说QUIC接管了TLS记录层的职责。

> TODO：图3

{{< block_img
indx="Figure_3_QUIC_Layers"
title="图3：QUIC的层"
type="svg"
src="/RFC9000_Chinese_Translation/images/Figure_2_States_for_Sending_Parts_of_Streams.svg" >}}

QUIC还依靠TLS来验证和协商那些安全和性能方面的关键参数。

这两种协议间没有严格的层次区分，取而代之的是它们相互合作：QUIC使用TLS的握手；TLS使用由QUIC提供的可靠性、有序交付和记录层等特性。

抽象地说，TLS组件和QUIC组件间主要有两类交互：

* TLS组件经由QUIC组件发送和接收消息，QUIC向TLS提供一种可靠的流的抽象。

* TLS组件向QUIC组件提供一系列状态更新，包括(a)新的数据包保护密钥，和(b)状态变更，例如握手完成、服务器证书，等等。

[图4]()更详细地展示了这些交互，并且把QUIC数据包保护单独提了出来。

> TODO：图4

{{< block_img
indx="Figure_4_QUIC_and_TLS_Interactions"
title="图4：QUIC和TLS的交互"
type="svg"
src="/RFC9000_Chinese_Translation/images/Figure_2_States_for_Sending_Parts_of_Streams.svg" >}}

不像基于TCP的TLS，想要发送数据的QUIC应用并不使用TLS应用数据记录来发送，而是将数据以QUIC**流帧**或其他类型的帧的形式发送，它们都是由QUIC数据包传递的。
