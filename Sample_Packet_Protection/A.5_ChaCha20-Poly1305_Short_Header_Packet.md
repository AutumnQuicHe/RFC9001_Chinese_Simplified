---
title: "A.5. 使用ChaCha20-Poly1305的短包头数据包"
anchor: "A.5_ChaCha20-Poly1305_Short_Header_Packet"
weight: 1250
rank: "h2"
---

本例展示了保护短包头数据包时所需的一些步骤。本例使用了`AEAD_CHACHA20_POLY1305`。

在本例中，TLS生成了一个应用写入秘密值（`secret`），服务器使用`HKDF-Expand-Label`从这个秘密值生成四个值：一个密钥（`key`）、一个IV（`iv`）、一个头部保护密钥（`hp`），和一个将被在密钥被更新后使用到的秘密值（`ku`，但它在本例中没有被使用到）。

{{% block_ref
indx="Pseudocode_A_5_1" %}}

```
secret
    = 9ac312a7f877468ebe69422748ad00a1
      5443f18203a07d6060f688f30f21632b

key = HKDF-Expand-Label(secret, "quic key", "", 32)
    = c6d98ff3441c3fe1b2182094f69caa2e
      d4b716b65488960a7a984979fb23e1c8

iv  = HKDF-Expand-Label(secret, "quic iv", "", 12)
    = e0459b3474bdd0e44a41c144

hp  = HKDF-Expand-Label(secret, "quic hp", "", 32)
    = 25a282b9e82f06f21f488917a4fc8f1b
      73573685608597d0efcb076b0ab7a7a4

ku  = HKDF-Expand-Label(secret, "quic ku", "", 32)
    = 1223504755036d556342ee9361d25342
      1a826c9ecdf3c7148684b36b714881f9
```

{{% /block_ref %}}

下面展示了保护一个目标连接ID为空的最小数据包时所需的一些步骤。这个数据包仅包含了一个**Ping帧**（也就是说，载荷是`0x01`），并且其数据包号为`654360564`。在本例中，使用长度为`3`的数据包号编码方式（也就是编码为`49140`）避免了扩充数据包载荷的需要；如果数据包号被编码至更少的字节中，那么就需要**填充帧**。

{{% block_ref
indx="Pseudocode_A_5_2" %}}

```
pn                 = 654360564 # 十进制
nonce              = e0459b3474bdd0e46d417eb0
unprotected header = 4200bff4
payload plaintext  = 01
payload ciphertext = 655e5cd55c41f69080575d7999c25a5bfb
```

{{% /block_ref %}}

其结果密文的长度是在可能的范围中最小的。在为头部保护采样时，会跳过一个字节。

{{% block_ref
indx="Pseudocode_A_5_3" %}}

```
sample = 5e5cd55c41f69080575d7999c25a5bfb
mask   = aefefe7d03
header = 4cfe4189
```

{{% /block_ref %}}

经保护的数据包，其21字节的长度是在可能的范围中最小的。

{{% block_ref
indx="Pseudocode_A_5_4" %}}

```
packet = 4cfe4189655e5cd55c41f69080575d7999c25a5bfb
```

{{% /block_ref %}}
