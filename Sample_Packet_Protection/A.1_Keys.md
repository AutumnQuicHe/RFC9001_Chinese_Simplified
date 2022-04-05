---
title: "A.1. 密钥"
anchor: "A.1_Keys"
weight: 1210
rank: "h2"
---

在`HKDF-Expand-Label`函数的执行期间生成的标签（也就是`HkdfLabel.label`），以及传给`HKDF-Expand`函数的参数为：

`client in`: `00200f746c73313320636c69656e7420696e00`

`server in`: `00200f746c7331332073657276657220696e00`

`quic key`: `00100e746c7331332071756963206b657900`

`quic iv`: `000c0d746c733133207175696320697600`

`quic hp`: `00100d746c733133207175696320687000`

初始秘密值是通用的：

{{% block_ref
indx="Pseudocode_A_1_1" %}}

```
initial_secret = HKDF-Extract(initial_salt, cid)
    = 7db5df06e7a69e432496adedb0085192
      3595221596ae2ae9fb8115c1e9ed0a44
```

{{% /block_ref %}}

用于保护客户端数据包的秘密值为：

{{% block_ref
indx="Pseudocode_A_1_2" %}}

```
client_initial_secret
    = HKDF-Expand-Label(initial_secret, "client in", "", 32)
    = c00cf151ca5be075ed0ebfb5c80323c4
      2d6b7db67881289af4008f1f6c357aea

key = HKDF-Expand-Label(client_initial_secret, "quic key", "", 16)
    = 1f369613dd76d5467730efcbe3b1a22d

iv  = HKDF-Expand-Label(client_initial_secret, "quic iv", "", 12)
    = fa044b2f42a3fd3b46fb255c

hp  = HKDF-Expand-Label(client_initial_secret, "quic hp", "", 16)
    = 9f50449e04a0e810283a1e9933adedd2
```

{{% /block_ref %}}

用于保护服务器数据包的秘密值为：

{{% block_ref
indx="Pseudocode_A_1_3" %}}

```
server_initial_secret
    = HKDF-Expand-Label(initial_secret, "server in", "", 32)
    = 3c199828fd139efd216c155ad844cc81
      fb82fa8d7446fa7d78be803acdda951b

key = HKDF-Expand-Label(server_initial_secret, "quic key", "", 16)
    = cf3a5331653c364c88f0f379b6067e37

iv  = HKDF-Expand-Label(server_initial_secret, "quic iv", "", 12)
    = 0ac1493ca1905853b0bba03e

hp  = HKDF-Expand-Label(server_initial_secret, "quic hp", "", 16)
    = c206b8d9b9f0f37644430b490eeaa314
```

{{% /block_ref %}}
