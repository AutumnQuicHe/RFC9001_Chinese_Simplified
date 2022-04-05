---
title: "A.3. 服务器初始数据包"
anchor: "A.3_Server_Initial"
weight: 1230
rank: "h2"
---

作为回应，服务器会发送以下载荷，其中包含一个**ACK帧**和一个**加密帧**，并且不包含**填充帧**：

{{% block_ref
indx="Pseudocode_A_3_1" %}}

```
02000000000600405a020000560303ee fce7f7b37ba1d1632e96677825ddf739
88cfc79825df566dc5430b9a045a1200 130100002e00330024001d00209d3c94
0d89690b84d08a60993c144eca684d10 81287c834d5311bcf32bb9da1a002b00
020304
```

{{% /block_ref %}}

来自服务器的头部包含着一个新的连接ID和一个值为`1`且被编码至双字节中数据包号：

{{% block_ref
indx="Pseudocode_A_3_2" %}}

```
c1000000010008f067a5502a4262b50040750001
```

{{% /block_ref %}}

对载荷进行保护后，从第三个密文字节起的一段数据被取作头部保护的样本。

{{% block_ref
indx="Pseudocode_A_3_3" %}}

```
sample = 2cd0991cd25b0aac406a5816b6394100
mask   = 2ec0d8356a
header = cf000000010008f067a5502a4262b5004075c0d9
```

{{% /block_ref %}}

最后，经保护的数据包的内容为：

{{% block_ref
indx="Pseudocode_A_3_4" %}}

```
cf000000010008f067a5502a4262b500 4075c0d95a482cd0991cd25b0aac406a
5816b6394100f37a1c69797554780bb3 8cc5a99f5ede4cf73c3ec2493a1839b3
dbcba3f6ea46c5b7684df3548e7ddeb9 c3bf9c73cc3f3bded74b562bfb19fb84
022f8ef4cdd93795d77d06edbb7aaf2f 58891850abbdca3d20398c276456cbc4
2158407dd074ee
```

{{% /block_ref %}}
