# 第十七九章

### 以太坊分叉历史 <a href="#user-content-ethereum_fork_history" id="user-content-ethereum_fork_history"></a>

大多数硬分叉计划作为路线图的一部分，并包含社区普遍认同的更新; 这通常被称为共识。然而，一些硬分叉并不总是保持共识，这导致多个不同的区块链。导致以太坊/以太坊经典分裂的事件就是这种情况。

#### 以太坊经典（ETC） <a href="#user-content-etc_origin" id="user-content-etc_origin"></a>

在以太坊社区的成员继续使用时间敏感的硬分叉（“DAO Hard Fork”）之后，以太坊经典就出现了。2016年7月20日，在以192万的区块高度上，以太坊通过硬分叉引入了不规则的状态变化，从而退还大约360万的ether，这些以太币来自一个名为The DAO的智能合约。

社区中的一些人不同意这种变化，认为这违反了以太坊的不变性; 他们选择在以太坊经典的绰号下继续保持原有的链条。虽然分裂本身最初是意识形态的，但两个链条已经发展成为它们各自独立的实体。

#### 去中心化的自治组织（The DAO） <a href="#user-content-dao_origin" id="user-content-dao_origin"></a>

DAO是由Slock.It创建的; 一支技术精湛的开发团队，包括以前的以太坊创始成员。Slock.It 将DAO视为基于社区为项目提供的资金的一种方式。其核心思想是提交提案，管理者人将管理提案，资金将从以太坊社区的投资者筹集，如果项目证明成功，那么投资者将获得一部分利润。

DAO也是以太坊 token中的第一个实验之一。参与者不是直接用Ether资助项目，而是将他们的以太币交换为DAO代币，使用它们对项目资金进行投票，然后能够将它们交换为以太币。

DAO token能够在2016年4月5日至4月30日期间的众筹中购买，占据了当时总价值约1.5亿美元的全部以太存款的近14％\[1]。

#### 重入（ Re-Entrancy ）Bug <a href="#user-content-dao_reentrancy_bug" id="user-content-dao_reentrancy_bug"></a>

6月9日，开发商Peter Vessenes和Chriseth报告称，大多数基于以太坊的合约管理基金都可能容易受到可以清空合约资金的漏洞<<\[2]>>的影响。几天后（6月12日）斯蒂芬·塔尔（Slock.It的创始人）报告说，DAO的代码并不容易受到彼得和克里斯描述的错误的影响。<<\[3]>> 令人担忧的DAO贡献者暂时松了一口气，直到5天后（6月17日），一名未知的攻击者（“DAO攻击者”）开始使用类似于6月9日描述的漏洞利用DAO <<\[4]>> 。最终，DAO攻击者从DAO中吸取了大约360万个ether。

同时，一群自称为Robinhood Group（RHG）的志愿者开始使用相同的漏洞来提取剩余的资金。6月21日，RHG宣布<<\[5]>>他们已经获得了另外70％的DAO，约720万以太，并计划将其退还社区。RHG的快速行动和思考被给予了很多感谢和赞扬，这有助于保护社区的大部分ether。

**Re-Entrancy技术**

虽然Phil Daian <<\[6]>> 描述了对该错误的更详细和详尽的解释，但简短的解释是可以在以太坊虚拟机上同时多次调用合约函数）。这允许DAO攻击者反复请求提取ether，并且在合约记录DAO攻击者已经提取之前，攻击者再次提取。

**Re-Entrancy 攻击流程**

想象一下，你的银行账户中有100美元，你可以向你的银行出纳员提取任意数量的提款单。银行出纳员按顺序为你提供每张单据的金额，并且只有在所有单据结束时才会记录你的提款。如果你给他们带来三张单，每张100美元怎么办？如果你给他们带来三千个怎么办？

**换句话说，流程是：**

1. DAO攻击者要求DAO合约提取DAO tokens。
2. 在合约更新其DAO被提取的记录之前，DAO攻击者要求合约再次提取DAO。
3. 尽可能重复第二步。
4. 合约最终记录了一次DAO的提取，失去了在此期间发生的取款。

#### DAO硬分叉 <a href="#user-content-dao_hard_fork" id="user-content-dao_hard_fork"></a>

DAO中的一想安全措施是所有提款请求都要延迟28天。这为社区提供了一个简短的时间来讨论如何处理漏洞利用。从大约6月17日到7月20日，DAO攻击者将无法将他们的DAO token转换为ether。

一些开发人员专注于寻找可行的解决方案，并在这么短的时间内探索了多种途径。其中包括6月24日宣布的DAO软分叉推迟DAO的退出，直到达成共识<<\[7]>>，以及7月15日宣布的DAO硬分叉，以不正常的方式扭转DAO攻击影响的状态改变<<\[8]>>。

6月28日，开发人员在DAO软分叉<<\[9]>>中发现了一个DoS漏洞，并得出结论，DAO硬分叉将是fork之路上的唯一可行选择。DAO硬分叉将把所有投资于DAO的ether转移到新的退款智能合约中，允许ether的原始所有者要求全额退款。这为返还被黑的资金提供了解决方案，但也意味着干扰网络上特定地址的余额；但他们是孤立的。在DAO的部分中也会有一些剩余的ether，称为childDAO <<\[12]>>。一组受托人将手动授权剩余的ether；当时的价值约为6-7百万美元<<\[8]>>。

随着时间的推移，多个以太坊开发团队创建了允许用户决定是否要启用此分叉的客户端。但是，客户端创建者想要决定是否选择 opt-in（默认不分叉），或选择opt-out（默认分叉）。7月15日，Carbonvote.com上的投票开始了<<\[10]>>。7月16日，在块\[1,894,000] <<\[11]>>，它被关闭。在以太供应总票数的5.5％中，约80％的选票（约占总供应量的4.5％）投票选择opt-out。选择opt-out的投票的四分之一来自单一地址<<\[12]>>。

最终决定成为选择opt-out，反对DAO硬分叉的人需要通过更改他们运行的软件中的配置选项来不分叉。

7月20日，在块1,920,000 <<\[13]>> 以太坊实施了DAO硬分叉 <<\[14]>>，因此创建了两个以太坊，一个支持不规则的状态变化，另一个与它相对。

当硬分叉的以太坊（现今的以太坊）获得了大部分采矿权时，许多人认为达成共识并且少数群体链将逐渐消失; 和以前的分叉一样。尽管如此，以太坊社区的相当大一部分开始支持原来的区块链，后来被称为以太坊经典。

几天之内，几个交易所开始列出以太坊（“ETH”）和以太坊经典（“ETC”）。由于硬分叉的性质，所有在分拆时持有ether的以太网用户现在都在两个区块链中都持有资金，在Poloniex于7月24日列出ETC后，ETC的市场价值很快就建立了 <<\[15]>>。

**硬分叉的讨论**

在DAO硬分叉前几周，/r/ethereum subreddit上发生了很多讨论。一些流行/关键的论点总结如下。

| 论点        | 原因                                      | 反对                                                                       |
| --------- | --------------------------------------- | ------------------------------------------------------------------------ |
| 责任/正义     | 如果可能的话，社区可以负责确定是否发生了盗窃并且应该纠正。有道德要求。     | 确定盗窃是否已经发生并且应该纠正的责任应该只由法律机构来完成。如果受影响的各方参与决策，则无法消除偏见。                     |
| DAO协议     | DAO的大多数参与者无法正确评估代码，因此他们不能同意受DAO代码的约束。   | DAO的条款和条件<<\[23]>>的开头段落声明“…​…​ DAO的代码控制并阐述了DAO创作的所有条款。”                  |
| 区块链不变性    | 区块链不变性是一种社会结构，因此如果多数人同意，我们可以改变它。        | 区块链不变性是一种社会结构，因此强制执行不变性非常重要。                                             |
| 选择加入与选择退出 | 社区可以选择Hard Fork是选择加入还是选择退出。我们投票决定是选择退出。 | 历史上Hard Forks是选择加入（即比特币）而非投票是不投票。在约1天的时间内，选择退出投票仅占总供应投票的4.5％。<< \[12] >> |

#### DAO硬分叉的时间线 <a href="#user-content-dao_hard_fork_timeline" id="user-content-dao_hard_fork_timeline"></a>

* 4月5日：Slock.It 在Dejavu Security<<\[16]>>的安全审计之后创建了DAO
* 4月30日：DAO众筹推出<<\[17]>>
* 5月27日：DAO众筹结束
* 6月9日：发现了潜在的递归调用错误，并认为它会影响跟踪用户余额的许多Solidity合约<<\[2]>>
* 6月12日：Stephen Tual宣布DAO资金没有风险<<\[3]>>
* 6月17日：DAO被利用，发现的bug的一个变种（称为“重新进入的bug”）被用来开始耗尽资金; 最终攫取了约30％的资金。<<\[6]>>
* 6月21日：RHG宣布它已经确保了存储在DAO中的其他\~70％的以太网。<<\[5]>>
* 6月24日：通过Geth和Parity客户通过选择加入信号宣布软叉投票。这旨在暂时扣留资金，直到社区可以更好地决定做什么。<<\[7]>>
* 6月28日：软叉中发现了一个漏洞，它已被废弃。<<\[9]>>
* 6月28日至7月15日：用户辩论是否硬分叉。大多数争论发生在/r/ethereum subreddit上。
* 7月15日：DAO Hard Fork被提议撤销DAO攻击。<<\[8]>>
* 7月15日：对carbonvote进行投票以决定DAO Hard Fork是否选择加入（默认情况下不分叉）或选择退出（默认为fork）。<<\[10]>>
* 7月16日：以太供应总票数的5.5％，约80％的选票（约占总供应量的4.5％）是选择退出硬分叉。支持投票的四分之一来自一个地址。<<\[11]>> <<\[12]>>
* 7月20日：硬分叉发生在1,920,000块。<<\[13]>> <<\[14]>>
* 7月20日：反对DAO Hard Fork的人继续运行旧的非硬分叉客户端软件。这会导致在两个链上重放交易的问题。<<\[18]>>
* 7月24日：Poloniex在股票代码ETC下列出原始的以太坊链; 这是第一次交换。<<\[15]>>
* 8月10日：RHG将290万回收的ETC转移至Poloniex，以便在Bity SA的建议下将其转换为ETH。RHG总持有量的14％从ETC转换为ETH和其他加密货币。Poloniex冻结了另外86％的沉积ETH。<<\[19]>>
* 8月30日：冻结的资金由Poloniex发送回RHG。然后RHG在ETC链上设立退款合约。<<\[20]>> <<\[21]>>
* 12月11日：IOHK的ETC开发团队组建。由以太坊创始成员Charles Hoskinson领导。
* 2017年1月13日：更新ETC网络以解决交易重播问题。这两个链现在在功能上是分开的。<<\[22]>>
* 2月20日：ETCDEVTeam表格。早期ETC开发人员Igor Artamonov（splix）领导。

#### 以太坊和以太坊经典 <a href="#user-content-eth_etc_differences" id="user-content-eth_etc_differences"></a>

虽然最初的分裂以DAO为中心，但以太坊和以太坊经典现在是独立的项目。完整的差异是不断发展的，而且过于广泛而无法在本章涵盖，值得注意的是，这些链条在核心发展和社区结构方面确实存在显着差异。

#### 技术差异 <a href="#user-content-eth_etc_differences_technical" id="user-content-eth_etc_differences_technical"></a>

**EVM**

对于大多数部分（截至2018年4月），两个网络保持高度兼容。为一条链生成的合约代码在另一条链上按预期运行。尽管EVM操作系统的差异很小（参见EIPs： [140](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-140.md), [145](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-145.md), 和[214](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-214.md)）

**核心网络开发**

所有区块链最终都有很多用户和贡献者。但是，由于开发此类软件所需的专业知识，核心网络开发（运行网络的代码）通常由分散的小组完成。因此，这些小组生成的代码与实际运行网络的代码密切相关。

| Ethereum    | Ethereum Classic   |
| ----------- | ------------------ |
| 以太坊基金会和志愿者。 | ETCDEV, IOHK, 和志愿者 |

#### 意识形态差异 <a href="#user-content-eth_etc_differences_ideological" id="user-content-eth_etc_differences_ideological"></a>

以太坊和以太坊经典之间最大的物质差异之一是意识形态，它以两种主要方式表现出来：不变性和社区结构。

**不变性**

在区块链的背景下，不变性指的是区块链历史的保存。

| Ethereum                                                 | Ethereum Classic                                           |
| -------------------------------------------------------- | ---------------------------------------------------------- |
| 遵循一种俗称“治理”的哲学。这种理念允许参与者以不同程度的代表性投票，在某些情况下（例如DAO攻击）改变区块链。 | 遵循一种理念，即一旦数据出现在区块链上，就不能被其他人修改。这是与比特币，Litecoin和其他加密货币共享的理念。 |

**社区结构**

虽然区块链旨在分散，但它们周围的世界大部分都是集中的。以太坊和以太坊经典以不同的方式处理这一现实。

| Ethereum                                                                                                                    | Ethereum Classic                                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_以太坊基金会所有：/r/ethereum Subreddit, ethereum.org 网站, 论坛, GitHub (ethereum), Twitter (@ethereum), Facebook, 和 Google+ account. | \_由单独的实体所有：/r/ethereumclassic Subreddit, the ethereumclassic.org 网站, 论坛, GitHubs (ethereumproject, ethereumclassic, etcdevteam, iohk, ethereumcommonwealth), Twitter (@eth\_classic), Telegrams, 和 Discord. |

#### 着名的以太坊分叉的时间表 <a href="#user-content-other_ethereum_forks" id="user-content-other_ethereum_forks"></a>

在以太坊也发生了其他几个分叉。其中一些是硬分叉，因为它们直接从预先存在的以太坊网络中分离出来。其他是软分叉：它们使用以太坊的客户端/节点软件，但运行完全独立的网络，没有与以太坊共享的任何历史记录。在以太坊的生活中可能会有更多的分叉。

还有一些其他项目声称是以太坊分叉，但实际上是基于ERC20 token并在以太坊网络上运行。其中两个例子是EtherBTC（ETHB）和以太坊修改（EMOD）。这些不是传统意义上的分叉，有时也可称为空投。

* Expanse是以太坊区块链的第一个获得牵引力的分支。它是在2015年9月7日通过比特币谈话论坛宣布的。实际的分叉发生在一周后的2015年9月14日，块高度为800,000。它最初由Christopher Franko和James Clayton创立。他们的愿景是创建一个先进的链：“身份，治理，慈善，商业和公平”。
* EthereumFog（ETF）于2017年12月14日推出，分块高度为4730660。他们的目标是通过专注于雾计算和分散存储来开发“世界分散雾计算”。关于这实际上会带来什么的信息仍然很少。
* EtherZero（ETZ）于2018年1月19日发布，块高4936270，块高4936270。其值得注意的创新是引入了masternode架构并取消了智能合约的交易费用，以实现更广泛的DAPP。以太网社区的一些著名成员MyEtherWallet和MetaMask遭到了一些批评，原因是围绕开发缺乏明确性以及对可能的网络钓鱼的一些指责。
* EtherInc（ETI）于2018年2月13日发布，高度为5078585，重点是建立分散的组织。他们还宣布减少封锁时间，增加矿工奖励，取消叔叔奖励并设置可开采硬币的上限。它们使用与以太坊相同的私钥，并实施了重放保护，以保护原始非重制链上的ether。

#### 参考 <a href="#usercontent-can-kao" id="usercontent-can-kao"></a>

* \[\[\[1]]] [https://www.economist.com/news/finance-and-economics/21699159-new-automated-investment-fund-has-attracted-stacks-digital-money-dao](https://www.economist.com/news/finance-and-economics/21699159-new-automated-investment-fund-has-attracted-stacks-digital-money-dao)
* \[\[\[2]]] [http://vessenes.com/more-ethereum-attacks-race-to-empty-is-the-real-deal/](http://vessenes.com/more-ethereum-attacks-race-to-empty-is-the-real-deal/)
* \[\[\[3]]] [https://blog.slock.it/no-dao-funds-at-risk-following-the-ethereum-smart-contract-recursive-call-bug-discovery-29f482d348b](https://blog.slock.it/no-dao-funds-at-risk-following-the-ethereum-smart-contract-recursive-call-bug-discovery-29f482d348b)
* \[\[\[4]]] [http://hackingdistributed.com/2016/06/18/analysis-of-the-dao-exploit](http://hackingdistributed.com/2016/06/18/analysis-of-the-dao-exploit)
* \[\[\[5]]] [https://www.reddit.com/r/ethereum/comments/4p7mhc/update\_on\_the\_white\_hat\_attack/](https://www.reddit.com/r/ethereum/comments/4p7mhc/update\_on\_the\_white\_hat\_attack/)
* \[\[\[6]]] [http://hackingdistributed.com/2016/06/18/analysis-of-the-dao-exploit/](http://hackingdistributed.com/2016/06/18/analysis-of-the-dao-exploit/)
* \[\[\[7]]] [https://blog.ethereum.org/2016/06/24/dao-wars-youre-voice-soft-fork-dilemma/](https://blog.ethereum.org/2016/06/24/dao-wars-youre-voice-soft-fork-dilemma/)
* \[\[\[8]]] [https://blog.slock.it/hard-fork-specification-24b889e70703](https://blog.slock.it/hard-fork-specification-24b889e70703)
* \[\[\[9]]] [https://blog.ethereum.org/2016/06/28/security-alert-dos-vulnerability-in-the-soft-fork/](https://blog.ethereum.org/2016/06/28/security-alert-dos-vulnerability-in-the-soft-fork/)
* \[\[\[10]]] [https://blog.ethereum.org/2016/07/15/to-fork-or-not-to-fork/](https://blog.ethereum.org/2016/07/15/to-fork-or-not-to-fork/)
* \[\[\[11]]] [https://etherscan.io/block/1894000](https://etherscan.io/block/1894000)
* \[\[\[12]]] [https://elaineou.com/2016/07/18/stick-a-fork-in-ethereum/](https://elaineou.com/2016/07/18/stick-a-fork-in-ethereum/)
* \[\[\[13]]] [https://etherscan.io/block/1920000](https://etherscan.io/block/1920000)
* \[\[\[14]]] [https://blog.ethereum.org/2016/07/20/hard-fork-completed/](https://blog.ethereum.org/2016/07/20/hard-fork-completed/)
* \[\[\[15]]] [https://twitter.com/poloniex/status/757068619234803712](https://twitter.com/poloniex/status/757068619234803712)
* \[\[\[16]]] [https://blog.slock.it/deja-vu-dao-smart-contracts-audit-results-d26bc088e32e](https://blog.slock.it/deja-vu-dao-smart-contracts-audit-results-d26bc088e32e)
* \[\[\[17]]] [https://blog.slock.it/the-dao-creation-is-now-live-2270fd23affc](https://blog.slock.it/the-dao-creation-is-now-live-2270fd23affc)
* \[\[\[18]]] [https://gastracker.io/block/0x94365e3a8c0b35089c1d1195081fe7489b528a84b22199c916180db8b28ade7f](https://gastracker.io/block/0x94365e3a8c0b35089c1d1195081fe7489b528a84b22199c916180db8b28ade7f)
* \[\[\[19]]] [https://bitcoinmagazine.com/articles/millions-of-dollars-worth-of-etc-may-soon-be-dumped-on-the-market-1472567361/](https://bitcoinmagazine.com/articles/millions-of-dollars-worth-of-etc-may-soon-be-dumped-on-the-market-1472567361/)
* \[\[\[20]]] [https://medium.com/@jackfru1t/the-robin-hood-group-and-etc-bdc6a0c111c3](https://medium.com/@jackfru1t/the-robin-hood-group-and-etc-bdc6a0c111c3)
* \[\[\[21]]] [https://www.reddit.com/r/EthereumClassic/comments/4xauca/follow\_up\_statement\_on\_the\_etc\_salvaged\_from/](https://www.reddit.com/r/EthereumClassic/comments/4xauca/follow\_up\_statement\_on\_the\_etc\_salvaged\_from/)
* \[\[\[22]]] [https://www.reddit.com/r/EthereumClassic/comments/5nt4qm/diehard\_etc\_protocol\_upgrade\_successful\_nethash/](https://www.reddit.com/r/EthereumClassic/comments/5nt4qm/diehard\_etc\_protocol\_upgrade\_successful\_nethash/)
* \[\[\[23]]] [https://web.archive.org/web/20160429141714/https://daohub.org/explainer.html/](https://web.archive.org/web/20160429141714/https://daohub.org/explainer.html/)
* \[\[\[24]]] [https://ethereumclassic.github.io/blog/2016-12-12-TeamGrothendieck/](https://ethereumclassic.github.io/blog/2016-12-12-TeamGrothendieck/)

全书完结

