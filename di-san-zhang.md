# 第三章

### 以太坊客户端 <a href="#user-content-ethereum_clients_chapter" id="user-content-ethereum_clients_chapter"></a>

以太坊客户端是实现以太坊规范并通过对等网络与其他以太坊客户端进行通信的软件应用程序。不同的以太坊客户端如果符合参考规范和标准化通信协议，就可以互操作。虽然这些不同的客户端由不同的团队和不同的编程语言实现，但他们都“说”相同的协议并遵循相同的规则。

以太坊是一个\_open source\_项目，源代码可在开放（LGPL v3.0）许可下使用，可免费下载并用于任何目的。开源意味着不仅仅是免费使用。这也意味着以太坊由一个开放的志愿者社区开发，任何人都可以修改。

以太坊由名为“黄皮书”的正式规范定义。 这与比特币相反，比特币没有任何正式的定义。比特币的“规范”是比特币核心的参考实现，以太坊的规范定义在一篇结合了英文和数学的（正式的）规范的论文中。 这个正式的规范，除了各种以太坊改进建议之外，还定义了以太坊客户端的标准行为。随着对以太坊的重大改变，黄皮书会定期更新。

作为以太坊明确的正式规范的结果，以太坊客户端有许多独立开发的，可互操作的软件实现。以太坊在网络上运行的实现方式比任何其他区块链都多。

### 以太坊网络 <a href="#usercontent-yi-tai-fang-wang-luo" id="usercontent-yi-tai-fang-wang-luo"></a>

存在各种基于以太坊的网络，这些网络很大程度上符合以太坊“黄皮书”中定义的正式规范，但它们可能或不能互操作。

在这些以太坊网络中有：Ethereum，Ethereum Classic，Ella，Expanse，Ubiq，Musicoin等等。虽然大多数在协议级别上兼容，但这些网络通常具需要以太坊客户端软件维护人员进行微小更改以支持每个网络的功能或属性。因此，并非以太坊客户端软件的每个版本都可以在每个以太坊区块链上运行。

目前，以六种不同语言编写的以太坊协议有六个主要实现：Go（Geth），Rust（parity），C ++（cpp-ethereum），Python（pyethereum），Scala（mantis）和Java（harmony）。

在本节中，我们将看看两个最常见的客户，Geth和Parity。我们将学习如何使用每个客户端启动一个节点，并探索他们的一些命令行和应用程序编程接口（API）。

#### 我应该运行一个完整的节点吗？ <a href="#user-content-full_node_importance" id="user-content-full_node_importance"></a>

区块链的健康，弹性和抗审查取决于拥有有多少独立运营和地理上分散的完整节点。每个完整节点都可以帮助其他新节点获取块数据以引导其操作，并为运营商提供对所有交易和合约的权威和独立验证。

但是，运行完整的节点会导致硬件资源和带宽的巨大成本。完整的节点必须下载超过80GB的数据（截至2018年4月;取决于客户端）并将其存储在本地硬盘上。随着新的交易和区块的添加，这种数据负担每天都会迅速增加。[完整节点的硬件要求](broken-reference) 中有关于此主题的更多信息。

在以太坊开发中，运行在活跃网络（主网）上的完整节点不是必需的。你可以使用\_testnet\_节点（它存储小型公共测试区块链的副本），或本地私有区块链（参见 [\[ganache\]](broken-reference)），或服务提供商提供的基于云的以太坊客户端（参见 [\[infura\]](broken-reference)），做几乎任何事。

你还可以选择运行轻量级客户端，该客户端不会存储区块链的本地副本或验证块和交易。这些客户端提供钱包的功能，并可以创建和广播交易。

轻量级客户端可用于连接到现有网络，例如你自己的完整节点，公共区块链，公开或许可的（PoA）测试网或私有本地区块链。在实践中，你可能会使用轻量级客户端，如MetaMask，Emerald Wallet，MyEtherWallet或MyCrypto作为在所有不同节点选项之间切换的便捷方式。

尽管存在一些差异，术语“轻量级客户端”和“钱包”可以互换使用。通常，轻量级客户端除了提供钱包的交易功能外，还提供API（如web3js API）。

不要将以太坊中轻量级钱包的概念与比特币中简化支付验证（SPV）客户端的概念混淆。SPV客户验证区块头并使用merkle证明来验证区块链中是否包含交易。以太坊轻量级客户端通常不验证区块头或交易。他们完全信任由第三方运营的完整客户端，让他们通过RPC访问区块链。

**完整节点的优点和缺点**

选择运行一个完整的节点可以帮助各种基于以太坊的网络，但也会给你带来一些温和的或适中的成本。我们来看看一些优点和缺点。

**优点：**

* 支持基于以太坊的网络的弹性和抗审查。
* 权威性验证所有交易。
* 可以与公共区块链上的任何合约进行交互（无需中介）。
* 如有必要，可以离线查询（只读）区块链状态（账户，合约等）。
* 可以在不让第三方知道你正在读取的信息的情况下查询区块链。
* 可以直接将自己的合约部署到公共区块链中（无需中介）。

**缺点：**

* 需要大量且不断增长的硬件和带宽资源。
* 需要几个小时或几天才能完成第一次初始下载的同步。
* 必须维护，升级并保持联机才能保持同步。

**公共测试网的优点和缺点**

无论你是否选择运行完整节点，你可能都需要运行公共testnet节点。我们来看看使用公共测试网的一些优点和缺点。

**优点：**

* 测试网络节点需要同步并存储少得多的数据，根据网络大小约为10GB（截至2018年4月）。
* 测试网络节点可以在几个小时内完全同步。
* 部署合约或进行交易需要测试ether，它没有价值，可以从几个“faucet”免费获得。
* Testnets是与其他许多用户和合约共享的区块链，运行“live”。

**缺点：**

* 你不能在测试网上使用“真实”的钱，它以测试ether运转。
* 因此，你无法针对真正对手进行安全性测试，因为没有任何风险。
* 公共区块链的某些方面无法在testnet上真实地测试。例如，交易费虽然是发送交易所必需的，但由于gas是免费的，因此不需要在测试网上考虑。测试网不会像公共网络那样经历网络拥塞。

**本地实例（TestRPC）的优点和缺点**

对于许多测试目的，最好的选择是使用 testrpc 节点启动一个实例私有区块链。TestRPC创建一个本地私有区块链，你可以与之交互，而无需任何其他参与者。它分享了公共测试网的许多优点和缺点，但也有一些差异。

**优点：**

* 不同步，磁盘上几乎没有数据。你自己挖掘第一块。
* 无需测试ether，你可以将挖矿奖励“奖励”给自己，用于测试。
* 没有其他用户，只有你。
* 没有其他合约，只有你启动后部署的合约。

**缺点：**

* 没有其他用户意味着它不像公共区块链一样。没有交易空间或交易排序的竞争。
* 除你之外没有矿工意味着采矿更具可预测性，因此你无法测试公开区块链上发生的一些情况。
* 没有其他合约意味着你必须部署所有你想测试的内容，包括依赖项和合约库。
* 你不能重新创建一些公共合约及其地址来测试一些场景（例如DAO合约）。

#### 运行以太坊客户端 <a href="#user-content-running_client" id="user-content-running_client"></a>

如果你有时间和资源，你应该尝试运行一个完整的节点，即使只是为了更多地了解这个过程。在接下来的几节中，我们将下载，编译和运行以太坊客户Go-Ethereum（Geth）和Parity。这需要熟悉在操作系统上使用命令行界面。无论你选择将它们作为完整节点，作为testnet节点还是作为本地私有区块链的客户端运行，都值得安装这些客户端。

**完整节点的硬件要求**

在我们开始之前，你应该确保你有一台具有足够资源的计算机来运行以太坊完整节点。你将需要至少80GB的磁盘空间来存储以太坊区块链的完整副本。如果你还想在以太坊测试网上运行完整节点，则至少需要额外的15GB。下载80GB的区块链数据可能需要很长时间，因此建议你使用快速的Internet连接。

同步以太坊区块链是非常密集的输入输出（I / O）。最好有一个固态硬盘（SSD）。如果你有机械硬盘驱动器（HDD），则至少需要8GB的RAM能用作缓存。否则，你可能会发现你的系统速度太慢，无法完全保持同步。

**最低要求：**

* 2核心CPU。
* 固态硬盘（SSD），至少80GB可用空间。
* 最小4GB内存，如果你使用HDD而不是SSD，则至少8GB。
* 8+ MBit/sec下载速度的互联网。

这些是同步基于以太坊的区块链的完整（但已修剪）副本的最低要求。

在编写本文时（2018年4月），Parity代码库的资源往往更轻，如果你使用有限的硬件运行，那么使用Parity可能会看到最好的结果。

如果你想在合理的时间内同步并存储我们在本书中讨论的所有开发工具，库，客户端和区块链，你将需要一台功能更强大的计算机。

**推荐规格：**

* 4个以上核心的快速CPU。
* 16GB+ RAM。
* 至少有500GB可用空间的快速SSD。
* 25+ MBit/sec下载速度的互联网。

很难预测区块链的大小会增加多快，以及何时需要更多的磁盘空间，所以建议你在开始同步之前检查区块链的最新大小。

**构建和运行客户端（节点）的软件要求**

本节介绍Geth和Parity客户端软件。并假设你正在使用类Unix的命令行环境。这些示例显示了在运行Bash shell（命令行执行环境）的Ubuntu Linux操作系统上输入的输出和命令。

通常，每个区块链都有自己的Geth版本，而Parity支持多个以太坊区块链（Ethereum，Ethereum Classic，Ellaism，Expanse，Musicoin）。

在我们开始之前，我们可能需要满足一些先决条件。如果你从未在你当前使用的计算机上进行任何软件开发，则可能需要安装一些基本工具。对于以下示例，你需要安装 git，源代码管理系统; Golang，Go编程语言和标准库; 和Rust，一种系统编程语言。

| Note | <p>Geth的要求各不相同，但如果你坚持使用Go版本1.10或更高版本，你应该能够编译你想要的任何版本的Geth。当然，你应该总是参考你选择的Geth的文档。</p><p>如果安装在你的操作系统上的Golang版本或者从系统的软件包管理器中获得的版本远远早于1.10，请将其删除并从golang.org安装最新版本。</p> |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| Note | Parity需要Rust版本1.24或更高版本。 |
| ---- | ------------------------ |

Parity还需要一些软件库，例如OpenSSL和libudev。要在Linux（Debian）兼容系统上安装，请执行以下操作：

```
$ sudo apt-get install openssl libssl-dev libudev-dev
```

现在你已经安装了 git，golang，rust 和必要的库，让我们开始工作吧！

**Parity**

Parity是完整节点以太坊客户端和DApp浏览器的实现。Parity是由Rust从头开始编写的，系统编程语言是为了构建一个模块化，安全和可扩展的以太坊客户端。Parity由英国公司Parity Tech开发，并以GPLv3开源许可证发布。

| Note | 披露：本书的作者之一Gavin Wood是Parity Tech的创始人，并撰写了大部分Parity客户端。Parity代表了约28%的以太坊客户端。 |
| ---- | --------------------------------------------------------------------------- |

要安装Parity，你可以使用Rust包管理器+cargo+或从GitHub下载源代码。软件包管理器也下载源代码，所以两种选择之间没有太大区别。在下一节中，我们将向你展示如何自己下载和编译Parity。

**安装 Parity**

Parity Wiki提供了在不同环境和容器中构建Parity的说明：

我们将从源代码构建奇偶校验。这假定你已经使用 rustup 安装了Rust（见 [构建和运行客户端（节点）的软件要求](broken-reference)）。

首先，让我们从GitHub获取源代码：

```
$ git clone https://github.com/paritytech/parity
```

现在，我们转到+parity+目录并使用+cargo+构建可执行文件：

```
$ cd parity
$ cargo build
```

如果一切顺利，你应该看到如下所示的内容：

```
$ cargo build
    Updating git repository `https://github.com/paritytech/js-precompiled.git`
 Downloading log v0.3.7
 Downloading isatty v0.1.1
 Downloading regex v0.2.1

 [...]

Compiling parity-ipfs-api v1.7.0
Compiling parity-rpc v1.7.0
Compiling parity-rpc-client v1.4.0
Compiling rpc-cli v1.4.0 (file:///home/aantonop/Dev/parity/rpc_cli)
Finished dev [unoptimized + debuginfo] target(s) in 479.12 secs
$
```

让我们通过调用+--version+选项来运行+parity+以查看它是否已安装：

```
$ parity --version
Parity
  version Parity/v1.7.0-unstable-02edc95-20170623/x86_64-linux-gnu/rustc1.18.0
Copyright 2015, 2016, 2017 Parity Technologies (UK) Ltd
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

By Wood/Paronyan/Kotewicz/Drwięga/Volf
   Habermeier/Czaban/Greeff/Gotchac/Redmann
$
```

现在已安装了Parity，我们可以同步区块链并开始使用一些基本的命令行选项。

**Go-Ethereum (Geth)**

Geth是Go语言实现的，它被积极开发并被视为以太坊客户端的“官方”实现。通常情况下，每个基于以太坊的区块链都会有自己的Geth实现。如果你正在运行Geth，那么你需要确保使用以下某个存储库链接为区块链获取正确的版本。

**版本库链接**

| Note | 你也可以跳过这些说明并为你选择的平台安装预编译的二进制文件。预编译的版本安装起来更容易，可以在上面版本库的“版本”部分找到。但是，你可以通过自己下载和编译软件来了解更多信息。 |
| ---- | --------------------------------------------------------------------------------------- |

**克隆存储库**

我们的第一步是克隆git仓库，以获得源代码的副本。

要创建此存储库的本地克隆，请使用 git 命令，如下所示，在你的主目录或用于开发的任何目录下：

```
$ git clone <Repository Link>
```

在将存储库复制到本地系统时，你应该看到进度报告：

```
Cloning into 'go-ethereum'...
remote: Counting objects: 62587, done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 62587 (delta 10), reused 13 (delta 4), pack-reused 62557
Receiving objects: 100% (62587/62587), 84.51 MiB | 1.40 MiB/s, done.
Resolving deltas: 100% (41554/41554), done.
Checking connectivity... done.
```

现在我们有了Geth的本地副本，我们可以为我们的平台编译一个可执行文件。

**从源代码构建Geth**

要构建Geth，切换到下载源代码的目录并使用 make 命令：

```
$ cd go-ethereum
$ make geth
```

如果一切顺利，你将看到Go编译器构建每个组件，直到它生成+ geth +可执行文件：

```
build/env.sh go run build/ci.go install ./cmd/geth
>>> /usr/local/go/bin/go install -ldflags -X main.gitCommit=58a1e13e6dd7f52a1d5e67bee47d23fd6cfdee5c -v ./cmd/geth
github.com/ethereum/go-ethereum/common/hexutil
github.com/ethereum/go-ethereum/common/math
github.com/ethereum/go-ethereum/crypto/sha3
github.com/ethereum/go-ethereum/rlp
github.com/ethereum/go-ethereum/crypto/secp256k1
github.com/ethereum/go-ethereum/common
[...]
github.com/ethereum/go-ethereum/cmd/utils
github.com/ethereum/go-ethereum/cmd/geth
Done building.
Run "build/bin/geth" to launch geth.
$
```

让我们在停止并更改它的配置之前运行 geth 以确保它工作：

```
$ ./build/bin/geth version

Geth
Version: 1.6.6-unstable
Git Commit: 58a1e13e6dd7f52a1d5e67bee47d23fd6cfdee5c
Architecture: amd64
Protocol Versions: [63 62]
Network Id: 1
Go Version: go1.8.3
Operating System: linux
GOPATH=/usr/local/src/gocode/
GOROOT=/usr/local/go
```

你的 geth version 命令可能会稍微不同，但你应该看到类似上面的版本报告。

最后，我们可能希望将 geth 命令复制到操作系统的应用程序目录（或命令行执行路径上的目录）。在Linux上，我们使用以下命令：

```
$ sudo cp ./build/bin/geth /usr/local/bin
```

先不要开始运行 geth，因为它会以“缓慢的方式”开始将区块链同步，这将花费太长的时间（几周）。[基于以太坊的区块链首次同步](broken-reference) 解释了以太坊区块链的初始同步带来的挑战。

#### 基于以太坊的区块链首次同步 <a href="#user-content-first_sync" id="user-content-first_sync"></a>

通常，在同步以太坊区块链时，你的客户端将下载并验证自创世区块以来的每个区块和每个交易。

虽然可以通过这种方式完整同步区块链，但同步会花费很长时间并且对计算资源要求较高（RAM更多，存储速度更快）。

许多基于以太坊的区块链在2016年底遭受了拒绝服务（DoS）攻击。受此攻击影响的区块链在进行完全同步时倾向于缓慢同步。

例如，在以太坊中，新客户端在到达区块2,283,397之前会进展迅速。该块在2016年9月18日开采，标志着DoS攻击的开始。从这个区块到2,700,031区块（2016年11月26日），交易验证变得非常缓慢，内存密集并且I/O密集。这导致每块的验证时间超过1分钟。以太坊使用硬分叉实施了一系列升级，以解决在拒绝服务中被利用的底层漏洞。这些升级还通过删除由垃圾邮件交易创建的大约2000万个空帐户来清理区块链。<<\[1]>>

如果你正在使用完整验证进行同步，则客户端会放慢速度并可能需要几天或更长时间才能验证受此DoS攻击影响的任何块。

大多数以太坊客户端包括一个选项，可以执行“快速”同步，跳过交易的完整验证，同步到区块链的顶端后，再恢复完整验证。

对于Geth，启用快速同步的选项通常称为 --fast。你可能需要参考你选择的以太坊链的具体说明。

对于Parity，较旧版本（<1.6），该选项为 --warp，较新版本（>=1.6）上默认启用（无需设置配置选项）。

| Note | Geth和Parity只能在空的区块数据库启动时进行快速同步。如果你已经开始没有“快速”模式的同步，则Geth和Parity无法切换。删除区块链数据目录并从头开始“快速”同步比继续完整验证同步更快。删除区块链数据时请小心不要删除任何钱包！ |
| ---- | ----------------------------------------------------------------------------------------------------------------------- |

**JSON-RPC接口**

以太坊客户端提供应用程序编程接口（API）和一组远程过程调用（RPC）命令，这些命令被编码为JavaScript对象表示法（JSON）。这被称为\_JSON-RPC API\_。本质上，JSON-RPC API是一个接口，允许我们将使用以太坊客户端的程序作为\_gateway\_编写到以太坊网络和区块链中。

通常，RPC接口作为端口+8545+上的HTTP服务提供。出于安全原因，默认情况下，它仅受限于从本地主机（你自己的计算机的IP地址为+127.0.0.1+）接受连接。

要访问JSON-RPC API，可以使用专门的库，用你选择的编程语言编写，它提供与每个可用的RPC命令相对应的“桩（stub）”函数调用。或者，你可以手动构建HTTP请求并发送/接收JSON编码的请求。你甚至可以使用通用命令行HTTP客户端（如 curl ）来调用RPC接口。让我们尝试一下（确保你已经配置并运行了Geth）：

Using curl to call the web3\_clientVersion function over JSON-RPC

```
$ curl -X POST -H "Content-Type: application/json" --data \
'{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}' \
http://localhost:8545

{"jsonrpc":"2.0","id":1,
"result":"Geth/v1.8.0-unstable-02aeb3d7/linux-amd64/go1.8.3"}
```

在这个例子中，我们使用 curl 建立一个HTTP连接来访问 http://localhost:8545。我们已经运行了 geth，它将JSON-RPC API作为端口8545上的HTTP服务提供。我们指示 curl 使用HTTP POST 命令并将内容标识为 Content-Type: application/json。最后，我们传递一个JSON编码的请求作为我们HTTP请求的+data+部分。我们的大多数命令行只是设置 curl 来正确地建立HTTP连接。有趣的部分是我们发布的实际的JSON-RPC命令：

```
{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":4192}
```

每个请求包含4个元素：

jsonrpc

JSON-RPC协议的版本。这\_必须\_是“2.0”。

method

要调用的方法的名称。

params

一个结构化值，用于保存在调用方法期间要使用的参数值。该元素可以省略。

id

由客户端建立的标识符，必须包含字符串，数字或NULL值（如果包含）。如果包含，服务器必须在Response对象中使用相同的值进行回复。该元素用于关联两个对象之间的上下文。

| Tip | id 参数主要用于在单个JSON-RPC调用中进行多个请求的情况，这种做法称为\_批处理\_。批处理用于避免每个请求的新HTTP和TCP连接的开销。例如，在以太坊环境中，如果我们想要在一个HTTP连接中检索数千个交易，我们将使用批处理。批处理时，为每个请求设置不同的 id，然后将其与来自JSON-RPC服务器的每个响应中的+id+进行匹配。实现这个最简单的方法是维护一个计数器并为每个请求增加值。 |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

The response we receive is:

```
{"jsonrpc":"2.0","id":4192,
"result":"Geth/v1.8.0-unstable-02aeb3d7/linux-amd64/go1.8.3"}
```

这告诉我们JSON-RPC API由Geth客户端版本1.8.0提供服务。

让我们尝试一些更有趣的事情。在下一个例子中，我们要求JSON-RPC API获取当前的gas价格，以wei为单位：

```
$ curl -X POST -H "Content-Type: application/json" --data \
'{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":4213}' \
http://localhost:8545

{"jsonrpc":"2.0","id":4213,"result":"0x430e23400"}
```

响应 0x430e23400 告诉我们，当前的gas价格是1.8wei（gigawei或十亿wei）。

**Parity的Geth兼容模式**

有一个特殊的“Geth兼容模式”，它提供了一个与+geth+相同的JSON-RPC API。要在Geth兼容模式下运行奇偶校验，请使用+--geth+开关：

#### 轻量级以太坊客户 <a href="#user-content-lw_eth_clients" id="user-content-lw_eth_clients"></a>

轻量级客户端提供了完整客户端的一部分功能。他们不存储完整的以太坊区块链，因此它们的启动速度更快，所需的数据存储量也更少。

轻量级客户端提供以下一项或多项功能：

* 管理钱包中的私钥和以太坊地址。
* 创建，签署和广播交易。
* 使用数据与智能合约进行交互。
* 浏览并与DApps交互。
* 提供到区块浏览器等外部服务的链接。
* 转换ether单位并从外部来源检索汇率。
* 将web3实例作为JavaScript对象注入到Web浏览器中。
* 使用另一个客户端提供/注入浏览器的web3实例。
* 在本地或远程以太网节点上访问RPC服务。

一些轻量级客户端（例如移动（智能手机）钱包）仅提供基本的钱包功能。其他轻量级客户端是完全开发的DApp浏览器。轻量级客户端通常提供完整节点以太坊客户端的某些功能，而无需同步以太坊区块链的本地副本。

我们来看看一些最受欢迎的轻量级客户端及其提供的功能。

#### 移动（智能手机）钱包 <a href="#user-content-mobile_wallets" id="user-content-mobile_wallets"></a>

所有的移动钱包都是轻量级的客户端，因为智能手机没有足够的资源来运行完整的以太坊客户端。

流行的移动钱包包括Jaxx，Status和Trust Wallet。我们列举这些作为流行手机钱包的例子（不是对这些钱包的安全或功能的认可）。

#### 浏览器钱包 <a href="#user-content-browser_wallets" id="user-content-browser_wallets"></a>

各种钱包和DApp浏览器可用作浏览器的插件或扩展，例如Chrome和Firefox：运行在浏览器内的轻量级客户端。

一些比较流行的是MetaMask，Jaxx和MyEtherWallet/MyCrypto。

**MetaMask**

MetaMask 在 [\[intro\]](broken-reference) 中介绍，它是一个多功能的基于浏览器的钱包，RPC客户端和基本合约浏览器。它可用于Chrome，Firefox，Opera和Brave Browser。在以下位置找到MetaMask：

乍一看，MetaMask是一款基于浏览器的钱包。但是，与其他浏览器钱包不同，MetaMask将web3实例注入浏览器，作为连接到各种以太坊区块链（例如mainnet，Ropsten testnet，Kovan testnet，本地RPC节点等）的RPC客户端。能够注入web3实例并充当外部RPC服务的入口，使MetaMask成为开发人员和用户非常强大的工具。例如，它可以与MyEtherWallet或MyCrypto相结合，充当这些工具的web3提供者和RPC网关。

**Jaxx**

在 [移动（智能手机）钱包](broken-reference) 中作为移动钱包介绍的Jaxx也可用作Chrome和Firefox扩展。可以在这里找到：

**MyEtherWallet (MEW)**

MyEtherWallet是一款基于浏览器的JavaScript轻量级客户端，提供：

* 在JavaScript中运行的软件钱包。
* 通往诸如Trezor和Ledger等流行硬件钱包的桥梁。
* 一个web3界面，可以连接到另一个客户端注入的web3实例（例如MetaMask）。
* 可以连接到以太坊完整客户端的RPC客户端。
* 给定合约地址和应用程序二进制接口（ABI），可以与智能合约交互的基本接口。

MyEtherWallet对于测试和作为硬件钱包界面非常有用。它不应该被用作主要的软件钱包，因为它在浏览器环境中会受到威胁，并且不是一个安全的密钥存储系统。

访问MyEtherWallet和其他基于浏览器的JavaScript钱包时，你必须非常小心，因为它们经常是钓鱼攻击的目标。始终使用书签而不是搜索引擎或链接访问正确的网址。MyEtherWallet可以在以下网址找到：

**MyCrypto**

就在本书第一版出版之前，MyEtherWallet项目分为由两个独立开发团队主导的竞争实现：一个“分叉”，就像在开源开发中所称的那样。这两个项目被称为MyEtherWallet（原始品牌）和MyCrypto。在拆分时，MyCrypto提供与MyEtherWallet相同的功能。由于两个开发团队采取不同的目标和优先事项，这两个项目可能会出现分歧。

与MyEtherWallet一样，在浏览器中访问MyCrypto时必须非常小心。始终使用书签，或者非常小心地输入URL（然后将其书签以备将来使用）。

MyCrypto可以在以下网址找到：\
[https://MyCrypto.com](https://mycrypto.com)

**Mist**

Mist是以太坊基金会创建的第一个启用以太坊的浏览器。它还包含一个基于浏览器的钱包，这是有史以来第一个实现ERC20代币标准的（Fabian Vogelsteller，ERC20的作者也是Mist的主要开发人员）。Mist也是第一个引入camelCase校验和的软件包（EIP-155，参见 [\[eip-155\]](broken-reference) ）。Mist运行一个完整的节点，并提供完整的DApp浏览器，支持基于Swarm的存储和ENS地址。可以在以下网址找到：\
[https://github.com/ethereum/mist](https://github.com/ethereum/mist)
