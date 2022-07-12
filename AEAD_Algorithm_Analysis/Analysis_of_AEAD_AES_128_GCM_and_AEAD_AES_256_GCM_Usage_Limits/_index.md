---
title: "B.1. 对于AEAD_AES_128_GCM和AEAD_AES_256_GCM用量上限的分析"
anchor: "B.1_Analysis_of_AEAD_AES_128_GCM_and_AEAD_AES_256_GCM_Usage_Limits"
weight: 1310
rank: "h2"
---

《[GCM-MU](https://doi.org/10.1145/3243734.3243816)》具体说明了`AEAD_AES_128_GCM`和`AEAD_AES_256_GCM`被用在TLS 1.3和QUIC中时准确的用量上限。本节使用了一些经简化的假设来概述这份分析：

* 攻击者在尝试伪造时使用的密文块数量上限为`v * l`，即尝试伪造的次数乘以每个数据包（以块为单位）的大小。

* 攻击者在线下完成的工作量在本分析的各项因素中并不占据主导地位。

《[GCM-MU](https://doi.org/10.1145/3243734.3243816)》中设定的上限比《[AEBounds](https://www.isg.rhul.ac.uk/~kp/TLS-AEbounds.pdf)》中使用的那些要更严格且更完备，这使得QUIC实现能够使用比《[TLS13](https://www.rfc-editor.org/info/rfc8446)》中所描述的更大的限制。
