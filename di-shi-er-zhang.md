# 第十二章

### Oracles <a href="#user-content-oracles_chap" id="user-content-oracles_chap"></a>

以太坊虚拟机的一个关键属性是它能够以完全确定的方式执行智能合约字节码。EVM保证相同的操作将返回相同的输出，而不管它们实际运行的计算机。这一特性虽然是以太坊安全保证的关键，但它通过阻止智能合约检索和处理脱链数据来限制智能合约的功能。

但是，许多区块链应用程序需要访问外部信息。这就是\*oracles\*发挥作用的地方。可以将Oracles定义为离线数据的权威来源，允许智能合约使用外部信息接收和条件执行 - 它们可以被视为弥合链上链下之间鸿沟的机制。允许智能合约根据实际事件和数据强制执行合约关系，大大扩展了其范围。可能由oracles提供的数据示例包括：

* 来自物理来源的随机数/熵（例如量子/热现象）：公平地选择彩票智能合约中的赢家
* 与自然灾害相关的参数触发器：触发巨灾债券智能合约（对于飓风债券来说的风速）
* 汇率数据：将稳定币与法定货币准确挂钩
* 资本市场数据：代币化资产/证券的定价篮子
* 基准参考数据：将利率纳入智能金融衍生品
* 静态/伪静态数据：安全标识符，国家/地区代码，货币代码
* 时间和间隔数据：事件触发器以精确的SI时间测量为基础
* 天气数据：基于天气预报的保险费计算
* 政治事件：预测市场决议
* 体育赛事：预测市场决议和幻想体育合约
* 地理位置数据：供应链跟踪
* 损害赔偿：保险合约
* 其他区块链上发生的事件：互操作函数
* 交易天然气价格：gas价格oracles
* 航班延误：保险合约

在本节中，我们将在Solidity中检查oracles的主要功能，oracle订阅模式，计算oracles，去中心化的oracles和oracle客户端实现。

#### 主要功能 <a href="#user-content-primary_functions_sec" id="user-content-primary_functions_sec"></a>

实际上，oracle可以实现为链上智能合约系统和用于监控请求，检索和返回数据的离线基础设施。来自去中心化应用的数据请求通常是涉及许多步骤的异步过程。

首先，外部所有帐户将与去中心化应用进行交易，从而与oracle智能合约中定义的函数进行交互。此函数初始化对oracle的请求，除了可能包含回调函数和调度参数的补充信息之外，还使用相关参数详细说明所请求的数据。一旦验证了此事务，就可以将oracle请求视为oracle合约发出的EVM事件，或者状态更改； 参数可以被取出并用于从脱链数据源执行实际查询。oracle可能需要处理请求的费用，回调的gas费用，以及访问所请求数据的权限/权限。最后，结果数据由oracle所有者签署，基本上证明在给定时间数据的价值，并在交易中交付给作出请求的去中心化应用 - 直接或通过oracle合约。根据调度参数，oracle可以定期广播进一步更新数据的事务，例如日终定价信息。

可能有一系列替代方案。可以从外部所有帐户请求数据并直接返回数据，从而无需使用oracle智能合约。类似地，可以向物联网启用的硬件传感器发出请求和响应。因此，oracles可以是人类，软件或基于硬件的。

oracle的主要功能可概括如下：

* 回应去中心化应用的查询
* 解析查询
* 检查是否符合付款和数据权限/权利义务
* 从脱链源检索数据
* 在交易中签署数据
* 向网络广播交易
* 进一步安排交易

#### 订阅模式 <a href="#user-content-subscription_paterns_sec" id="user-content-subscription_paterns_sec"></a>

上述订阅模式是典型的请求——响应模式，常见于客户端——服务器体系结构中。虽然这是一种有用的消息传递模式，允许应用程序进行双向对话，但它是一种相对简单的模式，在某些条件下可能不合适。例如，需要oracle提供利率的智能债券可能需要在请求-响应模式下每天请求数据，以确保利率始终是正确的。鉴于利率不经常变化，发布——订阅模式在这里可能更合适，尤其是考虑到以太坊的有限带宽。

发布——订阅是一种模式，其中发布者，这里是oracles，不直接向接收者发送消息，而是将发布的消息分到不同的类中。订阅者能够表达对一个或多个类的兴趣并仅检索那些感兴趣的消息。在这种模式下，oracle可以将利率写入其自己的内部存储，当且仅当它发生变化时。多个订阅的去中心化应用可以简单地从oracle合约中读取它，从而减少对网络带宽的影响，同时最大限度地降低存储成本。

在广播或多播模式中，oracle会将所有消息发布到一个频道，订阅合约将在各种订阅模式下收听该频道。例如，oracle可能会将消息发布到加密货币汇率通道。订阅智能合约如果需要时间序列，例如移动平均计算，则可以请求信道的全部内容; 另一个可能只需要最后一个价格来计算现货价格。在oracle不需要知道订阅合约的身份的情况下，广播模式是合适的。

#### 数据认证 <a href="#user-content-data_authentication_sec" id="user-content-data_authentication_sec"></a>

如果我们假设去中心化应用查询的数据源既具有权威性又值得信赖，那么一个悬而未决的问题仍然存在：假设oracle和查询/响应机制可能由不同的实体操作，我们如何才能信任这种机制？数据在传输过程中可能会被篡改，因此脱链方法能够证明返回数据的完整性至关重要。数据认证的两种常用方法是真实性证明和可信执行环境（TEE）。

真实性证明是加密保证，证明数据未被篡改。基于各种证明技术（例如，数字签名证明），它们有效地将信任从数据载体转移到证明者，即证明方法的提供者。通过在链上验证真实性，智能合约能够在对其进行操作之前验证数据的完整性。Oraclize\[1]是利用各种真实性证明的oracle服务的一个例子。目前可用于以太坊主网络的数据查询是TLSNotary Proof \[2]。TLSNotary Proofs允许客户端向第三方提供客户端和服务器之间发生HTTPS Web流量的证据。虽然HTTPS本身是安全的，但它不支持数据签名。结果是，TLSNotary证明依赖于TLSNotary（通过PageSigner \[3]）签名。TLSNotary Proofs利用传输层安全性（TLS）协议，使得在访问数据后对数据进行签名的TLS主密钥在三方之间分配：服务器（oracle），受审核方（Oraclize）和核数师。Oraclize使用Amazon Web Services（AWS）虚拟机实例作为审核员，可以证明自它实例化以来未经修改\[4]。此AWS实例存储TLSNotary机密，允许其提供诚实证明。虽然它提供了比纯信任查询/响应机制更高的数据篡改保证，但这种方法确实需要假设亚马逊本身不会篡改VM实例。

TownCrier \[5,6]是基于可信执行环境的经过身份验证的数据馈送oracle系统; 这些方法采用不同的机制，利用基于硬件的安全区域来验证数据的完整性。TownCrier使用英特尔的SGX（Software Guard eXtensions）来确保HTTPS查询的响应可以被验证为可靠。SGX提供完整性保证，确保在安全区内运行的应用程序受到CPU的保护，防止任何其他进程被篡改。它还提供机密性，确保在安全区内运行时应用程序的状态对其他进程不透明。最后，SGX允许证明，通过生成数字签名的证据，证明应用程序 - 通过其构建的哈希安全地识别 - 实际上是在安全区内运行。通过验证此数字签名，去中心化式应用程序可以证明TownCrier实例在SGX安全区内安全运行。反过来，这证明实例没有被篡改，因此TownCrier发出的数据是真实的。机密性属性还允许TownCrier通过允许使用TownCrier实例的公钥加密数据查询来处理私有数据。通过在诸如SGX的安全区内运行oracle的查询/响应机制，可以有效地将其视为在受信任的第三方硬件上安全运行，确保所请求的数据被返回到未被禁用的状态（假设我们信任Intel/SGX）。

#### 计算 oracles <a href="#user-content-computation_oracles_sec" id="user-content-computation_oracles_sec"></a>

到目前为止，我们只是在请求和提供数据的背景下讨论了oracles。然而，oracles也可用于执行任意计算，这一功能在以太坊固有的区块gas限制和相对昂贵的计算成本的情况下特别有用; Vitalik本人指出，与现有的集中服务相比，以太坊的计算成本效率低了一百万倍\[7]。计算oracles可以用于对一组输入执行相关计算，而不是仅仅中继查询结果，并返回计算结果，这可能是在链上计算不可行的。例如，可以使用计算oracle执行计算密集型回归计算，以估计债券合约的收益率。

Oraclize提供的服务允许去中心化应用请求输出在沙盒AWS虚拟机中执行的计算。AWS实例从包含在上传到IPFS的存档中的用户配置的Dockerfile创建可执行容器。根据请求，Oraclize使用其哈希检索此存档，然后在AWS上初始化并执行Docker容器，将作为环境变量提供给应用程序的任何参数传递。容器化应用程序根据时间限制执行计算，并且必须将结果写入标准输出，Oraclize可以将其返回到去中心化应用。Oraclize目前在可审核的t2.micro AWS实例上提供此服务。

作为可验证的oracle真理的标准，“cryptlet”的概念已被正式化为Microsoft更广泛的ESC框架\[8]的一部分。Cryptlet在加密的封装内执行，该封装抽象出基础设施，例如I/O，并附加了CryptoDelegate，以便自动对传入和传出的消息进行签名，验证和验证。Cryptlet支持分布式事务，因此合约逻辑可以以ACID方式处理复杂的多步骤，多区块链和外部系统事务。这允许开发人员创建便携，隔离和私有的真相解决方案，以便在智能合约中使用。Cryptlet遵循以下格式：

```
public class SampleContractCryptlet : Cryptlet
  {
        public SampleContractCryptlet(Guid id, Guid bindingId, string name, string address, IContainerServices hostContainer, bool contract)
            : base(id, bindingId, name, address, hostContainer, contract)
        {
            MessageApi =
                new CryptletMessageApi(GetType().FullName, new SampleContractConstructor())
```

TrueBit \[9]是可扩展和可验证的离线计算的解决方案。它引入了一个求解器和验证器系统，分别执行计算和验证。如果解决方案受到挑战，则在链上执行对计算子集的迭代验证过程 - 一种“验证游戏”。游戏通过一系列循环进行，每个循环递归地检查计算的越来越小的子集。游戏最终进入最后一轮，挑战是微不足道的，以至于评委 - 以太坊矿工 - 可以对挑战是否合理，在链上进行最终裁决。实际上，TrueBit是一个计算市场的实现，允许去中心化应用支付可在网络外执行的可验证计算，但依靠以太坊来强制执行验证游戏的规则。理论上，这使无信任的智能合约能够安全地执行任何计算任务。

TrueBit等系统有广泛的应用，从机器学习到任何工作量证明的验证。后者的一个例子是Doge-Ethereum桥，它利用TrueBit来验证Dogecoin的工作量证明，Scrypt，一种难以在以太坊块gas限制内计算的内存密集和计算密集型函数。通过在TrueBit上执行此验证，可以在以太坊的Rinkeby测试网络上的智能合约中安全地验证Dogecoin交易。

#### 去中心化的 oracles <a href="#user-content-decentralized_orackes_sec" id="user-content-decentralized_orackes_sec"></a>

上面概况的机制都描述了依赖于可信任权威的集中式oracle系统。虽然它们应该足以满足许多应用，但它们确实代表了以太坊网络中的中心故障点。已经提出了许多围绕去中心化oracle作为确保数据可用性手段的方案，以及利用链上数据聚合系统创建独立数据提供者网络。

ChainLink \[10]提出了一个去中心化oracle网络，包括三个关键的智能合约：信誉合约，订单匹配合约，汇总合约和数据提供商的脱链注册。信誉合约用于跟踪数据提供商的绩效。声誉合约中的分数用于填充离线注册表。订单匹配合约使用信誉合约从oracles中选择出价。然后，它最终确定服务级别协议（SLA），其中包括查询参数和所需的oracles数量。这意味着购买者无需直接与个别的oracles交易。聚合合约从多个oracles收集使用提交/显示方案提交的响应，计算查询的最终集合结果，

这种去中心化方法的主要挑战之一是汇总函数的制定。ChainLink建议计算加权响应，允许为每个oracle响应报告有效性分数。在这里检测“无效”分数是非常重要的，因为它依赖于前提：由对等体提供的响应偏差测量的外围数据点是不正确的。基于响应分布中的oracle响应的位置来计算有效性分数可能会使正确答案超过普通答案。因此，ChainLink提供了一组标准的聚合合约，但也允许指定自定义的聚合合约。

一个相关的想法是SchellingCoin协议\[11]。在这里，多个参与者报告价值，并将中位数作为“正确”答案。报告者必须提供重新分配的存款，以支持更接近中位数的价值，从而激励报告与其他价值相似的价值。一个共同的价值，也称为Schelling Point，受访者可能认为这是一个自然而明显的协调目标，预计将接近实际价值。

Teutsch最近提出了一种新的去中心化脱链数据可用性设计oracle \[12]。该设计利用专用的工作证明区块链，该区块链能够正确地报告在给定时期内的注册数据是否可用。矿工尝试下载，存储和传播所有当前注册的数据，因此保证数据在本地可用。虽然这样的系统在每个挖掘节点存储和传播所有注册数据的意义上是昂贵的，但是系统允许通过在注册周期结束之后释放数据来重用存储。

#### Solidity中的Oracle客户端接口 <a href="#user-content-oracle_client_interfaces_in_solidity_sec" id="user-content-oracle_client_interfaces_in_solidity_sec"></a>

下面是一个Solidity示例，演示如何使用API从Oraclize连续轮询ETH/USD价格并以可用的方式存储结果。：

```
/*
   ETH/USD price ticker leveraging CryptoCompare API

   This contract keeps in storage an updated ETH/USD price,
   which is updated every 10 minutes.
 */

pragma solidity ^0.4.1;
import "github.com/oraclize/ethereum-api/oraclizeAPI.sol";

/*
   "oraclize_" prepended methods indicate inheritance from "usingOraclize"
 */
contract EthUsdPriceTicker is usingOraclize {

    uint public ethUsd;

    event newOraclizeQuery(string description);
    event newCallbackResult(string result);

    function EthUsdPriceTicker() payable {
        // signals TLSN proof generation and storage on IPFS
        oraclize_setProof(proofType_TLSNotary | proofStorage_IPFS);

        // requests query
        queryTicker();
    }

    function __callback(bytes32 _queryId, string _result, bytes _proof) public {
        if (msg.sender != oraclize_cbAddress()) throw;
        newCallbackResult(_result);

        /*
         * parse the result string into an unsigned integer for on-chain use
         * uses inherited "parseInt" helper from "usingOraclize", allowing for
         * a string result such as "123.45" to be converted to uint 12345
         */
        ethUsd = parseInt(_result, 2);

        // called from callback since we're polling the price
        queryTicker();
    }

    function queryTicker() public payable {
        if (oraclize_getPrice("URL") > this.balance) {
            newOraclizeQuery("Oraclize query was NOT sent, please add some ETH to cover for the query fee");
        } else {
            newOraclizeQuery("Oraclize query was sent, standing by for the answer..");

            // query params are (delay in seconds, datasource type, datasource argument)
            // specifies JSONPath, to fetch specific portion of JSON API result
            oraclize_query(60 * 10, "URL", "json(https://min-api.cryptocompare.com/data/price?fsym=ETH&tsyms=USD,EUR,GBP).USD");
        }
    }
}
```

要与Oraclize集成，合约EthUsdPriceTicker必须是usingOraclize的子项；usingOraclize合约在oraclizeAPI文件中定义。数据请求是使用oraclize\_query()函数生成的，该函数继承自usingOraclize合约。这是一个重载函数，至少需要两个参数：

* 支持的数据源，例如URL，WolframAlpha，IPFS或计算
* 给定数据源的参数，可能包括使用JSON或XML解析助手

价格查询在queryTicke()函数中执行。为了执行查询，Oraclize要求在以太网中支付少量费用，包括将结果传输和处理到_callback()函数的gas成本以及随附的服务附加费。此数量取决于数据源，如果指定，则取决于所需的真实性证明类型。一旦检索到数据，_callback()函数由Oraclize控制的帐户调用，该帐户被允许进行回调; 它传递响应值和唯一的queryId参数，作为示例，它可用于处理和跟踪来自Oraclize的多个挂起的回调。

金融数据提供商Thomson Reuters还为以太坊提供了一项名为BlockOne IQ的oracle服务，允许在私有或许可网络上运行的智能合约请求市场和参考数据\[13]。下面是oracle的接口，以及将发出请求的客户端合约：

```
pragma solidity ^0.4.11;

contract Oracle {
    uint256 public divisor;
    function initRequest(uint256 queryType, function(uint256) external onSuccess, function(uint256) external onFailure) public returns (uint256 id);
    function addArgumentToRequestUint(uint256 id, bytes32 name, uint256 arg) public;
    function addArgumentToRequestString(uint256 id, bytes32 name, bytes32 arg) public;
    function executeRequest(uint256 id) public;
    function getResponseUint(uint256 id, bytes32 name) public constant returns(uint256);
    function getResponseString(uint256 id, bytes32 name) public constant returns(bytes32);
    function getResponseError(uint256 id) public constant returns(bytes32);
    function deleteResponse(uint256 id) public constant;
}

contract OracleB1IQClient {

    Oracle private oracle;
    event LogError(bytes32 description);

    function OracleB1IQClient(address addr) public payable {
        oracle = Oracle(addr);
        getIntraday("IBM", now);
    }

    function getIntraday(bytes32 ric, uint256 timestamp) public {
        uint256 id = oracle.initRequest(0, this.handleSuccess, this.handleFailure);
        oracle.addArgumentToRequestString(id, "symbol", ric);
        oracle.addArgumentToRequestUint(id, "timestamp", timestamp);
        oracle.executeRequest(id);
    }

    function handleSuccess(uint256 id) public {
        assert(msg.sender == address(oracle));
        bytes32 ric = oracle.getResponseString(id, "symbol");
        uint256 open = oracle.getResponseUint(id, "open");
        uint256 high = oracle.getResponseUint(id, "high");
        uint256 low = oracle.getResponseUint(id, "low");
        uint256 close = oracle.getResponseUint(id, "close");
        uint256 bid = oracle.getResponseUint(id, "bid");
        uint256 ask = oracle.getResponseUint(id, "ask");
        uint256 timestamp = oracle.getResponseUint(id, "timestamp");
        oracle.deleteResponse(id);
        // Do something with the price data..
    }

    function handleFailure(uint256 id) public {
        assert(msg.sender == address(oracle));
        bytes32 error = oracle.getResponseError(id);
        oracle.deleteResponse(id);
        emit LogError(error);
    }

}
```

使用initRequest()函数启动数据请求，该函数除了两个回调函数之外，还允许指定查询类型（在此示例中，是对日内价格的请求）。 这将返回一个uint256标识符，然后可以使用该标识符提供其他参数。addArgumentToRequestString()函数用于指定RIC（Reuters Instrument Code），此处用于IBM股票，addArgumentToRequestUint()允许指定时间戳。现在，传入block.timestamp的别名将检索IBM的当前价格。然后由executeRequest()函数执行该请求。处理完请求后，oracle合约将使用查询标识符调用onSuccess回调函数，允许检索结果数据，否则在检索失败时使用错误代码进行onFailure回调。成功检索的可用字段包括开盘价，最高价，最低价，收盘价（OHLC）和买/卖价。

Reality Keys \[14]允许使用POST请求对事实进行离线请求。响应以加密方式签名，允许在链上进行验证。在这里，请求使用blockr.io API在特定时间检查比特币区块链上的账户余额：

```
wget -qO- https://www.realitykeys.com/api/v1/blockchain/new --post-data="chain=XBT&address=1F1tAaz5x1HUXrCNLbtMDqcw6o5GNn4xqX&which_total=total_received&comparison=ge&value=1000&settlement_date=2015-09-23&objection_period_secs=604800&accept_terms_of_service=current&use_existing=1"
```

对于此示例，参数允许指定区块链，要查询的金额（总收到金额或最终余额）以及要与提供的值进行比较的结果，从而允许真或假的响应。除了“signature\_v2”字段之外，生成的JSON对象还包括返回值，该字段允许使用ecrecover()函数在智能合约中验证结果：

```
"machine_resolution_value" : "29665.80352",
"signature_v2" : {
	"fact_hash" : "aadb3fa8e896e56bb13958947280047c0b4c3aa4ab8c07d41a744a79abf2926b",
	"ethereum_address" : "6fde387af081c37d9ffa762b49d340e6ae213395",
	"base_unit" : 1,
	"signed_value" : "0000000000000000000000000000000000000000000000000000000000000001",
  	"sig_r" : "a2cd9dc040e393299b86b1c21cbb55141ef5ee868072427fc12e7cfaf8fd02d1",
  	"sig_s" : "8f3199b9c5696df34c5193afd0d690241291d251a5d7b5c660fa8fb310e76f80",
  	"sig_v" : 27
}
```

为了验证签名，ecrecover()可以确定数据确实由ethereum\_address签名，如下所示。fact\_hash和signed\_value经过哈希处理，并将三个签名参数传递给ecrecover（）：

```
bytes32 result_hash = sha3(fact_hash, signed_value);
address signer_address = ecrecover(result_hash, sig_v, sig_r, sig_s);
assert(signer_address == ethereum_address);
uint256 result = uint256(signed_value) / base_unit;
// Do something with the result..
```

#### 参考 <a href="#user-content-references_sec" id="user-content-references_sec"></a>

#### 其他链接 <a href="#user-content-other_links_sec" id="user-content-other_links_sec"></a>

