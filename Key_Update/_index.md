---
title: "6. 密钥更新"
anchor: "6_Key_Update"
weight: 600
rank: "h1"
---

当握手完成时（详见[第4.1.2章]()），终端{{< req_level MAY >}}发起密钥更新。

使用密钥阶段比特位可以区分用于保护数据包的数据包保护密钥。密钥阶段比特位在第一组1-RTT数据包上被初始化为状态`0`，并在后续每次密钥更新时切换状态。

密钥阶段比特位使得接收方即使没有接收到第一个发送的会引发密钥材料变化的数据包，也能检测到这种变化。注意到密钥阶段比特位变化的终端会更新密钥，再解密那个比特位发生变化的数据包。

发起密钥更新会导致两侧终端均更新密钥。这与TLS不同，终端在后者中可以独立更新密钥。

这项机制代替了TLS的密钥更新机制，后者依赖于受到1-RTT加密密钥保护的`KeyUpdate`（密钥更新）消息。终端{{< req_level MUST_NOT >}}发送TLS的`KeyUpdate`消息。终端{{< req_level MUST >}}将受到TLS的`KeyUpdate`消息的情况视作类型为`0x010a`的连接错误，它等价于TLS中致命级别的`unexpected_message`（意外的消息）警报；详见[第4.8章]()。

[图9]()展示了密钥更新的过程，其中初始时使用的那组密钥（标记为`@M`）被更新后的密钥（标记为`@N`）代替了。密钥阶段比特位的值用中括号`[]`来表示。

> TODO：图9

{{< block_img
indx="Figure_9_Key_Update"
title="图9：密钥更新"
type="svg"
src="/RFC9000_Chinese_Translation/images/Figure_2_States_for_Sending_Parts_of_Streams.svg" >}}
