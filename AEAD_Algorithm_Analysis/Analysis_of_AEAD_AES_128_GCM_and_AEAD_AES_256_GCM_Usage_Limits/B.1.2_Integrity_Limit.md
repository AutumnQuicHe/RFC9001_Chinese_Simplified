---
title: "B.1.2. 完整性上限"
anchor: "B.1.2_Integrity_Limit"
weight: 1312
rank: "h3"
---

在完整性方面，《[GCM-MU]()》中的定理4.3指出，攻击者在伪造数据包时次数不需要超过此值就能获得明显优势：

{{% block_ref
indx="Pseudocode_B_1_2_1" %}}

```
(1 / 2^(8 * n)) + ((2 * v) / 2^(2 * n))
        + ((2 * o * v) / 2^(k + n)) + (n * (v + (v * l)) / 2^k)
```

{{% /block_ref %}}

我们的目标是将此优势限制到<code>2<sup>-57</sup></code>以下。对于`AEAD_AES_128_GCM`，不等式中的第四项占据主导地位，所以其余项可以被移除而不会对结果产生重要影响。这会产生以下近似结果：

{{% block_ref
indx="Pseudocode_B_1_2_2" %}}

```
v <= 2^64 / l
```

{{% /block_ref %}}

不会尝试对超过<code>2<sup>11</sup></code>字节的数据包移除保护的终端最多可以尝试为<code>2<sup>57</sup></code>个数据包移除保护。并不限制所处理的数据包尺寸的终端最多可以尝试为<code>2<sup>52</sup></code>个数据包移除保护。

对于`AEAD_AES_256_GCM`，占据主导地位的是同一项，但是较大的`k`值会产生以下近似结果：

{{% block_ref
indx="Pseudocode_B_1_2_3" %}}

```
v <= 2^192 / l
```

{{% /block_ref %}}

这比对`AEAD_AES_128_GCM`的限制要大得多。但是，本文档建议对两个函数施加同样的限制，因为任一限制都是可接受且足够大的。
