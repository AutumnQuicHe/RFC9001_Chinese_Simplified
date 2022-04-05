---
title: "B.1.1. 可信度上限"
anchor: "B.1.1_Confidentiality_Limit"
weight: 1311
rank: "h3"
---

在可信度方面，《[GCM-MU]()》中的定理4.3指出，对于一个不会重复随机数的用户，计算攻击者随机选择的AEAD算法相比实际使用的真实AEAD算法的优势程度的表达式为：

{{% block_ref
indx="Pseudocode_B_1_1_1" %}}

```
2 * (q * l)^2 / 2^n
```

{{% /block_ref %}}

当目标优势度为<code>2<sup>-57</sup></code>时，会得到这样的关系：

{{% block_ref
indx="Pseudocode_B_1_1_2" %}}

```
q <= 2^35 / l
```

{{% /block_ref %}}

因此，发送不超过<code>2<sup>11</sup></code>字节的数据包的终端无法在单条连接中保护<code>2<sup>28</sup></code>个以上的数据包却不让攻击者获得超过<code>2<sup>-57</sup></code>优势度。对于允许数据包尺寸达到<code>2<sup>16</sup></code>字节的终端，则该限制为<code>2<sup>23</sup></code>个数据包。
