# 术语

账户 Account

包含地址、余额、随机数以及可选存储和代码的对象。账户可以是合约账户或外部拥有账户（EOA，externally owned account）.

地址 Address

一般来说，这代表一个 EOA 或合约，它可以在区块链上接收（目标地址）或发送（源地址）交易。更具体地说，它是 ECDSA 公钥的 Keccak 散列的最右边的160位，表现为16进制的40个字符长度，在前面加上“0x”字符。

断言 Assert

在 Solidity 中，assert(false) 编译为 **0xfe**, 是一个无效的操作码，用尽所有剩余的燃气（Gas），并恢复所有更改。 当 assert() 语句失败时，说明发生了严重的错误或异常，你必须修复你的代码。 你应该使用 assert 来避免永远不应该发生的条件。

大端序 Big-endian

一种数值的位置表示形式，最高有效位放在最前面。对应小端序（little-endian），最低有效位在前。

比特币改进提议 BIPs

比特币改进提议，Bitcoin Improvement Proposals。比特币社区成员提交的一组提案，旨在改进比特币。例如，BIP-21是改进比特币统一资源标识符（URI）方案的建议。

区块 Block

区块是关于所包含的交易的所需信息（区块头）的集合，以及称为ommer的一组其他区块头。它被矿工添加到以太坊网络中。

区块链 Blockchain

由工作证明系统验证的一系列区块，每个区块都连接到它的前任，一直到创世区块。这与比特币协议不同，因为它没有块大小限制；它改为使用不同的燃气限制。

拜占庭分叉 Byzantium Fork

拜占庭是大都会（ Metropolis ）发展阶段的两大分叉之一。它包括 EIP-649：大都会难度炸弹延迟和区块奖励减少，其中冰河时代（见下文）延迟1年，而区块奖励从5个以太坊减至3个以太坊。

编译 Compiling

将高级编程语言（例如 Solidity）编写的代码转换为低级语言（例如 EVM 字节码）

共识 Consensus

大量节点，通常是网络上的大多数节点，在其本地验证的最佳区块链中都有相同的区块的情况。 不要与共识规则混淆。

共识规则 Consensus rules

完整节点为了与其他节点保持一致，遵循的区块验证规则。不要与共识混淆。

君士坦丁堡 Constantinople

大都会阶段的第二部分，2018年中期的计划。预计将包括切换到混合工作证明/权益证明共识算法，以及其他变更。

合约账户 Contract account

包含代码的账户，每当它从另一个账户（EOA 或合约）收到交易时执行。

合约创建交易 Contract creation transaction

一个特殊的交易，以“零地址”作为收件人，用于注册合约并将其记录在以太坊区块链中（请参阅“零地址”）。

去中心化自治组织 DAO

去中心化自治组织 Decentralised Autonomous Organization. 没有层级管理的公司和其他组织。也可能是指2016年4月30日发布的名为“The DAO”的合约，该合约于2016年6月遭到黑客攻击，最终在第1,192,000个区块激起了硬分叉（代号 DAO），恢复了被攻击的 DAO 合约，并导致了以太坊和以太坊经典两个竞争系统。

去中心化应用 DApp

去中心化应用 Decentralised Application. 狭义上，它至少是智能合约和 web 用户界面。更广泛地说，DApp 是一个基于开放式，分散式，点对点基础架构服务的 Web 应用程序。另外，许多 DApp 包括去中心化存储和/或消息协议和平台。

契约 Deed

ERC721提案中引入了不可替代的标记标准。与ERC20代币不同，契约证明了所有权并且不可互换，虽然它们还未在任何管辖区都被认可为合法文件，至少目前不是。

难度 Difficulty

网络范围的设置，控制产生工作量证明需要多少计算。

数字签名 Digital signature

数字签名算法是一个过程，用户可以使用私钥为文档生成称为“签名”的短字符串数据，以便具有签名，文档，和相应公钥的任何人，都可以验证（1 ）该文件由该特定私钥的所有者“签名”，以及（2）该文件在签署后未被更改。

椭圆曲线数字签名算法 ECDSA

椭圆曲线数字签名算法（ Elliptic Curve Digital Signature Algorithm，ECDSA ）是以太坊用来确保资金只能由合法所有者使用的加密算法。

以太坊改进建议 EIP

以太坊改进建议，Ethereum Improvement Proposals，描述以太坊平台的建议标准。 EIP 是向以太坊社区提供信息的设计文档，描述新的功能，或处理过程，或环境。有关更多信息，请参见 [https://github.com/ethereum/EIPs（另请参见下面的](https://github.com/ethereum/EIPs%EF%BC%88%E5%8F%A6%E8%AF%B7%E5%8F%82%E8%A7%81%E4%B8%8B%E9%9D%A2%E7%9A%84) ERC 定义）。

熵 Entropy

在密码学领域，表示可预测性的缺乏或随机性水平。在生成秘密信息（如主私钥）时，算法通常依赖高熵源来确保输出不可预测。

以太坊名称服务 ENS

以太坊名称服务，Ethereum Name Service. 更多信息，参见 [https://github.com/ethereum/ens/](https://github.com/ethereum/ens/).

外部拥有账户 EOA

外部拥有账户，Externally Owned Account. 由或为以太坊的真人用户创建的账户。

以太坊注释请求 ERC

以太坊注释请求 Ethereum Request for Comments. 一些 EIP 被标记为 ERC，表示试图定义以太坊使用的特定标准的建议。

Ethash

以太坊1.0的工作量证明算法。更多信息，参见 [https://github.com/ethereum/wiki/wiki/Ethash](https://github.com/ethereum/wiki/wiki/Ethash).

以太 Ether

以太 Ether，是以太坊生态系统中使用的本地货币，在执行智能合约时承担燃气费用。它的符合是 Ξ, 极客用的大写 Xi 字符.

Event

事件允许EVM日志工具的使用，后者可以用来在DApp的用户界面中调用JavaScript回调来监听这些事件。更多信息，参见 [http://solidity.readthedocs.io/en/develop/contracts.html#events。](http://solidity.readthedocs.io/en/develop/contracts.html#events%E3%80%82)

以太坊虚拟机 EVM

Ethereum Virtual Machine, 基于栈的，执行字节码的虚拟机。在以太坊中，执行模型指定了系统状态如何在给定一系列字节码指令和少量环境数据的情况下发生改变。 这是通过虚拟状态机的正式模型指定的。

EVM汇编语言 EVM Assembly Language

字节码的人类可读形式。

后备方法 Fallback function

默认的方法，当缺少数据或声明的方法名时执行。

水龙头 Faucet

一个网站，为想要在testnet上做测试的开发人员提供免费测试以太形式的奖励。

前沿 Frontier

以太坊的试验开发阶段，从2015年7月至2016年3月。

Ganache

私有以太坊区块链，你可以在上面进行测试，执行命令，在控制区块链如何运作时检查状态。

燃气 Gas

以太坊用于执行智能合约的虚拟燃料。以太坊虚拟机使用会计机制来衡量天然气的消耗量并限制计算资源的消耗。参见“图灵完备”。 燃气是执行智能合约的每条指令产生的计算单位。燃气与以太加密货币挂钩。燃气类似于蜂窝网络上的通话时间。因此，以法定货币进行交易的价格是 gas **（ETH /gas）**（法定货币/ETH）。

燃气限制 Gas limit

在谈论区块时，它们也有一个名为燃气限制的区域。它定义了整个区块中所有交易允许消耗的最大燃气量。

创世区块 Genesis block

区块链中的第一个块，用来初始化特定的网络和加密数字货币。

Geth

Go语言的以太坊。Go编写的最突出的以太坊协议实现之一。

硬分叉 Hard fork

硬分叉也称为硬分叉更改，是区块链中的一种永久性分歧，通常发生在非升级节点无法验证升级节点创建的遵循新共识规则的区块时。不要与分叉，软分叉，软件分叉或Git分叉混淆。

哈希值 Hash

通过哈希方法为可变大小的数据生成的固定长度的指纹。

分层确定钱包 HD wallet

使用分层确定密钥生成和传输协议的钱包（BIP32）。

分层确定钱包种子 HD wallet seed

HD钱包种子或根种子是一个可能很短的值，用作生成HD钱包的主私钥和主链码的种子。钱包种子可以用助记词表示，使人们更容易复制，备份和恢复私钥。

家园 Homestead

以太坊的第二个发展阶段，于2016年3月在1,150,000区块启动。

冰河时代 Ice Age

以太坊在200,000区块的硬分叉，提出难度指数级增长（又名难度炸弹），引发了到权益证明Proof-of-Stake的过渡。

集成开发环境 IDE (Integrated Development Environment)

集成的用户界面，结合了代码编辑器、编译器、运行时和调试器。

不可变的部署代码问题 Immutable Deployed Code Problem

一旦部署了契约(或库)的代码，它就成为不可变的。修复可能的bug并添加新特性是软件开发周期的关键。这对智能合约开发来说是一个挑战。

互换客户端地址协议 Inter exchange Client Address Protocol (ICAP)

以太坊地址编码，与国际银行帐号（IBAN）编码部分兼容，为以太坊地址提供多样的，校验和的，可互操作的编码。 ICAP地址可以编码以太坊地址或通过以太坊名称注册表注册的常用名称。他们总是以XE开始。其目的是引入一个新的IBAN国家代码：XE，X表示"extended"， 加上以太坊的E，用于非管辖货币（例如XBT，XRP，XCP）。

内部交易（又称“消息”）Internal transaction (also "message")

从一个合约地址发送到另一个合约地址或EOA的交易。

Keccak256

以太坊使用的加密哈希方法。虽然在早期 Ethereum 代码中写作 SHA-3，但是由于在 2015 年 8 月 SHA-3 完成标准化时，NIST 调整了填充算法，所以 Keccak256 不同于标准的 NIST-SHA3。Ethereum 也在后续的代码中开始将 SHA-3 的写法替换成 Keccak256 。

密钥推导方法 Key Derivation Function (KDF)

也称为密码扩展算法，它被keystore格式使用，以防止对密码加密的暴力破解，字典或彩虹表攻击。它重复对密码进行哈希。

Keystore 文件

JSON 编码的文件，包含一个（随机生成的）私钥，被一个密码加密，以提供额外的安全性。

LevelDB

LevelDB是一种开源的磁盘键值存储系统。LevelDB是轻量的，单一目标的持久化库，支持许多平台。

库 Library

以太坊中的库，是特殊类型的合约，没有用于支付的方法，没有后备方法，没有数据存储。所以它不能接收或存储以太，或存储数据。库用作之前部署的代码，其他合约可以调用只读计算。

轻量级客户端 Lightweight client

轻量级客户端是一个以太坊客户端，它不存储区块链的本地副本，也不验证块和事务。它提供了钱包的功能，可以创建和广播交易。

消息 Message

内部交易，从未被序列化，只在EVM中发送。

大都会阶段 Metropolis Stage

大都会是以太坊的第三个开发阶段，在2017年10月启动。

METoken

Mastering Ethereum Token. 本书中用于演示的 ERC20 代币。

矿工 Miner

通过重复哈希计算，为新的区块寻找有效的工作量证明的网络节点。

Mist

Mist是以太坊基金会创建的第一个以太坊浏览器。它还包含一个基于浏览器的钱包，这是ERC20令牌标准的首次实施（Fabian Vogelsteller，ERC20的作者也是Mist的主要开发人员）。Mist也是第一个引入camelCase校验码（EIP-155）的钱包。Mist运行完整节点，提供完整的DApp浏览器，支持基于Swarm的存储和ENS地址

网络 Network

将交易和区块传播到每个以太坊节点（网络参与者）的对等网络。

节点 Node

参与到对等网络的软件客户端。

随机数 Nonce

密码学中，随机数指代只可以用一次的数值。在以太坊中用到两类随机数。

* 账户随机数 - 这只是一个账户的交易计数。
* 工作量证明随机数- 用于获得工作证明的区块中的随机值（取决于当时的难度）。

Ommer

祖父节点的子节点，但它本身并不是父节点。当矿工找到一个有效的区块时，另一个矿工可能已经发布了一个竞争的区块，并添加到区块链顶部。像比特币一样，以太坊中的孤儿区块可以被新的区块作为ommers包含，并获得部分奖励。术语 "ommer" 是对父节点的兄弟姐妹节点的性别中立的称呼，但也可以表示为“叔叔”。

Parity

以太坊客户端软件最突出的支持共同操作（多重签名）的实现之一。

权益证明 Proof-of-Stake (PoS)

权益证明是加密货币区块链协议旨在实现分布式共识的一种方法。权益证明要求用户证明一定数量的加密货币（网络中的“股份”）的所有权，以便能够参与交易验证。

工作量证明 Proof-of-Work (PoW)

一份需要大量计算才能找到的数据（证明）。在以太坊，矿工必须找到符合网络难度目标的 Ethash 算法的数字解决方案。

收据 Receipt

以太坊客户端返回的数据，表示特定交易的结果，包括交易的哈希值，其区块编号，使用的燃气量，以及在部署智能合约时的合约地址。

重入攻击 Re-entrancy Attack

当攻击者合约（Attacker contracts）调用受害者合约（Victim contracts）的方法时，可以重复这种攻击。让我们称它为victim.withdraw()，在对该合约函数的原始调用完成之前，再次调用victim.withdraw()方法，持续递归调用它自己。 递归调用可以通过攻击者合约的后备方法实现。 攻击者必须执行的唯一技巧是在用完燃气之前中断递归调用，并避免盗用的以太被还原。

Require

在Solidity中，require（false）编译为 **0xfd**，它是 **REVERT** 操作码。REVERT指令提供了一种停止执行和恢复状态更改的方式，不消耗所有提供的燃气并且能够返回原因。 应使用require函数来确保满足有效条件，如输入或合同状态变量，或者验证调用外部合约的返回值。 在\*拜占庭\*网络升级之前，有两种实际的方式来还原交易：耗尽燃气或执行无效指令。这两个选项都消耗了所有剩余的气体。 在\*Byzantium\*网络升级之前，在\*黄皮书\*中无法找到此操作码，并且因为该操作码没有规范，所以当EVM执行到它时，会抛出一个 _invalid opcode error_。

还原 Revert

当需要处理与 [require()](broken-reference) 相同的情况，但使用更复杂的逻辑时，使用 revert()。 例如，如果你的代码有一些嵌套的 if/else 逻辑流程，你会发现使用 [require()](broken-reference) 而不是require（）是合理的。

奖励 Reward

Ether（ETH）的数量，包含在每个新区块中的金额作为网络对找到工作证明解决方案的矿工的奖励。

递归长度前缀 Recursive Length Prefix (RLP)

RLP 是一种编码标准，由以太坊开发人员设计用来编码和序列化任意复杂度和长度的对象（数据结构）。

中本聪 Satoshi Nakamoto

Satoshi Nakamoto 是设计比特币及其原始实现 Bitcoin Core 的个人或团队的名字。作为实现的一部分，他们也设计了第一个区块链。在这个过程中，他们是第一个解决数字货币的双重支付问题的。他们的真实身份至今仍是个谜。

Vitalik Buterin

Vitalik Buterin 是俄国-加拿大的程序员和作家，以太坊和 Bitcoin 杂志的联合创始人。

Gavin Wood

Gavin Wood 是英国的程序员，以太坊的联合创始人和前 CTO。在2014年8月他提出了Solidity，用于编写智能合约的面向合约的编程语言。

密钥（私钥） Secret key (aka private key)

允许以太坊用户通过创建数字签名（参见公钥，地址，ECDSA）证明账户或合约的所有权的加密数字。

SHA

安全哈希算法 Secure Hash Algorithm，SHA 是美国国家标准与技术研究院（NIST）发布的一系列加密哈希函数。

SELFDESTRUCT 操作码

只要整个网络存在，智能合同就会存在并可执行。如果它们被编程为自毁的或使用委托调用（delegatecall）或调用代码（callcode）执行该操作，它们将从区块链中消失。 一旦执行自毁操作，存储在合同地址处的剩余Ether将被发送到另一个地址，并将存储和代码从状态中移除。 尽管这是预期的行为，但自毁合同的修剪可能或不会被以太坊客户实施。 SELFDESTRUCT 之前称作 SUICIDE, 在EIP6中, SUICIDE 重命名为 SELFDESTRUCT。

宁静 Serenity

以太坊第四个也是最后一个开发阶段。宁静还没有计划发布的日期。

Serpent

语法类似于 Python 的过程式（命令式）编程语言。也可以用来编写函数式（声明式）代码，尽管它不是完全没有副作用的。首先由 Vitalik Buterin 创建。

智能合约 Smart Contract

在以太坊的计算框架上执行的程序。

Solidity

过程式（命令式）编程语言，语法类似于 Javascript, C++ 或 Java。以太坊智能合约最流行和最常使用的语言。由 Gavin Wood（本书的联合作者）首先创造

Solidity inline assembly

内联汇编 Solidity 中包含的使用 EVM 汇编（EVM 代码的人类可读形式）的代码。内联汇编试图解决手动编写汇编时遇到的固有难题和其他问题。

Spurious Dragon

在＃2,675,00块的硬分叉，来解决更多的拒绝服务攻击向量，以及另一种状态清除。还有转播攻击保护机制。

Swarm

一种去中心化（P2P）的存储网络。与 Web3 和 Whisper 共同使用来构建 DApps。

Tangerine Whistle

在 #2,463,00 块的硬分叉，改变了某些 I/O 密集操作的燃气计算方式，并从拒绝服务攻击中清除累积状态，这种攻击利用了这些操作的低燃气成本。

测试网 Testnet

一个测试网络（简称 testnet），用于模拟以太网主要网络的行为。

交易 Transaction

由原始帐户签署的提交到以太坊区块链的数据，并以特定地址为目标。交易包含元数据，例如交易的燃气限额。

Truffle

一个最常用的以太坊开发框架。包含一些 NodeJS 包，可以使用 Node Package Manager (NPM) 安装。

图灵完备 Turing Complete

在计算理论中，如果数据操纵规则（如计算机的指令集，程序设计语言或细胞自动机）可用于模拟任何图灵机，则它被称为图灵完备或计算上通用的。这个概念是以英国数学家和计算机科学家阿兰图灵命名的。

Vyper

一种高级编程语言，类似 Serpent，有 Python 式的语法，旨在接近纯函数式语言。由 Vitalik Buterin 首先创造。

钱包 Wallet

拥有你的所有密钥的软件。作为访问和控制以太坊账户并与智能合约交互的界面。请注意，密钥不需要存储在你的钱包中，并且可以从脱机存储（例如 USB 闪存驱动器或纸张）中检索以提高安全性。尽管名字为钱包，但它从不存储实际的硬币或代币。

Web3

web 的第三个版本。有 Gavin Wood 首先提出，Web3 代表了 Web 应用程序的新愿景和焦点：从集中拥有和管理的应用程序到基于去中心化协议的应用程序。

Wei

以太的最小单位，1018 wei = 1 ether.

Whisper

一种去中心化（P2P）消息系统。与 Web3 和 Swarm 一起使用来构建 DApps。

零地址 Zero address

特殊的以太坊地址，全部是由 `0` 组成（即 `0x0000000000000000000000000000000000000000`)，被指定为创建一个智能合约所发起的交易（Transaction）的目标地址（即 `to` 参数的值）。
