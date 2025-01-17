# 第十七章

Permalink

Cannot retrieve contributors at this time

### 节点间的通信 —— 一个简单的视角 <a href="#user-content-communications_between_nodes" id="user-content-communications_between_nodes"></a>

以太坊节点之间通过简单的线路协议进行通信，形成一个虚拟或覆盖良好的网络 为实现这一目标，该协议称为\*ÐΞVp2p\*，使用\*RLP\*等技术和标准。

#### 传输协议 <a href="#user-content-transport_protocol" id="user-content-transport_protocol"></a>

为了提供机密性并防止网络中断，**ÐΞVp2p\*节点使用\*RLPx\*消息，一种加密且经过身份验证的\_transport协议。 \*RLPx\*使用类似于\*Kademlia\*的路由算法，\*Kademlia\*是用于分散的对等计算机网络的分布式哈希表（** DHT **）。 \*RLPx**，作为底层传输协议，允许\_“节点发现和网络形成”_。 \*RLPx\*的另一个显著特征是通过单个连接支持\_多个协议_。

当\*ÐΞVp2p\*节点通过Internet进行通信时（通常情况下），它们使用TCP，它提供面向连接的介质，但实际上\*ÐΞVp2p\*节点通过使用底层传输协议\*RLPx\*所提供的所谓设施（或消息），以数据包通信，允许它们通信发送和接收数据包。

数据包是 _动态构建_ _dynamicically framed_，前缀为\_RLP\_编码标头，经过加密和验证。通过帧头实现多路复用，帧头指定分组的目的协议。

**加密握手**

通过握手建立连接，并且一旦建立，就将数据包加密并封装为帧。

此握手将分两个阶段进行，第一阶段涉及密钥交换，第二阶段将执行身份验证，作为\*DEVp2p\*的一部分，还将交换每个节点的功能。

**安全 - 基本考虑因素**

所有加密操作都基于\*secp256k1\*，并且每个节点都应该维护一个静态私钥，该私钥在会话之间保存和恢复。

在实施加密之前，数据包具有时间戳属性，以减少执行重放攻击的时间窗口。 建议接收方只接受最近3秒内创建的数据包。

数据包被签名。通过从签名中恢复公钥并检查它是否与预期值匹配来执行验证。

#### ÐΞVp2p 消息和子协议 <a href="#user-content-devp2p_messages_subprotocols" id="user-content-devp2p_messages_subprotocols"></a>

使用\*RLP\*，我们可以编码不同类型的数据，其类型由RLP的第一个条目中使用的整数值确定。 这样，**ÐΞVp2p**，_基础线路协议_ _basic wire protocol_，支持\_任意的子协议\_。

\`0x00-0x10\`之间的\_Message IDs\_保留用于\*ÐΞVp2p\*消息。因此，假定\_sub-protocols\_的消息ID从“0x10”开始。

未在对等节点之间共享的子协议是\_忽略的\_。 如果共享相同（同名）子协议的多个版本，则数字最高的胜出。

**基本建立通信 - 基本ÐΞVp2p消息**

作为一个非常基本的例子，当两个对等节点发起他们的通信时，每个对等节点用另一个称为\*“Hello”**的特殊\*ÐΞVp2p\*消息来迎接另一个，该消息由“0x00”消息ID标识。 通过这个特定的\*ÐΞVp2p** \*“Hello”\*消息，每个节点将向其对等的相关数据公开，从而允许通信以非常基本的级别开始。

在此步骤中，每个对等方将知道有关其对等方的以下信息。

* P2P协议的实现\*版本\*。现在必须是'1\`。
* **客户端软件标识**，作为人类可读的字符串（例如\`Ethereum（++）/ 1.0.0\`）。
* 对等节点的\*capability name\*为长度为3的ASCII字符串。当前支持的能力名称为“eth”和“shh”。
* 对等节点的\*capability version\*为正整数。目前支持的版本是\`eth\`为\`34\`，``shh`为`1``。
* 客户端正在侦听的\*端口\*。如果为“0”则表示客户端没有收听。
* \*节点的唯一标识\*指定为512位散列。

**断开连接 - 基本ÐΞVp2p消息**

要执行有序的断开连接，要断开连接的节点将发送名为\*“Disconnect”**的\*ÐΞVp2p\*消息，该消息由\_“0x01”\_消息ID标识。此外，节点使用参数**“reason”\*指定断开的原因。

* “reason”**参数可以取值从“0x00”到“0x10”，例如“0x00”表示原因**“请求断开连接”**和“0x04”表示**“太多对等节点”\*。

**状态 - 以太坊子协议示例**

该子协议由\`+0x00\`消息-id标识。

此消息应在初始握手之后和任何与以太坊相关的消息之前发送，并通知其当前状态。

为此，节点向其对等方公开以下数据;

* **Protocol version**
* **Network Id**
* **Total Difficulty of the best chain**
* **Hash of the best known block**
* **Hash of the Genesis block**

**已知的当前网络ID**

这里是目前已知的网络ID列表：

* 0: **Olympic**; 以太坊公共预发布测试网
* 1: **Frontier**; Homestead，Metropolis，以太坊公共主网
* 1: **Classic**; (un)forked 公共以太坊Classic主网络，链ID 61
* 1: **Expanse**; 另一个以太坊实现，链ID 2
* 2: **Morden**; 公共以太坊测试网，现在是以太坊经典测试网
* 3: **Ropsten**; 公共跨客户端以太坊测试网
* 4: **Rinkeby**: 公共Geth以太坊测试网
* 42: **Kovan**; 公共Parity以太坊测试网
* 77: **Sokol**; 公共POA测试网
* 99: **POA**; 公共权威证明（PoA）以太网网络
* 7762959: **Musicoin**; 音乐区块链

**GetBlocks - 另一个子协议示例**

该子协议由\`+ 0x05\` message-id标识。

通过此消息，节点通过其自己的哈希向其对等方请求指定的块。

请求节点的方式是通过包含它们所有哈希值的列表，将消息采用以下形式;

```
[+0x05: P, hash_0: B_32, hash_1: B_32, ...]
```

请求节点必须没有包含所有请求的块的响应消息，在这种情况下，它必须再次请求那些尚未由其对等方发送的消息。

#### 节点标识和声誉 <a href="#usercontent-jie-dian-biao-shi-he-sheng-yu" id="usercontent-jie-dian-biao-shi-he-sheng-yu"></a>

\*ÐΞVp2p\*节点的标识是\*secp256k1\*公钥。

客户端可以自由标记新节点并使用节点ID作为\_决定节点的信誉\_的方法。

他们可以存储给定ID的评级并相应地给予优先权。



<details>

<summary></summary>



</details>
