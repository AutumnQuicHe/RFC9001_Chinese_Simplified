---
title: "8. QUIC中对TLS握手的调整"
anchor: "8_QUIC-Specific_Adjustments_to_the_TLS_Handshake"
weight: 800
rank: "h1"
---

Certain aspects of the TLS handshake are different when used with QUIC.

与QUIC一起使用时，TLS某些方面的行为会发生变化。

QUIC also requires additional features from TLS. In addition to negotiation of cryptographic parameters, the TLS handshake carries and authenticates values for QUIC transport parameters.

QUIC还需要TLS提供额外功能。除了协商加密参数外，TLS握手还要传递和认证QUIC的传输参数。
