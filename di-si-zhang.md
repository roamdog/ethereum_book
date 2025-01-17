# 第四章

### 以太坊测试网（Testnets） <a href="#user-content-testnets" id="user-content-testnets"></a>

#### 什么是测试网？ <a href="#usercontent-shi-mo-shi-ce-shi-wang" id="usercontent-shi-mo-shi-ce-shi-wang"></a>

测试网络（简称testnet）用于模拟以太网主网的行为。有一些公开的测试网络可以替代以太坊区块链。这些网络上的货币毫无价值，但它们仍然很有用，因为合约和协议变更的功能可以在不中断以太网主网或使用真实货币的情况下进行测试。当主网（简称mainnet）即将包含对以太坊协议的任何重大改变时，其测试主要在这些测试网络上完成。这些测试网络也被大量开发人员用于在部署到主网之前测试应用程序。

#### 使用 Testnets <a href="#usercontent-shi-yong-testnets" id="usercontent-shi-yong-testnets"></a>

你可以连接到公共可用的测试网络或创建你自己的私人测试网络。首先，让我们使用公共测试网来更简单地起步。要使用公共测试网络，需要一些测试网络以及到该网络的连接。对于testnet ether，使用“faucet”，faucet缓慢地分配测试ether，向任何询问的人“滴送”少量ether。要连接到一个测试网络，你需要一个以太坊客户端，完整的客户端，比如geth，或者完整的客户端的网关，比如MetaMask。

#### 获取测试以太网 <a href="#usercontent-huo-qu-ce-shi-yi-tai-wang" id="usercontent-huo-qu-ce-shi-yi-tai-wang"></a>

由于测试网不以真正的金钱运作，矿工保护测试网的动机很弱。因此，测试网必须保护自己免受滥用和攻击。因此，为这些测试网创建了水龙头，以受控的方式向开发人员分发免费的测试ether（大多数faucet每隔几秒左右"滴注"ether）。这种以太网的受控分配可防止用户滥用链，因为提供有限的ether供应可防止他们向链中写入过多内容或执行太多交易。另外，一些testnets已经实施了认证证明（Proof of Authentication）方案，使用faucet需要具有适当社交媒体网站的认证的凭证。

#### 连接到Testnets <a href="#usercontent-lian-jie-dao-testnets" id="usercontent-lian-jie-dao-testnets"></a>

**Metamask**

Metamask完全支持Ropsten，Kovan和Rinkeby测试网，但也可以连接到其他测试网和本地网。在Metamask中，只需单击“main network”下拉菜单，即可切换网络。MetaMask还提供了一个“buy”测试ether的选项，该选项将你引导至你可以请求免费测试以太网的faucet。如果使用Ropsten测试网，则可以从Ropsten测试faucet服务中获取ether。你可以从此页面访问此faucet。它需要Metamask扩展才能工作。[https://faucet.metamask.io/](https://faucet.metamask.io)

**Infura**

当MetaMask连接到测试网络时，它使用Infura服务提供商来访问JSON-RPC接口。Infura诞生的目的是为ConsenSys内部项目提供稳定可靠的RPC访问。除了JSON-RPC API之外，Infura还提供REST（表述性状态转移）API，IPFS（星际文件系统，即去中心化存储）API和Websockets（即流式传输）API。

Infura为Ethereum主网，Ropsten，Kovan，Rinkeby和INFURAnet（用于Infura的定制测试网络）提供网关API。

要通过MetaMask使用Infura进行较低级别的活动，你不需要账户。要直接使用API，你需要注册一个账户并使用Infura提供的API密钥。

有关Infura的更多信息，请访问：

**Remix集成开发环境（IDE）**

Remix IDE可用于在主网和测试网上部署和交互智能合约，包括Ropsten，Rinkeby和Kovan（Web3提供者使用Infura地址和API密钥或通过Injected Web3使用MetaMask中选择的网络）和Ganache（ Web3提供端点http://localhost:8545）

**Geth**

Geth本身支持Ropsten和Rinkeby网络。要连接到Ropsten网络，请使用命令行参数：

这将开始同步Ropsten区块链。名为 testnet 的新目录将在你的主Ethereum数据目录中创建。一个 keystore 目录将在 testnet 内部创建，并将存储你的testnet帐户的私钥。在撰写本文时，Ropsten区块链比以太坊主区块链小得多：大约14GB的数据。由于测试网需要的资源较少，因此首先在测试网上设置并测试你的代码会更简单。

与testnet的交互与mainnet类似。你可以使用控制台启动Geth testnet，方法是运行：

这使得执行操作成为可能，例如开设新账户，检查余额，检查其他以太坊地址的余额等。 在Geth控制台之外运行时，只需将\`--testnet\`参数添加到命令行指令中，就可以执行类似于在主网上执行的操作。作为列举所有可用的testnet帐户及其地址的示例，请运行：

```
geth --testnet account list
```

| Tip | 虽然小得多，但测试网仍需要一些时间才能完全同步。 |
| --- | ------------------------ |

你可以通过在geth交互式控制台中运行以下命令来检查geth是否已完成同步测试网络：

```
eth.getBlock("latest").number
```

同样，要连接到Rinkeby测试网络，请使用命令行参数：

**Parity**

Parity客户端支持Ropsten和Kovan测试网络。你可以用+chain+参数选择你要连接的网络。例如，要同步Ropsten测试网络：

同样，要同步Kovan测试网络，请使用：

### 深入以太坊Testnets <a href="#usercontent-shen-ru-yi-tai-fang-testnets" id="usercontent-shen-ru-yi-tai-fang-testnets"></a>

在这个阶段你可能会想：“我明白我为什么要使用测试网络，但为什么会有这么多呢？”

#### 工作量证明（挖矿）Proof-of-Work (Mining) 与 权威证明（联合签名）Proof-of-Authority (Federated Signing) <a href="#usercontent-gong-zuo-liang-zheng-ming-wa-kuang-proofofworkmining-yu-quan-wei-zheng-ming-lian-he-qian" id="usercontent-gong-zuo-liang-zheng-ming-wa-kuang-proofofworkmining-yu-quan-wei-zheng-ming-lian-he-qian"></a>

#### Morden（原始测试网） <a href="#usercontentmorden-yuan-shi-ce-shi-wang" id="usercontentmorden-yuan-shi-ce-shi-wang"></a>

#### Rinkeby <a href="#user-content-rinkeby" id="user-content-rinkeby"></a>

#### Kovan <a href="#user-content-kovan" id="user-content-kovan"></a>

### 以太坊经典Testnets <a href="#usercontent-yi-tai-fang-jing-dian-testnets" id="usercontent-yi-tai-fang-jing-dian-testnets"></a>

**Morden**

以太坊经典目前运行着Morden测试网的一个变体，与以太坊经典活跃网络保持功能相同。你可以通过gastracker RPC或者为\`geth\`或\`parity\`提供一个标志来连接它.

**Geth flag:** `geth --chain=morden`

**Parity flag:** `parity --chain=classic-testnet`

#### 以太坊测试网的历史 <a href="#usercontent-yi-tai-fang-ce-shi-wang-de-li-shi" id="usercontent-yi-tai-fang-ce-shi-wang-de-li-shi"></a>

Olympic, Morden to Ropsten, Kovan, Rinkeby

Olympic testnet (Network ID: 0) 是Frontier首个公共测试网（简称Ethereum 0.9）。它于2015年初推出，2015年中期被Morden取代时弃用。

Ethereum’s Morden testnet (Network ID: 2) 与Frontier一起发布，从2015年7月开始运行，直到2016年11月不再使用。虽然任何使用以太坊的人都可以创建测试网，但Morden是第一个“官方”公共测试网，取代了Olympic测试网。由于臃肿区块链的长同步时间以及Geth和Parity客户端之间的共识问题，测试网络重新启动并重新生成为Ropsten。

Ropsten (Network ID: 3) 是一个针对Homestead的公共跨客户端测试网，于2016年晚些时候推出，并作为公共测试网顺利运行至2017年2月底。根据Ethereum的核心开发人员PéterSzilágyi的说法，二月的时候，“恶意行为者决定滥用低PoW，并逐步将gas限制提高到90亿（从普通的470万），发送巨大交易损害了整个网络”。Ropsten在2017年3月被恢复。[https://github.com/ethereum/ropsten](https://github.com/ethereum/ropsten)

Kovan (Network ID: 42) 是由Parity的权威证明（PoA）共识算法驱动的Homestead的公共Parity测试网络。该测试网不受垃圾邮件攻击的影响，因为ether供应由可信方控制。这些值得信赖的各方是在Ethereum上积极开发的公司。 尽管看起来这应该是以太坊测试网问题的解决方案，但在以太坊社区内似乎存在关于Kovan测试网的共识问题。[https://github.com/kovan-testnet/proposal](https://github.com/kovan-testnet/proposal)

Rinkeby (Network ID: 4) 是由Ethereum团队于2017年4月开始的Homestead发布的Geth测试网络，并使用PoA共识协议。以斯德哥尔摩的地铁站命名，它几乎不受垃圾邮件攻击的影响（因为以太网供应由受信任方控制）。请参阅EIP 225：[ethereum/EIPs#225](https://github.com/ethereum/EIPs/issues/225)

#### 工作量证明（挖矿）Proof-of-Work (Mining) 与 权威证明（联合签名）Proof-of-Authority (Federated Signing) <a href="#usercontent-gong-zuo-liang-zheng-ming-wa-kuang-proofofworkmining-yu-quan-wei-zheng-ming-lian-he-qian" id="usercontent-gong-zuo-liang-zheng-ming-wa-kuang-proofofworkmining-yu-quan-wei-zheng-ming-lian-he-qian"></a>

Proof-of-Work 是一种协议，必须执行挖矿（昂贵的计算机计算）以在区块链（分布式账本）上创建新的区块（去信任的交易）。 缺点：能源消耗。集中的哈希算力与集中的采矿农场，不是真正的分布式。挖掘新块体所需的大量计算能力对环境有影响。

Proof-of-Authority 是一种协议，它只将造币的负载分配给授权和可信的签名者，他们可以根据自己的判断并随时以发币频率分发新的区块。[ethereum/EIPs#225](https://github.com/ethereum/EIPs/issues/225) 优点：具有最显赫的身份的区块链参与者通过算法选择来验证块来交付交易。

#### 运行本地测试网 <a href="#usercontent-yun-hang-ben-di-ce-shi-wang" id="usercontent-yun-hang-ben-di-ce-shi-wang"></a>

**Ganache: 以太坊开发的个人区块链**

你可以使用Ganache部署合约，开发应用程序并运行测试。它可用作Windows，Mac和Linux的桌面应用程序。

**Ganache CLI: Ganache 作为命令行工具。**

这个工具以前称为“ethereumJS TestRPC”。

```
$ npm install -g ganache-cli
```

让我们开始以太坊区块链协议的节点模拟。 \* \[]检查\`--networkId\`和\`--port\`标志值是否与truffle.js中的配置相匹配 \* \[]检查\`--gasLimit\`标志值是否与[https://ethstats.net上显示的最新主网gas极限（即8000000](https://ethstats.xn--netgas\(8000000-ic7vzx232eb78echc4uft9cov7kbbnfp8aef4j) gas）相匹配，以避免不必要地遇到\`gas’异常。请注意，4000000000的“--gasPrice”代表4 gwei的gas价格。 \* \[]可以输入一个\`--mnemonic’标志值来恢复以前的高清钱包和相关地址

```
$ ganache-cli \
  --networkId=3 \
  --port="8545" \
  --verbose \
  --gasLimit=8000000 \
  --gasPrice=4000000000;
```

