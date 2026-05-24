---
title: "A.4. 重试数据包"
anchor: "A.4_Retry"
weight: 1240
rank: "h2"
---

这里展示了一个可以被用于响应[附录A.2](#A.2_Client_Initial)中的初始数据包的重试数据包。完整性检查中使用了了由客户端选择的值为`0x8394c8f03e515708`的连接ID，但是这个值不会被包含在最终的重试数据包的明文中：

{{% block_ref
indx="Pseudocode_A_4_1" %}}

```
ff000000010008f067a5502a4262b574 6f6b656e04a265ba2eff4d829058fb3f
0f2496ba
```

{{% /block_ref %}}
