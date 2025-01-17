# 第九章

### 开发工具，框架和库 <a href="#usercontent-kai-fa-gong-ju-kuang-jia-he-ku" id="usercontent-kai-fa-gong-ju-kuang-jia-he-ku"></a>

### 框架 <a href="#usercontent-kuang-jia" id="usercontent-kuang-jia"></a>

框架可使以太坊智能合约开发变得轻松。自己做所有事情，你可以更好地理解所有事物如何结合在一起，但这是一项繁琐而重复的工作。下面列出的框架可以自动执行某些任务并使开发变得轻而易举。

#### Truffle <a href="#user-content-truffle" id="user-content-truffle"></a>

**安装 Truffle 框架**

Truffle 框架由多个 NodeJS+包组成。在我们安装+Truffle+之前，我们需要安装+NodeJS+和Node Package Manager（+npm）的最新版。

推荐的安装 NodeJS 和 npm 的方法是使用node版本管理器（NVM）nvm。一旦我们安装了+nvm+，它将为我们处理所有依赖和更新。我们将按照以下网址中的说明进行操作：

一旦在你的操作系统上安装了+nvm+，安装+NodeJS+就很简单了。我们使用+--lts+标志告诉nvm我们想要最新的“长期支持（LTS）”版本+NodeJS+

确认你已安装 node 和 npm：

```
$ node -v
v8.9.4
$ npm -v
5.6.0
```

创建一个包含DApp支持的Node.js版本的隐藏文件.nvmrc，这样开发人员只需要在项目目录的根目录下运行\`nvm install\`，它就会自动安装并切换到使用该版本。

```
$ node -v > .nvmrc
$ nvm install
```

看起来不错。现在安装Truffle：

```
$ npm -g install Truffle

+ Truffle@4.0.6
installed 1 package in 37.508s
```

**集成预编译的 Truffle 项目 (Truffle Box)**

如果我们想要使用或创建一个建立在预先构建的样板上的DApp，那么在Truffle Boxes链接中，我们可以选择一个现有的Truffle项目，然后运行以下命令来下载并提取它：

```
$ Truffle unbox <BOX_NAME>
```

**创建 Truffle 项目目录**

对于我们将使用Truffle的每个项目，我们创建一个项目目录并在该目录中初始化Truffle。Truffle将在我们的项目目录中创建必要的目录结构。通常，我们为项目目录指定一个描述我们项目的名称。对于这个例子，我们将使用Truffle从 [\[simple\_contract\_example\]](broken-reference) 部署我们的Faucet合约，因此我们将命名项目文件夹+Faucet+。

```
$ mkdir Faucet
$ cd Faucet
Faucet $
```

一旦进入 Faucet 目录，我们初始化 Truffle：

Truffle创建了一个目录结构和一些默认文件：

```
Faucet
├── contracts
│   └── Migrations.sol
├── migrations
│   └── 1_initial_migration.js
├── test
├── Truffle-config.js
└── Truffle.js
```

除了Truffle本身之外，我们还将使用一些JavaScript（nodeJS）支持包。我们可以用npm安装这些。我们初始化npm目录结构并接受npm建议的默认值：

```
$ npm init

package name: (faucet)
version: (1.0.0)
description:
entry point: (Truffle-config.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to Faucet/package.json:

{
  "name": "faucet",
  "version": "1.0.0",
  "description": "",
  "main": "Truffle-config.js",
  "directories": {
    "test": "test"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this ok? (yes)
```

现在，我们可以安装我们用来使Truffle变得更容易的依赖关系：

```
$ npm install dotenv Truffle-wallet-provider ethereumjs-wallet
```

你现在有一个带有数千个文件的+node\_modules+目录。

在将DApp部署到云生产或持续集成环境之前，指定 engines 字段非常重要，以便你的Dapp使用正确的Node.js版本进行构建，并且会安装相关的依赖关系。

**配置 Truffle**

Truffle 创建一些空的配置文件，Truffle.js+和+Truffle-config.js。在Windows系统上，当你尝试运行命令+Truffle+，Windows尝试运行+Truffle.js+时，+ Truffle.js+名称可能会导致冲突。为了避免这种情况，我们将删除+Truffle.js+并使用+Truffle-config.js+来支持Windows用户，他们的确已经受够了。

现在我们编辑 Truffle-config.js 并用下面的内容替换：

Truffle-config.js - a Truffle configuration to get us started

```
module.exports = {
	networks: {
		localnode: { // Whatever network our local node connects to
			network_id: "*", // Match any network id
			host: "localhost",
			port: 8545,
		}
	}
};
```

以上配置是一个很好的起点。它设置了一个默认的以太坊网络（名为+localnode+），该网络假定你正在运行以太坊客户端（如Parity），既可以作为完整节点，也可以作为轻客户端。该配置将指示Truffle与端口8545上的本地节点通过RPC进行通信。Truffle将使用本地节点连接的任何以太网（如Ethereum主网络）或测试网络（如Ropsten）。本地节点也将提供钱包功能。

在下面的章节中，我们将配置其他网络供Truffle使用，比如+ganache+ test-RPC区块链和托管网络提供商Infura。随着我们添加更多网络，配置文件将变得更加复杂，但它也将为我们的测试和开发工作流程提供更多选择。

**使用Truffle部署合约**

我们现在有一个针对我们的 Faucet 项目的基本工作目录，并且我们已经配置了Truffle和它的依赖关系。合约在我们项目的+contracts 子目录中。该目录已经包含一个“helper”合约，+Migrations.sol+管理合约升级。我们将在后面的章节中研究 +Migrations.sol 的使用。

让我们将 Faucet.sol 合约（[\[solidity\_faucet\_example\]](broken-reference)）复制到+contracts+子目录中，以便项目目录如下所示：

```
Faucet
├── contracts
│   ├── Faucet.sol
│   └── Migrations.sol
...
```

我们现在可以让Truffle编译我们的合约：

```
$ Truffle compile
Compiling ./contracts/Faucet.sol...
Compiling ./contracts/Migrations.sol...
Writing artifacts to ./build/contracts
```

**Truffle migrations - 理解部署脚本**

Truffle提供了一个名为\_migration\_的部署系统。如果你曾在其他框架中工作过，你可能会看到类似的东西：Ruby on Rails，Python Django和许多其他语言和框架都有+migrate+命令。

在所有这些框架中，migration的目的是处理不同版本软件之间数据模式的变化。以太坊migration的目的略有不同。因为以太坊合约是不可变的，而且要消耗gas部署，所以Truffle提供了一个migration机制来跟踪哪些合约（以及哪些版本）已经部署。在一个拥有数十个合约和复杂依赖关系的复杂项目中，你不希望为了重新部署尚未更改的合约而支付gas。你也不想手动跟踪哪些合约的哪些版本已经部署了。Trufflemigration机制通过部署智能合约+Migrations.sol+完成所有这些工作，然后跟踪所有其他合约部署。

我们只有一份合约，Faucet.sol，这至少意味着migration系统是大材小用的。不幸的是，我们必须使用它。但是，通过学习如何将它用于一个合约，我们可以开始练习一些良好的开发工作习惯。随着事情变得更加复杂，这项努力将会得到回报。

Truffle的+migrations+目录是找到迁移脚本的地方。现在，只有一个脚本 1\_initial\_migration.js，它会部署 Migrations.sol 合约本身：

\[\[1\_initial\_migration]] .1\_initial\_migration.js - the migration script for Migrations.sol

```
include::code/truffle/Faucet/migrations/1_initial_migration.js

var Migrations = artifacts.require("./Migrations.sol");

module.exports = function(deployer) {
  deployer.deploy(Migrations);
};
```

我们需要第二个migration脚本来部署 Faucet.sol。我们称之为+2\_deploy\_contracts.js+。它非常简单，就像+1\_initial\_migration.js+一样，只需稍作修改即可。实际上，你可以复制+ 1\_initial\_migration.js+的内容，并简单地将+Migrations+的所有实例替换为+Faucet+：

\[\[2\_deploy\_contracts]] .2\_deploy\_contracts.js - the migration script for Faucet.sol

```
include::code/truffle/Faucet/migrations/2_deploy_contracts.js

var Faucet = artifacts.require("./Faucet.sol");

module.exports = function(deployer) {
  deployer.deploy(Faucet);
};
```

脚本初始化变量+Faucet+，将+Faucet.sol+ Solidity源代码标识为定义+Faucet+的工件。然后，它调用部署功能来部署此合约。

我们都准备好了。我们使用 truffle migrate 来部署合约。我们必须使用+--network+参数指定在哪个网络上部署合约。我们只在配置文件中指定了一个网络，我们将其命名为+localnode+。确保你的本地以太坊客户端正在运行，然后输入：

```
Faucet $ Truffle migrate --network localnode
```

因为我们使用本地节点连接到以太坊网络并管理我们的钱包，所以我们必须授权Truffle创建的交易。我正在运行+parity+连接到Ropsten测试区块链，所以在Trufflemigration期间，我会在parity的Web控制台上看到一个弹出窗口：



Figure 1. Parity asking for confirmation to deploy Faucet

你将看到四笔交易，总计。一个部署+Migrations+，一个用于将部署计数器更新为+1+，一个用于部署+Faucet+，另一个用于将部署计数器更新为+2+。

Truffle将显示migration完成情况，显示每个交易并显示合约地址：

```
$ Truffle migrate --network localnode
Using network 'localnode'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0xfa090db179d023d2abae543b4a21a1479e70ca7d35a469a5d1a98bfc6bd80fe8
  Migrations: 0x8861c27715550bed8362c0345add158489df6db0
Saving successful migration to network...
  ... 0x985c4a32716826ddbe4eae284104bef8bc69e959899f62246a1b27c9dfcd6c03
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying Faucet...
  ... 0xecdbeef77f0558edc689440e34b7bba0a3ba7a45e4b680b071b47c30a930e9d6
  Faucet: 0xd01cd8e7bd29e4bff8c1693f59eee46137a9f300
Saving successful migration to network...
  ... 0x11f376bd7307edddfd40dc4a14c3f7cb84b6c921ac2465602060b67d08f9fd8a
Saving artifacts...
```

**使用Truffle控制台**

Truffle提供了一个JavaScript控制台，我们可以使用这个控制台与Ethereum网络（通过本地节点）进行交互，与已部署的合约进行交互，并与钱包提供商进行交互。在我们当前的配置（localnode）中，节点和钱包提供商是我们的本地parity客户端。

让我们开始Truffle控制台并尝试一些命令：

```
$ Truffle console --network localnode
Truffle(localnode)>
```

Truffle提示一个提示符，显示所选的网络配置（localnode）。记住并了解我们正在使用哪个网络很重要。你不希望在Ethereum主网络上意外部署测试合约或进行交易。这可能是一个昂贵的错误！

Truffle控制台提供了自动补全功能，使我们可以轻松探索环境。如果我们在部分完成的命令后按+Tab+，Truffle将为我们完成命令。如果有多个命令与我们的输入相匹配，按+Tab+两次将显示所有可能的完成。事实上，如果我们在空提示符下按两次+Tab+，Truffle将列出所有命令：

```
Truffle(localnode)>
Array Boolean Date Error EvalError Function Infinity JSON Math NaN Number Object RangeError ReferenceError RegExp String SyntaxError TypeError URIError decodeURI decodeURIComponent encodeURI encodeURIComponent eval isFinite isNaN parseFloat parseInt undefined

ArrayBuffer Buffer DataView Faucet Float32Array Float64Array GLOBAL Int16Array Int32Array Int8Array Intl Map Migrations Promise Proxy Reflect Set StateManager Symbol Uint16Array Uint32Array Uint8Array Uint8ClampedArray WeakMap WeakSet WebAssembly XMLHttpRequest _ assert async_hooks buffer child_process clearImmediate clearInterval clearTimeout cluster console crypto dgram dns domain escape events fs global http http2 https module net os path perf_hooks process punycode querystring readline repl require root setImmediate setInterval setTimeout stream string_decoder tls tty unescape url util v8 vm web3 zlib

__defineGetter__ __defineSetter__ __lookupGetter__ __lookupSetter__ __proto__ constructor hasOwnProperty isPrototypeOf propertyIsEnumerable toLocaleString toString valueOf
```

绝大多数钱包和节点相关功能由+web3+对象提供，该对象是 web3.js+库的一个实例。+web3+对象将RPC接口抽象为我们的parity节点。你还会注意到两个熟悉名称的对象：+Migrations 和 Faucet。这些代表我们刚刚部署的合约。我们将使用Truffle控制台与合约进行交互。首先，让我们通过 web3 对象检查我们的钱包：

```
Truffle(localnode)> web3.eth.accounts
[ '0x9e713963a92c02317a681b9bb3065a8249de124f',
  '0xdb5dc1a13e3a55cf3b4587cd8d1e5fdeb6738145' ]
```

我们的parity客户端有两个钱包，Ropsten有一些测试ether。web3.eth.accounts 属性包含所有帐户的列表。我们可以使用 getBalance 函数检查第一个帐户的余额：

```
Truffle(localnode)> web3.eth.getBalance(web3.eth.accounts[0]).toNumber()
191198572800000000
Truffle(localnode)>
```

web3.js 是一个大型JavaScript库，通过提供者（如本地客户端）为以太坊系统提供全面的界面。我们将在[\[web3js\]](broken-reference)中更详细地研究+web3.js+。现在让我们尝试与我们的合约进行交互：

```
Truffle(localnode)> Faucet.address
'0xd01cd8e7bd29e4bff8c1693f59eee46137a9f300'
Truffle(localnode)> web3.eth.getBalance(Faucet.address).toNumber()
0
Truffle(localnode)>
```

接下来，我们将使用 sendTransaction 发送一些测试ether，为 Faucet 提供资金。请注意使用+web3.toWei+为我们转换ether单位。在没有出错的情况下输入十八个零既困难又危险，因此使用单位转换器来获取值总是更好。以下是我们发送交易的方式：

```
Truffle(localnode)> web3.eth.sendTransaction({from:web3.eth.accounts[0], to:Faucet.address, value:web3.toWei(0.5, 'ether')});
'0xf134c75b985dc0e0c27c2f0412251e0860eb530a5055e660f21e7483ab336808'
```

切换到+parity+的Web控制台，你将看到一个弹出窗口，要求你确认该交易。等一下，一旦交易开始，你将能够看到我们的+Faucet+合约的余额：

```
Truffle(localnode)> web3.eth.getBalance(Faucet.address).toNumber()
500000000000000000
```

我们调用+withdraw+函数，从Faucet中取出一些测试ether：

```
Truffle(localnode)> Faucet.deployed().then(instance => {instance.withdraw(web3.toWei(0.1, 'ether'))}).then(console.log)
```

同样，你需要批准parity Web控制台中的交易。Faucet+的余额已经下降，我们的测试钱包已经收到+0.1 ether：

```
Truffle(localnode)> web3.eth.getBalance(Faucet.address).toNumber()
400000000000000000
```

```
Truffle(localnode)> Faucet.deployed().then(instance => {instance.withdraw(web3.toWei(1, 'ether'))})
```

```
StatusError: Transaction: 0xe147ae9e3610334ada8d863c9028c12bd0501be2d0cfd05865c18612b92d3f9c exited with an error (status 0).
```

#### Embark <a href="#user-content-embark" id="user-content-embark"></a>

#### OpenZeppelin <a href="#user-content-openzeppelin" id="user-content-openzeppelin"></a>

OpenZeppelin框架是以太坊智能合约使用最广泛的解决方案。这是由于社区讨论每个提议的解决方案并从这些解决方案的实施和整合中学习，这将变成一个不断增长的反馈循环，改进现有合约并找到将它们结合在一个清晰安全的体系结构中的新可能性。它不断增加新的可重用合约来解决越来越复杂的挑战，或在以太坊区块链上探索激动人心的新可能性。如前所述，该框架目前拥有丰富的合约库，从ERC20和ERC721 token的实现，到众多的crowdsale模型，到简单的行为，例如\`Ownable\`，``Pausable`或`LimitBalance``。 在某些情况下，此存储库中的合约甚至作为\_de facto\_标准实现。

该框架拥有MIT许可证，并且所有合约都采用模块化方法进行设计，以确保易用性和扩展性。这些都是干净而基本的构建块，可以在你的下一个以太坊项目中使用。让我们设置框架，并使用OpenZeppelin合约构建一个简单的crowdsale，作为使用它的简单例子。这个例子还强调了重用安全组件的重要性，而不是自己编写安全组件，并给出了以太坊平台及其社区成为可能的想法的一个小样本。

首先，我们需要将npm中的openzepelin-solidity库安装到我们的工作区中。截至撰写本文时的最新版本是\`v1.9.0\`，所以我们将使用该版本。

```
mkdir sample-crowdsale
cd sample-crowdsale
npm install openzeppelin-solidity@1.9.0
mkdir contracts
```

对于crowdsale而言，我们需要定义一个token，我们会给予投资者以换取其ether。在撰写本文时，OpenZeppelin包含了遵循ERC20，ERC721和ERC827标准的多个基本token合约，具有不同的发行，限制，兑现，生命周期等特征。

让我们制作一个ERC20 token，这意味着初始供应从0开始，token所有者（在我们的例子中，是crowdsale合约）可以创建新的 token并分配给投资者。为此，使用以下内容创建\`contracts/SampleToken.sol\`文件：

```
include::code/OpenZeppelin/contracts/SampleToken.sol

pragma solidity 0.4.23;

import 'openzeppelin-solidity/contracts/token/ERC20/MintableToken.sol';

contract SampleToken is MintableToken {
  string public name = "SAMPLE TOKEN";
  string public symbol = "SAM";
  uint8 public decimals = 18;
}
```

```
include::code/OpenZeppelin/contracts/SampleCrowdsale.sol

pragma solidity 0.4.23;

import './SampleToken.sol';
import 'openzeppelin-solidity/contracts/crowdsale/emission/MintedCrowdsale.sol';
import 'openzeppelin-solidity/contracts/crowdsale/distribution/PostDeliveryCrowdsale.sol';

contract SampleCrowdsale is PostDeliveryCrowdsale, MintedCrowdsale {

  constructor(
    uint256 _openingTime,
    uint256 _closingTime
    uint256 _rate,
    address _wallet,
    MintableToken _token
  )
    public
    Crowdsale(_rate, _wallet, _token)
    PostDeliveryCrowdsale(_openingTime, _closingTime)
  {
  }
}
```

最后，在我们对我们的解决方案感到满意并且我们已经彻底测试之后，我们需要部署它。OpenZeppelin与Truffle很好地集成在一起，所以我们可以按照上面的Truffle部分所述编写一个migration文件。在 migrations/2\_deploy\_contracts.js 中写入以下内容：

```
include::code/OpenZeppelin/migrations/2_deploy_contracts.js

const SampleCrowdsale = artifacts.require('./SampleCrowdsale.sol');
const SampleToken = artifacts.require('./SampleToken.sol');

module.exports = function(deployer, network, accounts) {
  const openingTime = web3.eth.getBlock('latest').timestamp + 2; // two secs in the future
  const closingTime = openingTime + 86400 * 20; // 20 days
  const rate = new web3.BigNumber(1000);
  const wallet = accounts[1];

  return deployer
    .then(() => {
      return deployer.deploy(SampleToken);
    })
    .then(() => {
      return deployer.deploy(
        SampleCrowdsale,
        openingTime,
        closingTime,
        rate,
        wallet,
        SampleToken.address
      );
    });
};
```

这只是OpenZeppelin框架中一些合约的简要概述。还有更多，社区总是提出新的想法，实施新的策略以使它们更安全，更简单，更清晰，并尽早发现漏洞以防止主要网络合约中的漏洞。欢迎你加入社区进行学习和贡献。

#### zeppelin\_os <a href="#user-content-zeppelin_os" id="user-content-zeppelin_os"></a>

[zeppelin\_os](https://github.com/zeppelinos) 是一款开源的分布式工具和服务平台，位于EVM之上，安全地开发和管理智能合约应用程序。

与OpenZeppelin的代码每次都需要重新部署每个应用程序不同，zeppelin\_os的代码处于链上。需要特定功能的应用程序（例如ERC20 token）不仅不需要重新设计和重新审计其实施（OpenZeppelin解决了这些问题），而且甚至不需要部署它。使用zeppelin\_os，应用程序可直接与 链上的token实现进行交互，这与桌面应用程序与其底层操作系统的组件进行交互的方式大致相同。

利用OpenZeppelin的应用程序通过重用库的组织和同行评审合约避免了“重新发明轮子”。然而，每当应用程序使用ERC20 token实现时，同一个ERC20字节码会一次又一次地部署到区块链中。这种字节码在网络中无数次重复存在。现在，使用zeppelin\_os的应用程序可以避免这种不必要的重复。他们并没有部署自己的ERC20实施，而是链接到定义了社区接受的最新ERC20实现的合约。这种单一的中央实现仅部署在区块链中，与Solidity的库非常相似，但却相当复杂。

与Solidity的库不同，zeppelin\_os提供的实现可以像常规合约一样对待，即它们具有存储空间。而且，它们是可升级的。如果在其中一个OS的官方实现中发现了一个漏洞，它可以简单地与升级的漏洞交换。对于ERC20 token，对其实施的升级会立即波及到所有使用它的应用程序。操作系统不仅为其所有实现提供可升级性，还为用户自己的合约提供升级能力，甚至为其自己的代码库提供升级能力！开发人员决定应用程序何时以及如何实施升级，甚至决定要遵守哪种实施方案。

zeppelin\_os的核心是一个非常聪明的合约，被称为“代理（proxy）”。代理是一种能够包装任何其他合约，暴露其接口而无需手动实现setter和getter的合约，并且可以在不丢失状态的情况下进行升级。在Solidity术语中，它可以被看作是一个正常的合约，其业务逻辑包含在一个库中，随时可以由一个新库来交换，而不会丢失其状态。代理链接到其实现的方式是完全自动的，并且封装给开发人员。实际上，任何合约都可以升级，代码几乎不变。关于zeppelin\_os的代理机制的更多信息可以在Zeppelin的博客中找到：[https://blog.zeppelinos.org/\[upgradeability-using-unstructured-storage\]，](https://blog.zeppelinos.org/\[upgradeability-using-unstructured-storage]%EF%BC%8C)

操作系统将其实现封装在可使用ZepTokens担保(vouched)的软件包或“发行版”中。因此，可以针对某个版本押注ZepTokens，将其标识为社区可接受的实现集。任何人都可以提交新的发行版，由社区审查并最终被接受为官方的新版本。作为奖励，发行版的开发者在它每次被押注时都会收到token。作为一名Dapp开发人员，担保(vouching)提供了一种可测量的方式来确定给定发行版获得的支持，以及可信度。

//// TODO: the example provided above is still a WIP - link to a tutorial once it’s finished

### 实用程序 <a href="#usercontent-shi-yong-cheng-xu" id="usercontent-shi-yong-cheng-xu"></a>

#### ethereumJS helpeth: 命令行实用程序 <a href="#usercontentethereumjshelpeth-ming-ling-hang-shi-yong-cheng-xu" id="usercontentethereumjshelpeth-ming-ling-hang-shi-yong-cheng-xu"></a>

helpeth是一个命令行工具，使开发人员更容易的操作密钥和交易。

它是基于JavaScript的库和工具集合ethereumjs的一部分。

```
Usage: helpeth [command]

Commands:
  signMessage <message>                     Sign a message
  verifySig <hash> <sig>                    Verify signature
  verifySigParams <hash> <r> <s> <v>        Verify signature parameters
  createTx <nonce> <to> <value> <data>      Sign a transaction
  <gasLimit> <gasPrice>
  assembleTx <nonce> <to> <value> <data>    Assemble a transaction from its
  <gasLimit> <gasPrice> <v> <r> <s>         components
  parseTx <tx>                              Parse raw transaction
  keyGenerate [format] [icapdirect]         Generate new key
  keyConvert                                Convert a key to V3 keystore format
  keyDetails                                Print key details
  bip32Details <path>                       Print key details for a given path
  addressDetails <address>                  Print details about an address
  unitConvert <value> <from> <to>           Convert between Ethereum units

Options:
  -p, --private      Private key as a hex string                        [string]
  --password         Password for the private key                       [string]
  --password-prompt  Prompt for the private key password               [boolean]
  -k, --keyfile      Encoded key file                                   [string]
  --show-private     Show private key details                          [boolean]
  --mnemonic         Mnemonic for HD key derivation                     [string]
  --version          Show version number                               [boolean]
  --help             Show help                                         [boolean]
```

#### dapp.tools <a href="#user-content-dapp-tools" id="user-content-dapp-tools"></a>

### 安装: <a href="#usercontent-an-zhuang" id="usercontent-an-zhuang"></a>

```
==== Dapp
https://dapp.tools/dapp/

==== Seth
https://dapp.tools/seth/

==== Hevm
https://dapp.tools/hevm/

==== SputnikVM

SputnikVM是一个独立的可插拔的用于不同的基于以太坊的区块链的虚拟机。它是用Rust编写的，可以用作二进制，货物箱，共享库，或者通过FFI，Protobuf和JSON接口集成。它有一个单独的用于测试目的的二进制sputnikvm-dev，它模拟大部分JSON RPC API和区块挖掘。

Github link; https://github.com/etcdevteam/sputnikvm

== Libraries

=== web3.js

web3.js是以太坊兼容的JS API，用于通过以太坊基金会开发的JSON RPC与客户进行通信。

Github link; https://github.com/ethereum/web3.js

+npm+ package repository link; https://www.npmjs.com/package/web3

Documentation link for web3.js API 0.2x.x; https://github.com/ethereum/wiki/wiki/JavaScript-API

Documentation link for web3.js API 1.0.0-beta.xx; https://web3js.readthedocs.io/en/1.0/web3.html

=== web3.py

web3.py 是一个用于与以太坊区块链进行交互的Python库。它现在也在以太坊基金会的GitHub中。

Github link; https://github.com/ethereum/web3.py

PyPi link; https://pypi.python.org/pypi/web3/4.0.0b9

Documentation link; https://web3py.readthedocs.io/

=== EthereumJS

以太坊的库和实用程序集合。

Github link; https://github.com/ethereumjs

Website link; https://ethereumjs.github.io/

=== web3j

web3j 是Java和Android库，用于与Ethereum客户端集成并使用智能合约。

Github link; https://github.com/web3j/web3j

Website link; https://web3j.io

Documentation link; https://docs.web3j.io

=== Etherjar


Etherjar 是与Ethereum集成并与智能合约一起工作的另一个Java库。它专为基于Java 8+的服务器端项目而设计，提供RPC的低层和高层封装，以太坊数据结构和智能合约访问。

Github link; https://github.com/infinitape/etherjar

=== Nethereum

Nethereum 是以太坊的.Net集成库。

Github link; https://github.com/Nethereum/Nethereum

Website link; http://nethereum.com/

Documentation link; https://nethereum.readthedocs.io/en/latest/

=== ethers.js

ethers.js 库是一个紧凑，完整，功能齐全，经过广泛测试的以太坊库，完全根据MIT许可证获得，并且已收到来自以太坊基金会的DevEx资助以扩展和维护。

GitHub link: https://github.com/ethers-io/ethers.js

Documentation: https://docs.ethers.io


=== Emerald Platform

Emerald Platform提供了库和UI组件，可以在以太坊上构建Dapps。Emerald JS和Emerald JS UI提供了一组模块和React组件来构建Javascript应用程序和网站，Emerald SVG Icons是一组区块链相关的图标。除了Javascript库之外，它还有Rust库来操作私钥和交易签名。所有Emerald库和组件都使用 Apache 2许可。

Github link; https://github.com/etcdevteam/emerald-platform

Documentation link; https://docs.etcdevteam.com

<<第十章#,下一章：Tokens>>

image::images/thanks.jpeg["赞赏译者",height=400,align="center"]
```
