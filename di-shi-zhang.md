# 第十章

### Tokens <a href="#user-content-tokens_chapter" id="user-content-tokens_chapter"></a>

#### 什么是Token? <a href="#user-content-tokens_definition" id="user-content-tokens_definition"></a>

单词\_Token\_来源于古英语“tacen”，意思是符号或符号。常用来表示私人发行的类似硬币的物品，价值不大，例如交通Token，洗衣Token，游乐场Token。

如今，基于区块链的Token将这个词重新定义为基于区块链的抽象概念，可以被拥有，并代表资产，货币或访问权。

“Token”一词与微不足道的价值之间的联系与物理Token的使用限制有很大关系。通常仅限于特定的企业，组织或地点，物理Token不易交换，不能用于多个功能。通过区块链标记，这些限制被删除。这些Token中的许多Token在全球范围内有多种用途，可以在全球流动市场中相互交易或与其他货币交易。随着这些限制的消失，“微不足道的价值”的期望也成为过去。

在本节中，我们将看到Token的各种用法以及它们的创建方式。我们还讨论Token的属性，如可互换性和内在性等。最后，我们通过基于构建自己的Token的实验来检验它们的标准和技术。

#### 如何使用Token？ <a href="#user-content-tokens_use" id="user-content-tokens_use"></a>

Token最明显的用途是作为数字私人货币。但是，这只是一个可能的用途。Token可以被编程为提供许多不同的功能，通常是重叠的。例如，Token可以同时传达投票权，访问权和资源所有权。货币只是第一个“应用程序”。

货币

Token可以作为一种货币形式，其价值通过私人交易来确定。例如，ether或bitcoin。

资源

Token可以表示在共享经济或资源共享环境中获得或生成的资源。例如，表示可通过网络共享的资源的存储或CPU的Token。

资产

Token可以代表内在或外在，有形或无形资产的所有权。例如，黄金，房地产，汽车，石油，能源等

访问

Token可以代表访问权限，可以访问数字或实体资产，例如论坛，专属网站，酒店房间，租车。

权益

Token可以代表数字组织（例如DAO）或法律虚拟主体（例如公司）中的股东权益

投票

Token可以代表数字或法律系统中的投票权。

收藏品

Token可以代表数字（例如CryptoPunks）或物理收藏品（例如绘画）

身份

Token可以代表数字（例如头像）或合法身份（例如国家ID）。

证明

Token可以代表某些机构或去中心化的信用系统（例如婚姻记录，出生证明，大学学位）的认证或事实证明。

实际用途

Token可用于访问或支付服务。

通常，单个Token包含其中几个功能。有时它们之间很难辨别，因为物理等价物一直是密不可分的。例如，在物理世界中，驾驶执照（认证）也是身份证件（身份证明），两者不能分开。在数字领域，以前的混合功能可以独立分离和开发（例如匿名认证）。

#### Tokens和可互换性 <a href="#user-content-tokens_fungibility" id="user-content-tokens_fungibility"></a>

来自Wikipedia:

```
在经济学中，可互换性是一种商品或商品的财产，其独立单位本质上是可以互换的。
```

当我们可以将Token的任何单个单元替换为另一个Token而其价值或功能没有任何差异时，Token是可替代的。例如，ether是一种可替代的Token，因为任何ether的单位具有相同的值并且与任何其他单位的ether一起使用。

严格地说，如果可以跟踪Token的历史出处，那么它就不是完全可替代的。追踪出处的能力可能导致黑名单和白名单，从而降低或消除互通性。我们将在[\[privacy\]](broken-reference)中进一步研究。

不可互换的Token是代表独特的有形或无形商品的Token，因此不可互换。例如，表示\_特定的\_ Van Gogh绘画所有权的Token不等同于代表毕加索的另一个Token。同样，表示特定数字收藏的Token，如特定的CryptoKitty（请参阅[\[cryptoKitties\]](broken-reference)）与任何其他CryptoKitty都不可互换。每个不可互换的Token与唯一标识符相关联，例如序列号。

本节后面我们将看到可替换和不可替换Token的例子。

#### 交易对手风险 <a href="#user-content-counterparty_risk" id="user-content-counterparty_risk"></a>

交易对手风险是交易中的其他方不能履行其义务的风险。由于在交易中增加了两个以上的交易方，某些类型的交易会产生额外的交易对手风险。例如，如果你持有贵金属存款证明并将其出售给某人，则该交易中至少有三方：卖方，买方和贵金属的保管人。有人持有有形资产，必要时他们成为一方并为涉及该资产的任何交易添加交易对手风险。当资产通过交换所有权信息而间接交易时，资产托管人有额外的交易对手风险。他们有资产吗？他们是否会根据Token的转让（例如证书，契约，所有权或数字Token）识别（或允许）所有权的转移？在数字Token的世界中，了解谁持有由Token表示的资产以及适用于该基础资产的规则很重要。

#### Tokens和内在性 <a href="#user-content-tokens_intrinsicality" id="user-content-tokens_intrinsicality"></a>

单词 "intrinsic" 源于拉丁词 "intra", 表示"来自内部".

一些Token代表对区块链来说是 _内在的_ 的数字项目。这些数字资产受共识规则的约束，就像Token本身一样。这具有重要的意义：代表固有资产的Token不会带来额外的交易对手风险。如果你持有1 ether的密钥，就没有其他方为你持有那个以太。区块链共识规则的应用，使得你对私钥的所有权（控制权）等同于资产的所有权，无需任何中介。

相反，许多Token用于表示 _外在的_ \_extrinsic\_事物，如房地产，公司投票股票，商标，金条。这些项目的所有权不属于区块链，属于法律，习惯和政策，与管理Token的共识规则分开。换句话说，Token发行人和所有者可能仍然依赖现实世界的非智能合约。因此，这些外部资产会带来额外的交易对手风险，因为它们由托管人持有，记录在外部注册管理机构中，或由区块链环境以外的法律和政策控制。

基于区块链的Token最重要的后果之一是能够将外部资产转换为内部资产，从而消除交易对手风险。一个很好的例子就是从一家公司的股权（外部）转向一个 _去中心化的自治组织_ 或类似的（内部）组织的股权或投票权。

#### 使用Tokens：效用或权益 <a href="#user-content-using_tokens" id="user-content-using_tokens"></a>

今天以太坊的几乎所有项目都以某种形式发布。但是，所有这些项目真的需要一个Token吗？使用Token有什么缺点，或者我们会看到口号“将所有东西Token化”的口号是否成熟？

首先，让我们首先澄清Token在新项目中的作用。大多数项目都以两种方式之一使用Token：要么是“实用Token”，要么是“权益Token”。很多时候，这两个角色是混合在一起的，难以区分。

实用Token是那些需要使用Token来支付服务，应用程序或资源的Token。实用Token的例子包括代表资源的Token，如共享存储，访问社交媒体网络等服务，或将ether作为以太坊平台的gas。相比之下，权益Token是代表创业公司股票的Token。

股权Token可以像享有利润和分红的无投票权股份一样有限，或者向去中心化自治组织的有投票权的股票一样广泛，其中平台是通过Token持有者的多数投票管理的。

**它不是一只鸭子**

仅仅因为Token用于为初创公司筹款，并不意味着它必须用作服务的支付，反之亦然。然而，许多初创公司面临着一个难题：Token是一种很好的筹款机制，但向大众提供证券（股权）是大多数司法管辖区的受监管活动。通过将股权Token伪装成实用Token，许多创业公司希望能够绕过这些监管限制，并从公开募股筹集资金，同时将其作为预售的实用Token。这些稀薄的股权产品是否能够摆脱监管机构仍有待观察。

正如俗语所说：“如果它像鸭子一样走路，像鸭子一样嘎嘎叫 - 它就是一只鸭子。” 监管机构不会因这些语义扭曲而分心，恰恰相反，他们更有可能将这种法律诡辩看作是企图欺骗公众。

**实用Token：谁需要它们？**

真正的问题是实用Token为初创公司带来了重大风险和被采用障碍。也许在遥远的将来，“将所有事物Token化”成为现实。但是，目前，获得，理解和使用Token的人数是已经很小的加密货币市场的一个子集。

对于创业公司而言，每项创新都代表着风险和市场过滤。创新走的是人迹罕至的路，远离传统的道路。它已经是一个孤独的散步。如果一家创业公司试图在一个新的技术领域进行创新，比如P2P网络上的存储共享，那么这是一条足够孤单的道路。为该创新添加实用Token并要求用户采用Token以使用该服务会增加风险并增加被采用的障碍。它走出了已然孤独的P2P存储创新之路，进入荒野。

将每项创新视为过滤器。它限制了可以成为这种创新的早期采用者的市场子集。添加第二个过滤器化合物，会进一步限制可找到的市场。你要求你的早期采用者采用的不仅仅是两种全新的技术：你构建的新颖应用程序/平台/服务以及Token经济。

对于初创公司而言，每项创新都会带来风险，从而增加创业失败的可能性。如果你已经采取冒险的创业想法并添加实用Token，则也同时增加了所有底层平台（以太坊），更广泛的经济（交易所，流动性），监管环境（股票/商品监管机构）和技术（智能合约，Token标准）的风险。这对创业公司来说是一个很大的风险。

“Tokenize all the things”的倡导者可能会通过采用Token来反对上述说法，他们也继承了整个Token经济的市场热情，早期采用者，技术，创新和流动性。这也是事实。问题是收益和热情是否超过风险和不确定性。

尽管如此，一些最具创新性的商业理念确实发生在加密领域。如果监管机构不能快速通过法律并支持新的商业模式，人才和企业家将寻求在更加加密友好的其他司法辖区开展业务。这实际上正在发生。

最后，在本章开始时，介绍Token时，我们将Token的口语意义解释为“微不足道的价值”。大多数Token的价值微不足道的根本原因是因为它们只能用在非常狭窄的环境中：一家巴士公司，一家洗衣店，一家商场，一家酒店，一家公司商店。流动性有限，适用性有限，转换成本高，一路降低Token的价值，直到它只有“Token”那么小的价值。因此，当你将实用Token添加到你的平台上，但该Token只能在你自己的一个平台上使用且市场很小时，则会重新创建使物理Token毫无价值的条件。如果为了使用你的平台，用户必须将某些东西转换为你的实用Token，使用它，然后将其余部分再转换回更普遍有用的东西，你实际是创建了公司凭证。数字Token的转换成本比没有市场的物理Token低了几个数量级，但转换成本并不是零。在整个行业中工作的实用Token将非常有趣并且可能非常有价值。但是，如果你将创业公司设定为必须引导整个行业标准才能成功，那么你可能已经失败了。

在像以太坊这样的通用平台上部署服务的好处之一就是能够连接智能合约，增加流动性和Token效用的潜力。

为了正确的理由做出这个决定。采用Token是因为你的应用程序\_不使用Token无法工作\_ （例如以太坊）。采用它是因为Token解决了基本的市场障碍或访问问题。不要因为这是你可以快速筹集资金的唯一方式而引入实用Token，你需要假装它不是公开发行的证券。

#### Token 标准 <a href="#user-content-token_std" id="user-content-token_std"></a>

区块链标记在以太坊之前就已存在。在某些方面，第一块区块链货币比特币本身就是一种Token。在Ethereum之前，还在比特币和其他加密货币上开发了许多Token平台。然而，在以太坊上引入第一个Token标准导致Token爆炸。

Vitalik Buterin建议将Token作为通用可编程区块链（如以太坊）最明显和最有用的应用之一。事实上，在以太坊的第一年，经常看到Vitalik和其他人穿着印有Ethereum标志的T恤和背面的智能合约样本。这件T恤有几种变化，但最常见的是一种Token的实现。

**ERC20 Token 标准**

第一个标准由Fabian Vogelsteller于2015年11月引入，作为以太坊征求意见（ERC）。它被自动分配了GitHub发行号码20，从而获得了名字“ERC20 Token”。绝大多数Token目前都基于ERC20。ERC20征求意见最终成为以太坊改进建议EIP20，但大多仍以原名ERC20提及。你可以在这里阅读标准：

ERC20是\_可替换Token\_的标准，意味着ERC20标记的不同单元是可互换的，没有唯一属性。

ERC20标准为实现Token的合同定义了一个通用接口，这样任何兼容的Token都可以以相同的方式访问和使用。该接口包含许多必须存在于标准的每个实现中的函数，以及可能由开发人员添加的一些可选函数和属性。

**ERC20 必须的函数和事件**

totalSupply

返回当前存在的Token的总单位。ERC20Token可以有固定或可变的供应量。

balanceOf

给定一个地址，返回该地址的Token余额。

transfer

给定一个地址和数量，将该数量的Tokens从执行该方法的地址的余额转移到该地址。

transferFrom

给定发送者，接收人和数量，将Token从一个帐户转移到另一个帐户。与+approve+结合使用。

approve

在给定接收者地址和数量的情况下，授权该地址从发布批准的帐户执行多次转账，直到到达指定的数量。

allowance

给定一个所有者地址和一个消费者地址，返回该消费者被批准从所有者的取款的剩余金额。

Transfer event

成功转移时触发的事件（调用+transfer+或+transferFrom+）（即使对于零值转移）。

Approval event

成功调用+approve+时记录的事件。

**ERC20 可选函数**

name

返回Token的可读名称（例如“US Dollars”）。

symbol

返回Token的人类可读符号（例如“USD”）。

decimals

返回用于分割Token数量的小数位数。例如，如果小数为2，则将Token数除以100以获取其用户表示。

**在Solidity中定义的ERC20接口**

以下是在Solidity中ERC20接口规范的样子：

```
contract ERC20 {
   function totalSupply() constant returns (uint theTotalSupply);
   function balanceOf(address _owner) constant returns (uint balance);
   function transfer(address _to, uint _value) returns (bool success);
   function transferFrom(address _from, address _to, uint _value) returns (bool success);
   function approve(address _spender, uint _value) returns (bool success);
   function allowance(address _owner, address _spender) constant returns (uint remaining);
   event Transfer(address indexed _from, address indexed _to, uint _value);
   event Approval(address indexed _owner, address indexed _spender, uint _value);
}
```

**ERC20 数据结构**

如果你检查任何ERC20实现，它将包含两个数据结构，一个用于追踪余额，另一个用于追踪配额（allowances）。在Solidity中，它们使用\_data mapping\_实现。

第一个data mapping按拥有者实现了Token余额的内部表。这允许Token合约跟踪谁拥有Token。每次转账都是从一个余额中扣除的，并且是对另一个余额的增加。

Balances: a mapping from address (owner) to amount (balance)

```
mapping(address => uint256) balances;
```

第二个数据结构是配额的data mapping。正如我们将在[ERC20工作流程：“transfer”和“approve & transferFrom”](broken-reference)中看到的那样，使用ERC20Token，Token的所有者可以将权限委托给花钱者，允许他们从所有者的余额中花费特定金额（配额）。ERC20合同通过二维映射追踪配额，主关键字是Token所有者的地址，映射到一个花费者地址和配额金额：

Allowances: a mapping from address (owner) to address (spender) to amount (allowance)

```
mapping (address => mapping (address => uint256)) public allowed;
```

**ERC20工作流程：“transfer”和“approve & transferFrom”**

ERC20Token标准具有两种传输功能。你可能想知道为什么？

ERC20允许两种不同的工作流程。第一个是使用+transfer+函数的单次交易，简单的工作流程。这个工作流程是钱包用来将Token发送给其他钱包的工作流程。绝大多数Token交易都发生在+transfer+工作流程中。

执行转让合同非常简单。如果爱丽丝希望向鲍勃发送10个Token，她的钱包会向Token合约的地址发送一个交易，并用Bob的地址和“10”作为参数调用+transfer+函数。Token合约调整Alice的余额（-10）和Bob的余额（+10）并发出+Transfer+事件。

第二个工作流程是使用+approve+和+transferFrom+的双交易工作流程。该工作流程允许Token所有者将其控制权委托给另一个地址。它通常用于委托控制权给合约来分配Token，但它也可以被交易所使用。例如，如果一家公司为ICO出售Token，他们可以+approve+一个crowdsale合同地址来分发一定数量的Token。然后crowdsale合同可以用+transferFrom+转移给Token的每个买家。



Figure 1. The two-step approve & transferFrom workflow of ERC20 Tokens

对于 approve & transferFrom 工作流程，需要两个交易。假设Alice希望允许AliceICO合同将所有AliceCoin Token的50％卖给像Bob和Charlie这样的买方。首先，Alice发布AliceCoin ERC20合同，将所有AliceCoin发放到她自己的地址。然后，Alice发布可以以ether出售Token的AliceICO合同。接下来，Alice启动+approve & transferFrom+工作流程。她向AliceCoin发送一个交易，调用+approve+，参数是AliceICO的地址和+totalSupply+的50％。这将触发+Approval+事件。现在，AliceICO合同可以出售AliceCoin了。

当AliceICO从Bob那收到ether，它需要发送一些AliceCoin给Bob作为回报。在AliceICO合约内是AliceCoin和ether之间的汇率。Alice在创建AliceICO时设置的汇率决定了Bob将根据他发送给AliceICO的ether数量能得到多少Token。当AliceICO调用AliceCoin transferFrom+函数时，它将Alice的地址设置为发送者，将Bob的地址设置为接收者，并使用汇率来确定将在“value”字段中将多少AliceCoin Token传送给Bob。AliceCoin合同将余额从Alice的地址转移到Bob的地址并触发 +Transfer 事件。只要不超过Alice设定的审批限制，AliceICO合同可以调用 transferFrom 无限次数。AliceICO合同可以通过调用+allowance+函数来跟踪它能卖出多少AliceCoinToken。

**ERC20 实现**

虽然可以在约三十行Solidity代码中实现兼容ERC20的Token，但大多数实现都更加复杂，以解决潜在的安全漏洞。在EIP20标准中提到了两种实现：

Consensys EIP20

简单易读的ERC20兼容Token的实现。

OpenZeppelin StandardToken

此实现与ERC20兼容，并具有额外的安全防范措施。它构成了OpenZeppelin库的基础，实现了更复杂的与ERC20兼容的Token，包括筹款上限，拍卖，归属时间表和其他功能。

**发布我们自己的ERC20Token**

让我们创建并发布我们自己的Token。在这个例子中，我们将使用+truffle+ 框架（参见[\[truffle\]](broken-reference)）。该示例假设你已经安装了+truffle+，进行了配置，并熟悉其基本操作。

我们将称之为“Mastering Ethereum Token”，标志为“MET”。

首先，让我们创建并初始化一个Truffle项目目录，就像我们在[\[truffle\_project\_directory\]](broken-reference)中所做的那样。运行这四个命令并接受任何问题的默认答案：

```
$ mkdir METoken
$ cd METoken
METoken $ truffle init
METoken $ npm init
```

你现在应该具有以下目录结构：

```
METoken/
├── contracts
│   └── Migrations.sol
├── migrations
│   └── 1_initial_migration.js
├── package.json
├── test
├── truffle-config.js
└── truffle.js
```

编辑+truffle.js+或+truffle-config.js+配置文件以设置+Truffle+环境，或复制我们使用的环境：

如果使用示例+truffle-config.js+，请记住在包含你的测试私钥的+METoken+文件夹中创建文件+.env+，以便在公共以太网测试网络（如ganache或Kovan）上进行测试和部署。你可以从MetaMask中导出你的测试网络私钥。

之后你的目录看起来像：

```
METoken/
├── contracts
│   └── Migrations.sol
├── migrations
│   └── 1_initial_migration.js
├── package.json
├── test
├── truffle-config.js
├── truffle.js
└── .env *new file*
```

| Warning | 只能使用不用于在以太坊主网络上持有资金的测试密钥或测试助记符。切勿使用持有真正金钱的钥匙进行测试。 |
| ------- | ------------------------------------------------- |

对于我们的示例，我们将导入OpenZeppelin StandardContract，它实现了一些重要的安全检查并且易于扩展。让我们导入该库：

```
$ npm install zeppelin-solidity

+ zeppelin-solidity@1.6.0
added 8 packages in 2.504s
```

\+ zeppelin-solidity 包将在 node\_modules +目录下添加约250个文件。OpenZeppelin库包含的不仅仅是ERC20Token，但我们只使用它的一小部分。

接下来，让我们编写我们的Token合约。创建一个新文件+METoken.sol+并从GitHub复制示例代码：

我们的合同非常简单，因为它继承了OpenZeppelin StandardToken库的所有功能：

METoken.sol : A Solidity contract implementing an ERC20 Token

```
link:code/METoken/contracts/METoken.sol[]
```

在这里，我们定义可选变量+name+，symbol+和+decimals。我们还定义了一个+\_initial\_supply+变量，设置为2,100万个Token，以及两个小数细分（总共21亿）。在契约的初始化（构造函数）函数中，我们将+totalSupply+设置为等于+\_initial\_supply+，并将所有+\_initial\_supply+分配给创建 METoken 契约的帐户余额（msg.sender）。

我们现在使用+truffle+编译+METoken+代码：

```
$ truffle compile
Compiling ./contracts/METoken.sol...
Compiling ./contracts/Migrations.sol...
Compiling zeppelin-solidity/contracts/math/SafeMath.sol...
Compiling zeppelin-solidity/contracts/Token/ERC20/BasicToken.sol...
Compiling zeppelin-solidity/contracts/Token/ERC20/ERC20.sol...
Compiling zeppelin-solidity/contracts/Token/ERC20/ERC20Basic.sol...
Compiling zeppelin-solidity/contracts/Token/ERC20/StandardToken.sol...
```

如你所见，+truffle+包含了OpenZeppelin库的必要依赖关系，并编译了这些契约。

我们建立一个migration脚本，部署 METoken+合约。在+METoken/migrations+文件夹中创建一个新文件+2\_deploy\_contracts.js。从Github存储库中的示例复制内容：

以下是它包含的内容：

2\_deploy\_contracts: Migration to deploy METoken

```
link:code/METoken/migrations/2_deploy_contracts.js[]

var METoken = artifacts.require("METoken");

module.exports = function(deployer) {
  // Deploy the METoken contract as our only task
  deployer.deploy(METoken);
};
```

在我们部署其中一个以太坊测试网络之前，让我们开始一个本地区块链来测试一切。正如我们在[\[using\_ganache\]](broken-reference)中所做的那样，从 ganache-cli 的命令行或从图形用户界面启动 ganache 区块链。

一旦 ganache 启动，我们就可以部署我们的METoken合约，看看是否一切都按预期工作：

```
$ truffle migrate --network ganache
Using network 'ganache'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0xb2e90a056dc6ad8e654683921fc613c796a03b89df6760ec1db1084ea4a084eb
  Migrations: 0x8cdaf0cd259887258bc13a92c0a6da92698644c0
Saving successful migration to network...
  ... 0xd7bc86d31bee32fa3988f1c1eabce403a1b5d570340a3a9cdba53a472ee8c956
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying METoken...
  ... 0xbe9290d59678b412e60ed6aefedb17364f4ad2977cfb2076b9b8ad415c5dc9f0
  METoken: 0x345ca3e014aaf5dca488057592ee47305d9b3e10
Saving successful migration to network...
  ... 0xf36163615f41ef7ed8f4a8f192149a0bf633fe1a2398ce001bf44c43dc7bdda0
Saving artifacts...
```

在+ganache+控制台上，我们应该看到我们的部署创建了4个新的交易：



Figure 2. METoken deployment on Ganache

**使用Truffle控制台与METoken交互**

我们可以使用+Truffle控制台+与我们的+ganache+区块链合同进行互动。这是一个交互式的JavaScript环境，可以访问Truffle环境，并通过Web3访问区块链。在这种情况下，我们将+Truffle控制台+连接到+ganache+区块链：

```
$ truffle console --network ganache
truffle(ganache)>
```

```
+truffle(ganache)>+ 提示符表明我们已连接到 +ganache+区块链并准备输入我们的命令。+Truffle控制台+支持所有的Truffle命令，所以我们可以从控制台+compile+和+migrate+。我们已经运行过这些命令，所以让我们直接看看合同本身。METoken合约作为Truffle环境内的JavaScript对象存在。在提示符下键入+METoken+，它将转储整个合约定义：
```

```
truffle(ganache)> METoken
{ [Function: TruffleContract]
  _static_methods:

[...]

currentProvider:
 HttpProvider {
   host: 'http://localhost:7545',
   timeout: 0,
   user: undefined,
   password: undefined,
   headers: undefined,
   send: [Function],
   sendAsync: [Function],
   _alreadyWrapped: true },
network_id: '5777' }
```

\+METoken+对象还公开几个属性，例如合同的地址（由+migrate+命令部署）：

```
truffle(ganache)> METoken.address
'0x345ca3e014aaf5dca488057592ee47305d9b3e10'
```

如果我们想要与已部署的合同进行交互，我们必须以JavaScript“promise”的形式使用异步调用。我们使用+deployment+函数来获取合约实例，然后调用+totalSupply+函数：

```
truffle(ganache)> METoken.deployed().then(instance => instance.totalSupply())
BigNumber { s: 1, e: 9, c: [ 2100000000 ] }
```

接下来，让我们使用由+ganache+创建的账户来检查我们的METoken余额并将一些METoken发送到另一个地址。首先，让我们获取帐户地址：

```
truffle(ganache)> let accounts
undefined
truffle(ganache)> web3.eth.getAccounts((err,res) => { accounts = res })
undefined
truffle(ganache)> accounts[0]
'0x627306090abab3a6e1400e9345bc60c78a8bef57'
```

accounts 列表现在包含由+ganache+创建的所有帐户，而+account\[0]+是部署了该METoken合约的帐户。它应该有METoken的余额，因为我们的METoken构造函数将全部Token提供给了创建它的地址。让我们检查：

```
truffle(ganache)> METoken.deployed().then(instance => { instance.balanceOf(accounts[0]).then(console.log) })
undefined
BigNumber { s: 1, e: 9, c: [ 2100000000 ] }
```

最后，通过调用合约的 transfer+函数，让我们从+account\[0] 向 account\[1] 转移1000.00 METoken：

```
truffle(ganache)> METoken.deployed().then(instance => { instance.transfer(accounts[1], 100000) })
undefined
truffle(ganache)> METoken.deployed().then(instance => { instance.balanceOf(accounts[0]).then(console.log) })
undefined
truffle(ganache)> BigNumber { s: 1, e: 9, c: [ 2099900000 ] }

undefined
truffle(ganache)> METoken.deployed().then(instance => { instance.balanceOf(accounts[1]).then(console.log) })
undefined
truffle(ganache)> BigNumber { s: 1, e: 5, c: [ 100000 ] }
```

| Tip | METoken具有2位精度的小数，这意味着1个METoken在合同中是100个单位。当我们传输1000个METoken时，我们在传输函数中将该值指定为100,000。 |
| --- | ----------------------------------------------------------------------------------- |

如你所见，在控制台中，+ account \[0] 现在拥有20,999,000 MET， account \[1] +拥有1000 MET。

如果切换到+ganache+图形用户界面，你将看到名为+transfer+函数的交易：



Figure 3. METoken transfer on Ganache

**将ERC20Token发送到合同地址**

到目前为止，我们已经设置了ERC20Token并从一个帐户转移到另一个帐户。我们用于这些示范的所有账户都是外部拥有账户（EOAs），这意味着它们由私钥控制，而不是合同。如果我们将MET发送到合同地址会发生什么？让我们看看！

首先，我们将其他合约部署到我们的测试环境中。对于这个例子，我们将使用我们的第一个合同+Faucet.sol+。我们将它添加到METoken项目中，方法是将它复制到+contracts+目录。我们的目录应该是这样的：

```
METoken/
├── contracts
│   ├── Faucet.sol
│   ├── METoken.sol
│   └── Migrations.sol
```

我们还会添加一个migration，从+METoken+单独部署+Faucet+：

```
var Faucet = artifacts.require("Faucet");

module.exports = function(deployer) {
  // Deploy the Faucet contract as our only task
  deployer.deploy(Faucet);
};
```

让我们从Truffle控制台编译和迁移合同：

```
$ truffle console --network ganache
truffle(ganache)> compile
Compiling ./contracts/Faucet.sol...
Writing artifacts to ./build/contracts

truffle(ganache)> migrate
Using network 'ganache'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x89f6a7bd2a596829c60a483ec99665c7af71e68c77a417fab503c394fcd7a0c9
  Migrations: 0xa1ccce36fb823810e729dce293b75f40fb6ea9c9
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Replacing METoken...
  ... 0x28d0da26f48765f67e133e99dd275fac6a25fdfec6594060fd1a0e09a99b44ba
  METoken: 0x7d6bf9d5914d37bcba9d46df7107e71c59f3791f
Saving artifacts...
Running migration: 3_deploy_faucet.js
  Deploying Faucet...
  ... 0x6fbf283bcc97d7c52d92fd91f6ac02d565f5fded483a6a0f824f66edc6fa90c3
  Faucet: 0xb18a42e9468f7f1342fa3c329ec339f254bc7524
Saving artifacts...
```

现在让我们将一些MET发送到 Faucet 合约：

```
truffle(ganache)> METoken.deployed().then(instance => { instance.transfer(Faucet.address, 100000) })
truffle(ganache)> METoken.deployed().then(instance => { instance.balanceOf(Faucet.address).then(console.log)})
truffle(ganache)> BigNumber { s: 1, e: 5, c: [ 100000 ] }
```

好的，我们已将1000 MET转移到 Faucet+合约。现在，我们如何从 +Faucet 提款呢？

请记住，Faucet.sol+是一个非常简单的合同。它只有一个功能，+withdraw，这是提取\_ether\_。它没有提取MET或任何其他ERC20Token的功能。如果我们使用+withdraw+它将尝试发送ether，但由于Faucet还没有ether的余额，它将失败。

METoken+合约知道+Faucet+有余额，但它可以转移该余额的唯一方法是它从合约地址收到+transfer+调用。无论如何，我们需要让+Faucet 合约调用+MET+中的+transfer+函数。

如果你在思考下一步该做什么，不必了。这个问题没有解决办法。MET发送到+Faucet+将永远卡住。只有+Faucet+合约可以转让它，+Faucet+合约没有调用ERC20Token合约的+transfer+函数的代码。

也许你预料到了这个问题。最有可能的是，你没有。实际上，数百名以太坊用户也无意将各种Token转让给没有任何ERC20能力的合同。据估计，价值超过250万美元的Token被这样“卡住”，并且永远丢失。

ERC20Token的用户可能无意中在转移中丢失其Token的方式之一是当他们尝试转移到交易所或其他服务时。他们从交易所的网站上复制以太坊地址，认为他们可以简单地向其发送Token。但是，许多交易所都公布实际上是合同的接收地址！这些合同具有许多不同的功能，通常将发送给他们的所有资金清扫到“冷存储”或另一个集中的钱包。尽管有许多警告说“不要将Token发送到这个地址”，但许多Token会以这种方式丢失。

**演示 approve & transferFrom 流程**

我们的+Faucet+合同无法处理ERC20Token。使用+transfer+函数发送Token给它，会导致这些Token的丢失。我们重写合同，并处理ERC20Token。具体来说，我们将把它变成一个Faucet，将MET发给任何询问的人。

对于这个例子，我们制作了Truffle项目目录的副本，将其称为 METoken\_METFaucet，初始化Truffle，npm，安装OpenZeppelin依赖项并复制+METoken.sol+合同。有关详细说明，请参阅我们的第一个示例[发布我们自己的ERC20Token](broken-reference)。

现在，让我们创建一个新的Faucet合同，称之为+METFaucet.sol+。它看起来像这样：

METFaucet.sol: a faucet for METoken

```
include::code/METoken_METFaucet/contracts/METFaucet.sol

// Version of Solidity compiler this program was written for
pragma solidity ^0.4.19;

import 'zeppelin-solidity/contracts/Token/ERC20/StandardToken.sol';


// A faucet for ERC20 Token MET
contract METFaucet {

	StandardToken public METoken;
	address public METOwner;

	// METFaucet constructor, provide the address of METoken contract and
	// the owner address we will be approved to transferFrom
	function METFaucet(address _METoken, address _METOwner) public {

		// Initialize the METoken from the address provided
		METoken = StandardToken(_METoken);
		METOwner = _METOwner;
	}

	function withdraw(uint withdraw_amount) public {

    	// Limit withdrawal amount to 10 MET
    	require(withdraw_amount <= 1000);

		// Use the transferFrom function of METoken
		METoken.transferFrom(METOwner, msg.sender, withdraw_amount);
    }

	// REJECT any incoming ether
	function () public payable { revert(); }

}
```

我们对基本的Faucet示例做了很多改动。由于METFaucet将使用+METoken+中的+transferFrom+函数，它将需要两个额外的变量。其中一个将保存已部署的+METoken+合约地址。另一个将持有MET所有者的地址，他们将提供Faucet提款的批准。+METFaucet+将调用+METoken.transferFrom+并指示它将MET从所有者移至Faucet提取请求所来自的地址。

我们在这里声明这两个变量：

```
StandardToken public METoken;
address public METOwner;
```

由于我们的Faucet需要使用+METoken+和+METOwner+的正确地址进行初始化，因此我们需要声明一个自定义构造函数：

```
// METFaucet constructor, provide the address of METoken contract and
// the owner address we will be approved to transferFrom
function METFaucet(address _METoken, address _METOwner) public {

	// Initialize the METoken from the address provided
	METoken = StandardToken(_METoken);
	METOwner = _METOwner;
}
```

下一个改变是+withdraw+函数。METFaucet+使用+METoken+中的+transferFrom+函数，并要求+METoken+将MET传输给Faucet的接收者，而不是调用+transfer。

```
// Use the transferFrom function of METoken
METoken.transferFrom(METOwner, msg.sender, withdraw_amount);
```

最后，由于我们的Faucet不再发送ether，我们应该阻止任何人将ether送到+METFaucet+，因为我们不希望它被卡住。我们更改fallback函数以拒绝发进来的ether，使用+revert+功能还原任何收款：

```
// REJECT any incoming ether
function () public payable { revert(); }
```

现在我们的+METFaucet.sol+代码已准备就绪，我们需要修改migration脚本来部署它。这个migration脚本会有点复杂，因为+METFaucet+依赖于+METoken+的地址。我们将使用JavaScript promise按顺序部署这两个合约。创建+2\_deply\_contracts.js+，如下所示：

\[\[2\_deploy\_contracts]]

```
var METoken = artifacts.require("METoken");
var METFaucet = artifacts.require("METFaucet");
var owner = web3.eth.accounts[0];

module.exports = function(deployer) {

	// Deploy the METoken contract first
	deployer.deploy(METoken, {from: owner}).then(function() {
		// then deploy METFaucet and pass the address of METoken
		// and the address of the owner of all the MET who will approve METFaucet
		return deployer.deploy(METFaucet, METoken.address, owner);
  	});
}
```

现在，我们可以测试Truffle控制台中的所有内容。首先，我们使用+migrate+来部署合同。当+METoken+部署时，它会将所有MET分配给创建它的帐户，web3.eth.accounts\[0]。然后，我们在METoken中调用+approve+函数来批准+METFaucet+代表+web3.eth.accounts\[0]+发送1000 MET。最后，为了测试我们的Faucet，我们从+web3.eth.accounts\[1]+调用+METFaucet.withdraw+并尝试提取10个MET。以下是控制台命令：

```
$ truffle console --network ganache
truffle(ganache)> migrate
Using network 'ganache'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x79352b43e18cc46b023a779e9a0d16b30f127bfa40266c02f9871d63c26542c7
  Migrations: 0xaa588d3737b611bafd7bd713445b314bd453a5c8
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Replacing METoken...
  ... 0xc42a57f22cddf95f6f8c19d794c8af3b2491f568b38b96fef15b13b6e8bfff21
  METoken: 0xf204a4ef082f5c04bb89f7d5e6568b796096735a
  Replacing METFaucet...
  ... 0xd9615cae2fa4f1e8a377de87f86162832cf4d31098779e6e00df1ae7f1b7f864
  METFaucet: 0x75c35c980c0d37ef46df04d31a140b65503c0eed
Saving artifacts...
truffle(ganache)> METoken.deployed().then(instance => { instance.approve(METFaucet.address, 100000) })
truffle(ganache)> METoken.deployed().then(instance => { instance.balanceOf(web3.eth.accounts[1]).then(console.log) })
truffle(ganache)> BigNumber { s: 1, e: 0, c: [ 0 ] }
truffle(ganache)> METFaucet.deployed().then(instance => { instance.withdraw(1000, {from:web3.eth.accounts[1]}) } )
truffle(ganache)> METoken.deployed().then(instance => { instance.balanceOf(web3.eth.accounts[1]).then(console.log) })
truffle(ganache)> BigNumber { s: 1, e: 3, c: [ 1000 ] }
```

从结果中可以看出，我们可以使用 approve and transferFrom 工作流来授权一个合约转移另一个Token中定义的Token。如果使用得当，ERC20Token可以由EOA和其他合同使用。

但是，正确管理ERC20Token的负担会推送到用户界面。如果用户错误地尝试将ERC20Token转移到合同地址，并且该合同没有配备接收ERC20Token的功能，则Token将丢失。

**ERC20Token的问题**

ERC20Token标准的采用确实是爆炸性的。成千上万的Token已经启动，既可以尝试新的功能，也可以通过各种“众筹”拍卖和初始投币产品（ICO）筹集资金。然而，正如我们在将Token转移到合同地址的问题所看到的那样，存在一些潜在的陷阱。

ERC20Token不太明显的问题之一是它们暴露了Token和ether本身之间的细微差别。如果ether通过以接收者地址为目的地的交易转移，则Token转移发生在 _specific Token contract state_ 中，并且将Token合同作为其目的地，而不是接收者的地址。Token合同跟踪余额并发布事件。在Token传输中，实际上没有交易发送给Token的接收者。相反，接收者的地址将被添加到Token合约本身的映射中。将ether发送到地址的交易会改变地址的状态。将Token转移到地址的交易只会改变Token合约的状态，而不会改变接收者地址的状态。即使是支持ERC20Token的钱包，也不会意识到Token的余额，除非用户明确将特定Token合约添加到“监视”中。一些钱包观察最受欢迎的Token合约，以检测由他们控制的地址持有的余额，但这仅限于ERC20合同的一小部分。

事实上，用户不太可能会追踪所有可能的ERC20Token合约中的所有余额。许多ERC20Token更像是垃圾邮件，而不是可用的Token。他们自动为拥有ether活动的帐户创建余额，以吸引用户。如果你有一个活动历史悠久的以太坊地址，特别是如果它是在预售中创建的，你会发现它充满了凭空出现的“垃圾”Tokens。当然，这个地址并不是真的充满了Token，而是那些Token合约有你的地址。如果你用于查看地址的资源管理器或钱包正在监视这些Token合约，才能看到这些余额。

Token不像ether。Ether通过+send+功能发送，并由合同中的任何payable函数或任何EOA接受。Token仅使用在ERC20合同中存在的+transfer+ 或+approve＆transferFrom+函数发送，并且不会（至少在ERC20中）触发收款合同中的任何payable函数。Token的功能就像ether这样的加密货币，但它们带有一些细微的区别，可以打破这种错觉。

考虑另一个问题。要发送ether，或使用任何以太坊合同，你需要ether来支付gas。发送Token，你\_也需要ether\_。你无法用Token支付交易的gas，而Token合同也无法为你支付gas费用。这可能会导致一些相当奇怪的用户体验。例如，假设你使用交易所或Shapeshift将某些比特币转换为Token。你在钱包中“收到”该Token，该钱包会跟踪该Token的合同并显示你的余额。它看起来与你钱包中的任何其他加密货币相同。现在尝试发送Token，你的钱包会通知你，你需要ether才能这样做。你可能会感到困惑 - 毕竟你不需要ether接收Token。也许你没有ether。也许你甚至不知道该Token是以太坊上的ERC20Token，也许你认为这是一个拥有自己的区块链的加密货币。错觉就这样被打破了。

其中一些问题是ERC20Token特有的。其他更一般的问题涉及到以太坊内的抽象和界面边界。有些可以通过更改Token接口来解决，其他可能需要更改以太坊内的基础结构（例如EOAs和合同之间以及交易和消息之间的区别）。有些可能不完全“可解决”，并且可能需要用户界面设计来隐藏细微差别并使用户体验一致，而不管其底层区别如何。

在接下来的部分中，我们将看看试图解决其中一些问题的各种提案。

**ERC223 - 一种建议的Token合同接口标准**

ERC223提案试图通过检测目的地地址是否是合同来解决无意中将Token转移到合同（可能支持或不支持Token）的问题。ERC223要求用于接受Token的契约实现名为+TokenFallback+的函数。如果传输的目的地是合同并且合同不支持Token（即不实现+TokenFallback+），则传输失败。

为了检测目标地址是否为契约，ERC223参考实现使用了一小段内联字节码，并采用了一种颇具创造性的方式：

```
function isContract(address _addr) private view returns (bool is_contract) {
	uint length;
	assembly {
		  //retrieve the size of the code on target address, this needs assembly
		  length := extcodesize(_addr)
	}
	return (length>0);
}
```

你可以在这里看到有关ERC223提案的讨论：

ERC223合同接口规范是：

```
interface ERC223Token {
  uint public totalSupply;
  function balanceOf(address who) public view returns (uint);

  function name() public view returns (string _name);
  function symbol() public view returns (string _symbol);
  function decimals() public view returns (uint8 _decimals);
  function totalSupply() public view returns (uint256 _supply);

  function transfer(address to, uint value) public returns (bool ok);
  function transfer(address to, uint value, bytes data) public returns (bool ok);
  function transfer(address to, uint value, bytes data, string custom_fallback) public returns (bool ok);

  event Transfer(address indexed from, address indexed to, uint value, bytes indexed data);
}
```

ERC223没有得到广泛的实施，ERC讨论中有一些关于向前兼容性和在合同接口级别或用户界面上实现更改之间的折衷的争论。争论仍在继续。

**ERC777 - 一种建议的Token合同接口标准**

另一项改进Token合同标准的提案是ERC777。该提案有几个目标，包括：

* 提供ERC20兼容性界面
* 使用+send+功能传输Token，类似于ether传输
* 与ERC820兼容Token合同注册
* 合同和地址可以通过在发送之前调用+TokensToSend+函数来控制它们发送的Token
* 通过在接收者中调用+TokensReceived+函数来通知合同和地址
* Token传输交易包含 userData 和 operatorData 字段中的元数据
* 无论是发送到合同还是EOA，都以相同的方式运作

有关ERC777的详细信息和正在进行的讨论可以在这里找到：

ERC777合同接口规范是：

```
interface ERC777Token {
    function name() public constant returns (string);
    function symbol() public constant returns (string);
    function totalSupply() public constant returns (uint256);
    function granularity() public constant returns (uint256);
    function balanceOf(address owner) public constant returns (uint256);

    function send(address to, uint256 amount) public;
    function send(address to, uint256 amount, bytes userData) public;

    function authorizeOperator(address operator) public;
    function revokeOperator(address operator) public;
    function isOperatorFor(address operator, address TokenHolder) public constant returns (bool);
    function operatorSend(address from, address to, uint256 amount, bytes userData, bytes operatorData) public;

    event Sent(address indexed operator, address indexed from, address indexed to, uint256 amount, bytes userData, bytes operatorData);
    event Minted(address indexed operator, address indexed to, uint256 amount, bytes operatorData);
    event Burned(address indexed operator, address indexed from, uint256 amount, bytes userData, bytes operatorData);
    event AuthorizedOperator(address indexed operator, address indexed TokenHolder);
    event RevokedOperator(address indexed operator, address indexed TokenHolder);
}
```

ERC777的参考实现与提案相关联。ERC777依赖于ERC820中关于注册合同的并行提案。关于ERC777的一些争论是关于同时采用两个大变化的复杂性：一个新的Token标准和一个注册标准。讨论仍在继续。

**ERC721 - 不可替代的Token（契据）标准**

我们目前看到的所有Token标准都是\_可互换\_Token，这意味着Token的每个单元都是完全可以互换的。ERC20Token标准仅跟踪每个帐户的最终余额，并且（明确地）跟踪任何Token的出处。

ERC721提案是\_不可互换的\_ Tokens标准，也称为\_契据\_ _deeds_。

牛津词典：

```
契约：签署和交付的法律文件，尤其是关于财产或合法权利所有权的法律文件。
```

契约一词的使用旨在反映“财产所有权”部分，即使这些部分在任何司法管辖区都不被承认为“法律文件”，至少目前不是。

不可互换的Token追踪独特事物的所有权。拥有的东西可以是数字项目，例如游戏物品或数字收藏品。或者，这种东西可以是物理事物，其物主通过Token进行跟踪，例如房屋，汽车，艺术品等。契约也可以代表负值的东西，例如贷款（债务），留置权，地役权等。ERC721标准对所有权由契约追踪的事物的性质没有限制或期望，只是它可以是唯一标识，在这个标准的情况下是由256位标识符实现的。

标准和讨论的细节在两个不同的GitHub位置进行跟踪：

要掌握ERC20和ERC721之间的基本差异，只需查看ERC721中使用的内部数据结构即可：

```
// Mapping from deed ID to owner
mapping (uint256 => address) private deedOwner;
```

ERC20跟踪属于每个所有者的余额，所有者是映射的主键，ERC721跟踪每个契约ID以及谁拥有它，契约ID是映射的主键。从这个基本差异衍生出不可替代的Token的所有属性。

ERC721 合同接口规范是：

```
interface ERC721 /* is ERC165 */ {
    event Transfer(address indexed _from, address indexed _to, uint256 _deedId);
    event Approval(address indexed _owner, address indexed _approved, uint256 _deedId);
    event ApprovalForAll(address indexed _owner, address indexed _operator, bool _approved);

    function balanceOf(address _owner) external view returns (uint256 _balance);
    function ownerOf(uint256 _deedId) external view returns (address _owner);
    function transfer(address _to, uint256 _deedId) external payable;
    function transferFrom(address _from, address _to, uint256 _deedId) external payable;
    function approve(address _approved, uint256 _deedId) external payable;
    function setApprovalForAll(address _operateor, boolean _approved) payable;
    function supportsInterface(bytes4 interfaceID) external view returns (bool);
}
```

ERC721还支持两个\_\*可选\*\_接口，一个用于元数据，一个用于枚举契约和所有者。

用于元数据的ERC721可选接口是：

```
interface ERC721Metadata /* is ERC721 */ {
    function name() external pure returns (string _name);
    function symbol() external pure returns (string _symbol);
    function deedUri(uint256 _deedId) external view returns (string _deedUri);
}
```

用于枚举的ERC721可选接口是：

```
interface ERC721Enumerable /* is ERC721 */ {
    function totalSupply() external view returns (uint256 _count);
    function deedByIndex(uint256 _index) external view returns (uint256 _deedId);
    function countOfOwners() external view returns (uint256 _count);
    function ownerByIndex(uint256 _index) external view returns (address _owner);
    function deedOfOwnerByIndex(address _owner, uint256 _index) external view returns (uint256 _deedId);
}
```

#### Token标准 <a href="#user-content-token_std_review" id="user-content-token_std_review"></a>

在本节中，我们回顾几个建议的标准和几个广泛部署的Token合约标准。这些标准究竟做了什么？你应该使用这些标准吗？你应该如何使用它们？你应该添加超出这些标准的功能吗？你应该使用哪些标准？接下来我们将研究所有这些问题。

**什么是Token标准？他们的目的是什么？**

Token标准是实现的\_最小\_规范。这意味着为了符合ERC20的要求，你至少需要实施ERC20规定的功能和行为。你还可以通过实现不属于标准的功能来自由添加功能。

这些标准的主要目的是鼓励合同之间的互用性。因此，所有钱包，交易所，用户界面和其他基础设施组件都可以以可预见的方式与任何遵循规范的合同进行交流。

标准的目的是 _描述性的_ _descriptive_，而不是\_规定性的\_ _prescriptive_。你如何选择实现这些功能取决于你 - 合同的内部功能与标准无关。它们有一些功能要求，它们管理特定情况下的行为，但它们没有规定实现。例如，如果值设置为零，则传递函数的行为。

**你应该使用这些标准吗？**

鉴于所有这些标准，每个开发人员都面临两难选择：使用现有标准还是创新超出他们施加的限制？

这种困境并不容易解决。标准必然会限制你的创新能力，创造一个你必须遵循的狭窄“车辙”。另一方面，基本标准来自数百个应用程序的经验，并且通常与99％的用例非常吻合。

作为这一考虑的一部分，还有一个更大的问题：互操作性和广泛采用的价值。如果你选择使用现有标准，你将获得设计用于该标准的所有系统的价值。如果你选择偏离标准，则必须考虑自己构建所有基础架构的成本，或者说服其他人支持你新标准的实施。建立自己的道路并忽视现有标准的倾向被称为“Not Invented Here”，并且与开源文化相对立。另一方面，进步和创新有时依靠背离传统。这是一个棘手的选择，所以仔细考虑吧！

```
Not Invented Here是由社会，企业或机构文化采取的立场，由于其外部起源和成本（如版税），避免使用或购买已有产品，研究，标准或知识。
```

#### 安全成熟度 <a href="#user-content-security_maturity" id="user-content-security_maturity"></a>

除了标准的选择之外，还有\_implementation\_的并行选择。当你决定使用标准（如ERC20）时，你必须决定如何实施兼容Token。以太坊生态系统中广泛使用了一些现有的“参考”实现。或者你可以从头开始写你自己的。再次，这个选择代表了一个可能产生严重安全隐患的困境。

现有的实施是“战斗测试”。虽然不可能证明它们是安全的，但其中许多都支持数百万美元的Token。他们一再受到攻击，并且受到了强烈的攻击。到目前为止，没有发现重大的漏洞。写你自己的并不容易 - 有许多微妙的方式可以让合约受到损害。使用经过充分测试的广泛使用的实现更加安全。在我们上面的例子中，我们使用了ERC20标准的OpenZeppelin实现，因为这个实现从头到尾都是安全的。

如果你使用现有的实现，你也可以扩展它。再次小心这种冲动。复杂性是安全的敌人。你添加的每一行代码都会扩展合约的\_受攻击面\_，并可能代表处于等待状态的漏洞。你可能没有注意到一个问题，直到你在合同上投入了很多价值并且有人打破了它。

#### Token接口标准的扩展 <a href="#user-content-extend_token_interface" id="user-content-extend_token_interface"></a>

本节中讨论的Token标准以非常小的接口开始，功能有限。许多项目已经创建了扩展实现，以支持他们的应用程序所需的功能。其中一些包括：

所有者控制

特定地址或一组地址（多重签名）具有特殊功能，例如黑名单，白名单，铸造，恢复等。

燃烧

Token燃烧是指Token被转移到不可靠的地址或删除余额并减少供应时故意销毁。

Minting

以可预测的速率添加Token的总供应量的能力，或通过Token创建者的“命令”添加的能力。

Crowdfunding

提供Token销售的能力，例如通过拍卖，市场销售，反向拍卖等。

上限

总供给的预定义和不可改变的限制，与“minting”功能相反。

恢复“后门”

恢复资金，反向传输或拆除由指定地址或一组地址激活的Token（多重签名）的功能。

白名单

限制Token传输仅限于列出的地址的功能。在经过不同司法管辖区的规则审核后，最常用于向“经认可的投资者”提供Token。通常有一种更新白名单的机制。

黑名单

通过禁止特定地址来限制Token传输的能力。通常有更新黑名单的功能。

在OpenZeppelin库中有许多这些功能的参考实现。其中一些是面向特定用例的，仅在少数Token中实现。到目前为止，这些功能的接口还没有被广泛接受的标准。

如前所述，扩展具有附加功能的Token标准的决定代表了创新/风险与互操作性/安全性之间的权衡。

#### Tokens 和 ICOs <a href="#user-content-tokens_ico" id="user-content-tokens_ico"></a>

Token已经成为以太坊生态系统中的爆炸性发展。它们可能是所有智能合约平台（如以太坊）中非常重要的基础组件。

尽管如此，这些标准的重要性和未来影响不应该与当前Token产品的认可相混淆。就像在任何早期阶段的技术一样，第一波产品和公司几乎都会失败。今天在Ethereum上提供的许多Token几乎都是伪装的骗局，传销和金钱争夺。

诀窍是将这种技术的长期愿景和影响与可能非常大的Token ICO的短期泡沫区分开来，这种泡沫充斥着欺诈行为。两者在同一时间都可以是真实的。Token标准和平台将在目前的Token狂热中幸存下来，然后他们可能会改变世界。

