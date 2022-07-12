---
title: "10. 关于IANA的考量"
anchor: "10_IANA_Considerations"
weight: 1000
rank: "h1"
---

IANA已经在“TLS扩展类型值”注册表（详见《[TLS-REGISTRIES](https://www.rfc-editor.org/info/rfc8447)》）中为`quic_transport_parameters`（QUIC传输参数）扩展（有关定义详见[第8.2章](#8.2_QUIC_Transport_Parameters_Extension)）注册了值为`57`（也就是`0x39`）的码点。

该扩展的受推荐一栏被标记为“是”。TLS 1.3一栏中包含CH（`ClientHello`，客户端问候）和EE（`EncryptedExtensions`，加密扩展）。

{{% block_ref
indx="Table_2_TLS_ExtensionType_Values_Registry_Entry"
title="表2：TLS扩展类型值注册项" %}}

| 值   | 扩展名称                      | TLS 1.3 | 受推荐 | 参考文献 |
|:----|:--------------------------|:--------|:----|:-----|
| 57  | quic_transport_parameters | CH, EE  | 是   | 本文档  |

{{% /block_ref %}}
