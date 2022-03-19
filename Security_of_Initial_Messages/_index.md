---
title: "7. 初始消息的安全性"
anchor: "7_Security_of_Initial_Messages"
weight: 700
rank: "h1"
---

Initial packets are not protected with a secret key, so they are subject to potential tampering by an attacker. QUIC provides protection against attackers that cannot read packets but does not attempt to provide additional protection against attacks where the attacker can observe and inject packets. Some forms of tampering -- such as modifying the TLS messages themselves -- are detectable, but some -- such as modifying ACKs -- are not.

初始数据包并不受密钥的保护，因此它们可能会被攻击者篡改。QUIC提供了针对无法读取数据包的攻击者的保护，但此保护并不足以抵御来自有能力观测和注入数据包的攻击者的攻击。部分形式的篡改——例如TLS消息的修改——是能被检测出来的，但是另一些——例如**ACK帧**的修改——则不能。

For example, an attacker could inject a packet containing an ACK frame to make it appear that a packet had not been received or to create a false impression of the state of the connection (e.g., by modifying the ACK Delay). Note that such a packet could cause a legitimate packet to be dropped as a duplicate. Implementations SHOULD use caution in relying on any data that is contained in Initial packets that is not otherwise authenticated.

举例来说，攻击者可以注入一个包含**ACK帧**的数据包，以使得某个数据包看上去还未被接收到，或建立有关连接状态的错误印象（例如，通过修改ACK延迟）。注意，这样的数据包会使得本应合法的数据包被认为是重复而丢弃。对于初始数据包中包含的未经其他途径验证的数据，QUIC实现{{< req_level SHOULD >}}谨慎地使用它们。

It is also possible for the attacker to tamper with data that is carried in Handshake packets, but because that sort of tampering requires modifying TLS handshake messages, any such tampering will cause the TLS handshake to fail.

攻击者还有可能篡改使用握手数据包传递的数据，但由于这类篡改依赖于修改TLS握手消息，所以它们会使得TLS握手失败。
