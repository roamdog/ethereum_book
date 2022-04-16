# 第十三章

Permalink

Cannot retrieve contributors at this time

### gas（Gas） <a href="#user-content-gas" id="user-content-gas"></a>

**Gas**是以太坊用于衡量程序执行一个或一组动作所需计算量的单位。交易或合约执行的每项操作都需要一定数量的gas; 所需的gas数量与正在执行的计算步骤的类型和数量有关。与仅以千字节（kB）计算交易规模的比特币交易费相比，以太坊交易费必须考虑智能合约代码可以执行的任意数量的计算步骤。程序执行的操作数越多，运行完成的成本就越高。

每次操作都需要固定量的gas。以太坊黄皮书的的一些例子：

* 添加两个数字需要3个gas
* 计算Keccak256哈希值，需要30个gas+ 每256位数据被哈希6个gas
* 发送交易成本为21000 gas

gas是以太坊的重要组成部分，具有双重作用。一，作为以太坊价格（具有波动性）和矿工对其工作的奖励之间的抽象层。另一种是抵御拒绝服务攻击。为了防止网络中的意外或恶意无限循环或其他计算浪费，每个交易的发起者需要设置他们愿意花费在gas上的金额的限制。因此，gas系统阻止攻击者发送垃圾邮件交易，因为他们必须按比例支付他们消耗的计算，带宽和存储资源。

#### 停机问题 <a href="#usercontent-ting-ji-wen-ti" id="usercontent-ting-ji-wen-ti"></a>

交易费和会计的想法似乎很实用，但你可能想知道为什么以太坊首先需要gas。gas是关键，因为它不仅可以解决停机问题，而且对安全和活力也至关重要。什么是停机问题，安全和活力，为什么要关心？

#### 支付gas <a href="#usercontent-zhi-fu-gas" id="usercontent-zhi-fu-gas"></a>

虽然gas有价格，但它不能“拥有”也不能“花”。gas仅存在于以太坊虚拟机（EVM）内部，作为计算工作量的计数。发起方被收取ether交易费，然后转换为gas，然后转回到ether，作为矿工的块奖励。这些转换步骤用于将计算的价格（与“工作量”相关）与ether的价格（与市场波动相关）分开。

#### gas成本与gas价格 <a href="#usercontentgas-cheng-ben-yu-gas-jia-ge" id="usercontentgas-cheng-ben-yu-gas-jia-ge"></a>

虽然**gas成本**是EVM中执行的操作步骤的度量，但gas本身也具有以ether测量的**gas价格**。在执行交易时，发起方指定他们愿意为每个gas单位支付的gas价格（以ether为单位），允许市场决定ether的价格与计算操作的成本之间的关系（以gas衡量） 。

`total gas used * gas price paid = transaction fee`，以ether为单位

此金额将在交易执行开始时从发起方的帐户中扣除。发起方不是设置“total gas used”，而是设置**gas limit**，该限制应足以覆盖执行交易所需的gas量。

#### gas成本限制和gas耗尽 <a href="#usercontentgas-cheng-ben-xian-zhi-he-gas-hao-jin" id="usercontentgas-cheng-ben-xian-zhi-he-gas-hao-jin"></a>

在发送交易之前，发起方必须指定**gas limit** - 他们愿意购买的最大gas数量。他们还必须指定**gas price** - 他们愿意为每单位gas支付的以太价格。

以ether计算的\`gas limit \* gas price\`在交易执行开始时从发起方的账户中扣除作为存款。这是为了防止发送者在执行中期“破产”并且无法支付gas费用。由于这个原因，用户也无法设置超出其帐户余额的gas限制。

理想情况下，发起方将设置一个高于或等于实际使用的gas的gas限制。如果gas限制设置高于消耗的gas量，发货人将收到超额金额的退款，因为矿工只获得他们实际工作的补偿。

在这种情况下：

\`（gas限制 - 多余gas）\*gas价格以太以矿块作为块奖励

`(gas limit - excess gas) * gas price` ether作为矿工的区块奖励

`excess gas * gas price` ether退回发起方

但是，如果使用的gas超过规定的gas限制，即如果在执行期间交易“runs out of gas”，则操作终止。虽然交易不成功，但由于矿工已经完成了计算工作，不会退回发送人的交易费用，矿工因此得到补偿。

**示例**

如果交易是从外部拥有账户（EOA）发送的，则从EOA的余额中扣除gas费。换句话说，交易的发起人正在支付gas费。发起人为交易消耗的总gas以及随后的任何子执行提供资金。这意味着如果发起者X附加1000个gas来调用合约A，其在计算上花费500个gas然后向合约B发送另一个消息，则A用于将消息发送到B的gas也会再已开始从X的gas限制中扣除。

```
EOA帐户X启动交易并调用合约帐户A上的功能，附带1000个gas

合约A在计算上花费500gas，并向合约B发送消耗100gas的消息

合约B在计算上花费300个gas并完成交易。

100个gas退还给X.
```

因此，如果该交易的发起人在开始时没有附加足够高的gas费，那么在交易中执行一部分操作的中间合约（例如，在我们的示例中为合约A）理论上可以耗尽gas。如果合约在执行中期用完，除了gas费支付外，所有状态变更都会被撤销。

#### 估算 Gas <a href="#usercontent-gu-suan-gas" id="usercontent-gu-suan-gas"></a>

通过假装交易已经被包含在区块链中来估算gas，然后返回如果操作是真实的那么可以收取的确切gas量。换句话说，它使用与矿工用来计算实际费用但从未开采过区块链的完全相同的程序。

请注意，由于各种原因（包括EVM机制和节点性能），估计值可能远远超过交易实际使用的gas量。

```
var result = web3.eth.estimateGas({
    to: "0xc4abd0339eb8d57087278718986382264244252f",
    data: "0xc6888fa10000000000000000000000000000000000000000000000000000000000000003"
});
console.log(result); // "0x0000000000000000000000000000000000000000000000000000000000000015"
```

#### gas价格和交易优先顺序 <a href="#usercontentgas-jia-ge-he-jiao-yi-you-xian-shun-xu" id="usercontentgas-jia-ge-he-jiao-yi-you-xian-shun-xu"></a>

gas价格是交易发起方愿意为每个gas单位支付的ether量。开采下一个区块的矿工决定要包括哪些交易。由于gas价格被计入他们将作为奖励的交易费中，他们更可能首先包括具有最高gas价格的交易。如果发起方将gas价格设置得太低，他们可能需要等待很长时间才能将其交易进入一个区块。

矿工还可以决定块中包含交易的顺序。由于多个矿工竞争将其区块附加到区块链，因此区块内的交易顺序由“获胜”矿工任意决定，然后其他矿工用该订单核实。虽然可以任意排列来自不同账户的交易，但是来自个人账户的交易是按照自动递增的随机数的顺序执行的。

#### 谁来决定区块gas限制是多少？ <a href="#usercontent-shui-lai-jue-ding-qu-kuai-gas-xian-zhi-shi-duo-shao" id="usercontent-shui-lai-jue-ding-qu-kuai-gas-xian-zhi-shi-duo-shao"></a>

网络上的矿工决定区块gas限制是什么。想要在以太坊网络上挖矿的个人使用挖矿程序，例如ethminer，它连接到Geth或Parity Ethereum客户端。以太坊协议有一个内置机制，矿工可以对gas限制进行投票，因此无需在硬分叉上进行协调就可以增加容量。块的矿工能够在任一方向上将块气限制调整1/1024（0.0976％）。其结果是根据当时网络的需要调整块大小。这一机制与默认的开采策略结合在一起，矿工默认将投票决定至少470万的gas限制，但如果这一数字更高的话，将把目标对准最近的(1024区块指数移动)平均gas的150%，从而使数量有机地增加。矿工们可以选择改变这一点，但是他们中的许多人不这样做，并保留默认值。

#### gas退款 <a href="#usercontentgas-tui-kuan" id="usercontentgas-tui-kuan"></a>

以太坊通过退还高达一半的gas费用来鼓励删除存储的变量。 EVM中有2个负的gas操作：

清理合约是-24,000（SELFDESTRUCT） 清理存储为-15,000（SSTORE \[x] = 0）

**GasToken**

GasToken是一种符合ERC20标准的token，允许任何人在gas价格低时“储存”gas，并在gas价格高时使用gas。通过使其成为可交易的资产，它基本上创造了一个gas市场。 它的工作原理是利用前面描述的gas退款机制。

#### 租金 <a href="#usercontent-zu-jin" id="usercontent-zu-jin"></a>

目前，以太坊社区提出了一项关于向智能合约收取“租金”以保持活力的建议。

在没有支付租金的情况下，智能合约将被“睡眠”，即使是简单的读取操作也无法获得数据。需要通过支付租金和提交Merkle证据来唤醒进入睡眠状态的合约。



<details>

<summary></summary>



</details>
