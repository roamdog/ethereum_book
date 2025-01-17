# 第八章

我们在 [\[intro\]](broken-reference) 中发现，以太坊有两种不同类型的账户：外部所有账户（EOAs）和合约账户。EOAs由以太坊以外的软件（如钱包应用程序）控制。合约帐户由在以太坊虚拟机（EVM）内运行的软件控制。两种类型的帐户都通过以太坊地址标识。在本节中，我们将讨论第二种类型，合约账户和控制它们的软件：智能合约。

#### 以太坊高级语言简介 <a href="#user-content-high_level_languages" id="user-content-high_level_languages"></a>

EVM是一台虚拟计算机，运行一种特殊形式的 _机器代码_ ，称为\_EVM 字节码\_，就像你的计算机CPU运行机器代码x86\_64一样。我们将在 [\[evm\]](broken-reference) 中更详细地检查EVM的操作和语言。在本节中，我们将介绍如何编写智能合约以在EVM上运行。

虽然可以直接在字节码中编写智能合约。EVM字节码非常笨重，程序员难以阅读和理解。相反，大多数以太坊开发人员使用高级符号语言编写程序和编译器，将它们转换为字节码。

虽然任何高级语言都可以用来编写智能合约，但这是一项非常繁琐的工作。智能合约在高度约束和简约的执行环境（EVM）中运行，几乎所有通常的用户界面，操作系统界面和硬件界面都是缺失的。从头开始构建一个简约的智能合约语言要比限制通用语言并使其适用于编写智能合约更容易。因此，为编程智能合约出现了一些专用语言。以太坊有几种这样的语言，以及产生EVM可执行字节码所需的编译器。

一般来说，编程语言可以分为两种广泛的编程范式：分别是声明式和命令式，也分别称为“函数式”和“过程式”。在声明式编程中，我们编写的函数表示程序的 _逻辑_ _logic_，而不是 _流程_ _flow_。声明式编程用于创建没有 _副作用_ _side effects_ 的程序，这意味着在函数之外没有状态变化。声明式编程语言包括Haskell，SQL和HTML等。相反，命令式编程就是程序员编写一套程序的逻辑和流程结合在一起的程序。命令式编程语言包括例如BASIC，C，C++和Java。有些语言是“混合”的，这意味着他们鼓励声明式编程，但也可以用来表达一个必要的编程范式。这样的混合体包括Lisp，Erlang，Prolog，JavaScript和Python。一般来说，任何命令式语言都可以用来在声明式的范式中编写，但它通常会导致不雅的代码。相比之下，纯粹的声明式语言不能用来写入一个命令式的范例。在纯粹的声明式语言中，_没有“变量”_。

虽然命令式编程更易于编写和读取，并且程序员更常用，但编写按预期方式 _准确_ 执行的程序可能非常困难。程序的任何部分改变状态的能力使得很难推断程序的执行，并引入许多意想不到的副作用和错误。相比之下，声明式编程更难以编写，但避免了副作用，使得更容易理解程序的行为。

智能合约给程序员带来了很大的负担：错误会花费金钱。因此，编写不会产生意想不到的影响的智能合约至关重要。要做到这一点，你必须能够清楚地推断程序的预期行为。因此，声明式语言在智能合约中比在通用软件中扮演更重要的角色。不过，正如你将在下面看到的那样，最丰富的智能合约语言是命令式的（Solidity）。

智能合约的高级编程语言包括（按大概的年龄排序）：

LLL

一种函数式（声明式）编程语言，具有类似Lisp的语法。这是以太坊智能合约的第一个高级语言，但今天很少使用。

Serpent

一种过程式（命令式）编程语言，其语法类似于Python。也可以用来编写函数式（声明式）代码，尽管它并不完全没有副作用。很少被使用。最早由Vitalik Buterin创建。

Solidity

具有类似于JavaScript，C ++或Java语法的过程式（命令式）编程语言。以太坊智能合约中最流行和最常用的语言。最初由Gavin Wood（本书的合着者）创作。

Vyper

最近开发的语言，类似于Serpent，并且具有类似Python的语法。旨在成为比Serpent更接近纯粹函数式的类Python语言，但不能取代Serpent。最早由Vitalik Buterin创建。

Bamboo

一种新开发的语言，受Erlang影响，具有明确的状态转换并且没有迭代流（循环）。旨在减少副作用并提高可审计性。非常新，很少使用。

如你所见，有很多语言可供选择。然而，在所有这些中，Solidity是迄今为止最受欢迎的，以至于成为了以太坊甚至是其他类似EVM的区块链的事实上的高级语言。我们将花大部分时间使用Solidity，但也会探索其他高级语言的一些例子，以了解其不同的哲学。

#### 用Solidity构建智能合约 <a href="#user-content-building_a_smart_contract_sec" id="user-content-building_a_smart_contract_sec"></a>

来自维基百科：

> Solidity是编写智能合约的“面向合约的”编程语言。它用于在各种区块链平台上实施智能合约。它由Gavin Wood，Christian Reitwiessner，Alex Beregszaszi，Liana Husikyan，Yoichi Hirai和几位以前的以太坊核心贡献者开发，以便在区块链平台（如以太坊）上编写智能合约。

— Wikipedia entry for Solidity

Solidity由GitHub上的Solidity项目开发团队开发并维护：

Solidity项目的主要“产品”是\_Solidity Compiler（solc）\_，它将用Solidity语言编写的程序转换为EVM字节码，并生成其他制品，如应用程序二进制接口（ABI）。Solidity编译器的每个版本都对应于并编译Solidity语言的特定版本。

要开始，我们将下载Solidity编译器的二进制可执行文件。然后我们会编写一个简单的合约。

**选择一个Solidity版本**

目前，Solidity的版本是+0.4.21+，其中+0.4+是主要版本，21是次要版本，之后指定的任何内容都是补丁版本。Solidity的0.5版本主要版本即将推出。

正如我们在[\[intro\]](broken-reference)中看到的那样，你的Solidity程序可以包含一个+pragma+指令，用于指定与之兼容的Solidity的最小和最大版本，并且可用于编译你的合约。

由于Solidity正在快速发展，最好始终使用最新版本。

**下载/安装**

有许多方法可以用来下载和安装Solidity，无论是作为二进制发行版还是从源代码编译。你可以在Solidity文档中找到详细的说明：

在[Installing solc on Ubuntu/Debian with apt package manager](broken-reference)中，我们将使用 apt package manager 在Ubuntu/Debian操作系统上安装Solidity的最新二进制版本：

Installing solc on Ubuntu/Debian with apt package manager

```
$ sudo add-apt-repository ppa:ethereum/ethereum
$ sudo apt update
$ sudo apt install solc
```

一旦你安装了 solc，运行以下命令来检查版本：

```
$ solc --version
solc, the solidity compiler commandline interface
Version: 0.4.21+commit.dfe3193c.Linux.g++
```

根据你的操作系统和要求，还有许多其他方式可以安装Solidity，包括直接从源代码编译。有关更多信息，请参阅

**开发环境**

要在Solidity中开发，你可以在命令行上使用任何文本编辑器和+solc+。但是，你可能会发现为开发而设计的一些文本编辑器（例如Atom）提供了附加功能，如语法突出显示和宏，这些功能使Solidity开发变得更加简单。

使用可以提高生产力的工具。最后，Solidity程序只是纯文本文件。虽然花哨的编辑器和开发环境可以让事情变得更容易，但除了简单的文本编辑器（如vim（Linux / Unix），TextEdit（MacOS）甚至NotePad（Windows）），你无需任何其他东西。只需将程序源代码保存为+.sol+扩展名即可，Solidity编译器将其识别为Solidity程序。

**Writing a simple Solidity program**

在[\[intro\]](broken-reference)中，我们编写了我们的第一个Solidity程序，名为+Faucet+。当我们第一次构建+Faucet+时，我们使用Remix IDE来编译和部署合约。在本节中，我们将重新查看，改进和修饰+Faucet+。

我们的第一次尝试是这样的：

Faucet.sol : A Solidity contract implementing a faucet

```
// Our first contract is a faucet!
contract Faucet {

    // Give out ether to anyone who asks
    function withdraw(uint withdraw_amount) public {

        // Limit withdrawal amount
        require(withdraw_amount <= 100000000000000000);

        // Send the amount to the address that requested it
        msg.sender.transfer(withdraw_amount);
    }

    // Accept any incoming amount
    function () public payable {}

}
```

从 [\[make\_it\_better\]](broken-reference) 开始，我们将在第一个示例的基础上构建。

**用Solidity编译器（solc）编译**

现在，我们将使用命令行上的Solidity编译器直接编译我们的合约。Solidity编译器+solc+提供了多种选项，你可以通过+--help+参数来查看。

我们使用+solc+的 --bin 和 --optimize 参数来生成我们示例合约的优化二进制文件：

Compiling Faucet.sol with solc

```
$ solc --optimize --bin Faucet.sol
======= Faucet.sol:Faucet =======
Binary:
6060604052341561000f57600080fd5b60cf8061001d6000396000f300606060405260043610603e5763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416632e1a7d4d81146040575b005b3415604a57600080fd5b603e60043567016345785d8a0000811115606357600080fd5b73ffffffffffffffffffffffffffffffffffffffff331681156108fc0282604051600060405180830381858888f19350505050151560a057600080fd5b505600a165627a7a723058203556d79355f2da19e773a9551e95f1ca7457f2b5fbbf4eacf7748ab59d2532130029
```

\+solc+产生的结果是一个可以提交给以太坊区块链的十六进制序列化二进制文件。

#### 以太坊合约应用程序二进制接口（ABI） <a href="#user-content-eth_contract_abi_sec" id="user-content-eth_contract_abi_sec"></a>

在计算机软件中，应用程序二进制接口（ABI）是两个程序模块之间的接口；通常，一个在机器代码级别，另一个在用户运行的程序级别。ABI定义了如何在\*机器码\*中访问数据结构和功能；不要与API混淆，API以高级的，通常是人类可读的格式将访问定义为\*源代码\*。因此，ABI是将数据编码到机器码，和从机器码解码数据的主要方式。

在以太坊中，ABI用于编码EVM的合约调用，并从交易中读取数据。ABI的目的是定义合约中的哪些函数可以被调用，并描述函数如何接受参数并返回数据。

合约ABI的JSON格式由一系列函数描述（参见[\[solidity\_functions\]](broken-reference)）和事件（参见[\[solidity\_events\]](broken-reference)）的数组给出。函数描述是一个JSON对象，它包含\`type\`，`name`，`inputs`，`outputs`，``constant`和`payable`字段。事件描述对象具有`type``，`name`，\`inputs\`和\`anonymous\`的字段。

我们使用+solc+命令行Solidity编译器为我们的+Faucet.sol+示例合约生成ABI：

```
solc --abi Faucet.sol
======= Faucet.sol:Faucet =======
Contract JSON ABI
[{"constant":false,"inputs":[{"name":"withdraw_amount","type":"uint256"}],"name":"withdraw","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"payable":true,"stateMutability":"payable","type":"fallback"}]
```

如你所见，编译器会生成一个描述由 Faucet.sol 定义的两个函数的JSON对象。这个JSON对象可以被任何希望在部署时访问 Faucet 合约的应用程序使用。使用ABI，应用程序（如钱包或DApp浏览器）可以使用正确的参数和参数类型构造调用 Faucet 中的函数的交易。例如，钱包会知道要调用函数+withdraw+，它必须提供名为 withdraw\_amount 的 uint256 参数。钱包可以提示用户提供该值，然后创建一个编码它并执行+withdraw+功能的交易。

应用程序与合约进行交互所需的全部内容是ABI以及合约的部署地址。

**选择Solidity编译器和语言版本**

正如我们在 [Compiling Faucet.sol with solc](broken-reference) 中看到的，我们的 Faucet 合约在Solidity 0.4.21版本中成功编译。但是如果我们使用了不同版本的Solidity编译器呢？语言仍然不断变化，事情可能会以意想不到的方式发生变化。我们的合约非常简单，但如果我们的程序使用了仅添加到Solidity版本+0.4.19+中的功能，并且我们尝试使用+0.4.18+进行编译，该怎么办？

为了解决这些问题，Solidity提供了一个\_compiler指令\_，称为\_version pragma\_，指示编译器程序需要特定的编译器（和语言）版本。我们来看一个例子：

Solidity编译器读取版本编译指示，如果编译器版本与版本编译指示不兼容，将会产生错误。在这种情况下，我们的版本编译指出，这个程序可以由Solidity编译器编译，最低版本为+0.4.19+。但是，符号^表示我们允许编译任何\_minor修订版\_在+0.4.19+之上的，例如+0.4.20+，但不是+0.5.0+（这是一个主要版本，不是小修订版） 。Pragma指令不会编译为EVM字节码。它们仅由编译器用来检查兼容性。

让我们在我们的 Faucet 合约中添加一条编译指示。我们将命名新文件 Faucet2.sol，以便在我们继续处理这些示例时跟踪我们的更改：

Faucet2.sol : Adding the version pragma to Faucet

```
// Version of Solidity compiler this program was written for
pragma solidity ^0.4.19;

// Our first contract is a faucet!
contract Faucet {

    // Give out ether to anyone who asks
    function withdraw(uint withdraw_amount) public {

        // Limit withdrawal amount
        require(withdraw_amount <= 100000000000000000);

        // Send the amount to the address that requested it
        msg.sender.transfer(withdraw_amount);
    }

    // Accept any incoming amount
    function () public payable {}

}
```

添加版本 pragma 是最佳实践，因为它避免了编译器和语言版本不匹配的问题。我们将探索其他最佳实践，并在本章中继续改进+Faucet+合约。

#### 使用Solidity编程 <a href="#usercontent-shi-yong-solidity-bian-cheng" id="usercontent-shi-yong-solidity-bian-cheng"></a>

在本节中，我们将看看Solidity语言的一些功能。正如我们在 [\[intro\]](broken-reference) 中提到的，我们的第一份合约示例非常简单，并且在许多方面也存在缺陷。我们将逐渐改进这个例子，同时学习如何使用Solidity。然而，这不会是一个全面的Solidity教程，因为Solidity相当复杂且快速发展。我们将介绍基础知识，并为你提供足够的基础，以便能够自行探索其余部分。Solidity的完整文档可以在以下网址找到：

**数据类型**

首先，我们来看看Solidity中提供的一些基本数据类型：

boolean (bool)

布尔值, true 或 false, 以及逻辑操作符 ! (not), && (and), || (or), == (equal), != (not equal).

整数 (int/uint)

有符号 (int) 和 无符号 (uint) 整数，从 u/int8 到 u/int256以 8 bits 递增，没有大小后缀的话，表示256 bits。

定点数 (fixed/ufixed)

定点数, 定义为 u/fixedMxN，其中 M 是位大小（以8递增），N 是小数点后的十进制数的个数。

地址

20字节的以太坊地址。address 对象有 balance (返回账户的余额) 和 transfer (转移ether到该账户) 成员方法。

字节数组（定长）

固定大小的字节数组，定义为+bytes1+到+bytes32+。

字节数组 (动态)

动态大小的字节数组，定义为+bytes+或+string+。

enum

枚举离散值的用户定义类型。

struct

包含一组变量的用户定义的数据容器。

mapping

\+key ⇒ value+对的哈希查找表。

除上述数据类型外，Solidity还提供了多种可用于计算不同单位的字面值：

时间单位

seconds, minutes, hours, 和 days 可用作后缀，转换为基本单位 seconds 的倍数。

以太的单位

wei, finney, szabo, 和 ether 可用作后缀, 转换为基本单位 wei 的倍数。

到目前为止，在我们的+Faucet+合约示例中，我们使用+uint+（这是+uint256+的别名），用于+withdraw\_amount+变量。我们还间接使用了+address+变量，它是+ msg.sender+。在本章中，我们将在示例中使用更多数据类型。

让我们使用单位的倍数之一来提高示例合约+Faucet+的可读性。在+withdraw+函数中，我们限制最大提现额，将数量限制表示为+wei+，以太的基本单位：

```
require(withdraw_amount <= 100000000000000000);
```

这不是很容易阅读，所以我们可以通过使用单位倍数 ether 来改进我们的代码，以ether而不是wei表示值：

```
require(withdraw_amount <= 0.1 ether);
```

**预定义的全局变量和函数**

在EVM中执行合约时，它可以访问一组较小范围内的全局对象。这些包括 block，msg 和 tx 对象。另外，Solidity公开了许多EVM操作码作为预定义的Solidity功能。在本节中，我们将检查你可以从Solidity的智能合约中访问的变量和函数。

**调用交易/消息上下文**

msg

\+msg+对象是启动合约执行的交易（源自EOA）或消息（源自合约）。它包含许多有用的属性：

msg.sender

我们已经使用过这个。它代表发起消息的地址。如果我们的合约是由EOA交易调用的，那么这是签署交易的地址。

msg.value

与消息一起发送的以太网值。

msg.gas

调用我们的合约的消息中留下的gas量。它已经被弃用，并将被替换为Solidity v0.4.21中的gasleft()函数。

msg.data

调用合约的消息中的数据。

msg.sig

数据的前四个字节，它是函数选择器。

| Note | 每当合约调用另一个合约时，msg+的所有属性的值都会发生变化，以反映新的调用者的信息。唯一的例外是在原始+msg+上下文中运行另一个合约/库的代码的 +delegatecall 函数。 |
| ---- | -------------------------------------------------------------------------------------------- |

**交易上下文**

tx.gasprice

发起调用的交易中的gas价格。

tx.origin

源自（EOA）的交易的完整调用堆栈。

**区块上下文**

block

包含有关当前块的信息的块对象。

block.blockhash(blockNumber)

指定块编号的块的哈希，直到之前的256个块。已弃用，并使用Solidity v.0.4.22中的+blockhash()+函数替换。

block.coinbase

当前块的矿工地址。

block.difficulty

当前块的难度（Proof-of-Work）。

block.gaslimit

当前块的区块gas限制。

block.number

当前块号（高度）。

block.timestamp

矿工在当前块中放置的时间戳，自Unix纪元（秒）开始。

**地址对象**

任何地址（作为输入传递或从合约对象转换而来）都有一些属性和方法：

address.balance

地址的余额，以wei为单位。例如，当前合约余额是 address(this).balance。

address.transfer(amount)

将金额（wei）转移到该地址，并在发生任何错误时抛出异常。我们在+Faucet+示例中的+msg.sender+地址上使用了此函数，msg.sender.transfer()。

address.send(amount)

类似于前面的+transfer+, 但是失败时不抛出异常，而是返回+false+。

address.call()

低级调用函数，可以用+value+，data+构造任意消息。错误时返回+false。

address.delegatecall()

低级调用函数，保持发起调用的合约的+msg+上下文，错误时返回+false+。

**内置函数**

addmod, mulmod

模加法和乘法。例如，addmod(x,y,k) 计算 (x + y) % k。

keccak256, sha256, sha3, ripemd160

用各种标准哈希算法计算哈希值的函数。

ecrecover

从签名中恢复用于签署消息的地址。

**合约的定义**

Solidity的主要数据类型是\_contract\_对象，它在我们的+Faucet+示例的顶部定义。与面向对象语言中的任何对象类似，合约是一个包含数据和方法的容器。

Solidity提供了另外两个与合约类似的对象：

interface

接口定义的结构与合约完全一样，只不过没有定义函数，它们只是声明。这种类型的函数声明通常被称为 _桩_ _stub_，因为它告诉你有关函数的参数和返回值，没有任何实现。它用来指定合约接口，如果继承，每个函数都必须在子类中指定。

library

一个库合约是一个只能部署一次并被其他合约使用的合约，使用+delegatecall+方法（见[地址对象](broken-reference)）。

**函数**

在合约中，我们定义了可以由EOA交易或其他合约调用的函数。在我们的+Faucet+示例中，我们有两个函数：+withdraw+和（未命名的）\_fallback\_函数。

函数使用以下语法定义：

**function** FunctionName(\[_parameters_]) {**public**|**private**|**internal**|**external**} \[**pure**|**constant**|**view**|**payable**] \[_modifiers_] \[**returns** (<_return types_>)]

我们来看看每个组件：

FunctionName

定义函数的名称，用于通过交易（EOA），其他合约或同一合约调用函数。每个合约中的一个功能可以定义为不带名称的，在这种情况下，它是\_fallback\_函数，在没有指定其他函数时调用该函数。fallback函数不能有任何参数或返回任何内容。

parameters

在名称后面，我们指定必须传递给函数的参数，包括名称和类型。在我们的+Faucet+示例中，我们将+uint withdraw\_amount+定义为+withdraw+函数的唯一参数。

下一组关键字 (public, private, internal, external) 指定了函数的\_可见性\_：

public

Public是默认的，这些函数可以被其他合约，EOA交易或合约内部调用。在我们的+Faucet+示例中，这两个函数都被定义为public。

external

外部函数就像public一样，但除非使用关键字this作为前缀，否则它们不能从合约中调用。

internal

内部函数只能在合约内部"可见"，不能被其他合约或EOA交易调用。他们可以被派生合约调用（继承的）。

private

private函数与内部函数类似，但不能由派生的合约调用（继承的）。

请记住，术语 internal 和 private 有些误导性。公共区块链中的任何函数或数据总是\_可见的\_，意味着任何人都可以看到代码或数据。以上关键字仅影响函数的调用方式和时机。

下一组关键字（pure, constant, view, payable）会影响函数的行为：

constant/view

标记为\_view\_的函数，承诺不修改任何状态。术语\_constant\_是\_view\_的别名，将被弃用。目前，编译器不强制执行\_view\_修饰器，只产生一个警告，但这应该成为Solidity v0.5中的强制关键字。

pure

纯(pure)函数不读写任何变量。它只能对参数进行操作并返回数据，而不涉及任何存储的数据。纯函数旨在鼓励没有副作用或状态的声明式编程。

payable

payable函数是可以接受付款的功能。没有payable的函数将拒绝收款，除非它们来源于coinbase（挖矿收入）或 作为 SELFDESTRUCT（合约终止）的目的地。在这些情况下，由于EVM中的设计决策，合约无法阻止收款。

正如你在+Faucet+示例中看到的那样，我们有一个payable函数（fallback函数），它是唯一可以接收付款的函数。

**合约构造和自毁**

有一个特殊函数只能使用一次。创建合约时，它还运行 _构造函数_ _constructor function_（如果存在），以初始化合约状态。构造函数与创建合约时在同一个交易中运行。构造函数是可选的。事实上，我们的+Faucet+示例没有构造函数。

构造函数可以通过两种方式指定。到Solidity v.0.4.21，构造函数是一个名称与合约名称相匹配的函数：

Constructor function prior to Solidity v0.4.22

```
contract MEContract {
	function MEContract() {
		// This is the constructor
	}
}
```

这种格式的难点在于如果合约名称被改变并且构造函数名称没有改变，它就不再是构造函数了。这可能会导致一些非常令人讨厌的，意外的并且很难注意到的错误。想象一下，例如，如果构造函数正在为控制目的而设置合约的“所有者”。它不仅可以在创建合约时设置所有者，还可以像正常功能那样“可调用”，允许任何第三方在合约创建后劫持合约并成为“所有者”。

为了解决构造函数的潜在问题，它基于与合约名称相同的名称，Solidity v0.4.22引入了一个+constructor+关键字，它像构造函数一样运行，但没有名称。重命名合约并不会影响构造函数。此外，更容易确定哪个函数是构造函数。看起来像这样：

```
pragma ^0.4.22
contract MEContract {
	constructor () {
		// This is the constructor
	}
}
```

总而言之，合约的生命周期始于EOA或其他合约的创建交易。如果有一个构造函数，它将在相同的创建交易中调用，并可以在创建合约时初始化合约状态。

合约生命周期的另一端是 _合约销毁_ _contract destruction_。合约被称为+SELFDESTRUCT+的特殊EVM操作码销毁。它曾经是+SUICIDE+，但由于该词的负面性，该名称已被弃用。在Solidity中，此操作码作为高级内置函数+selfdestruct+公开，该函数采用一个参数：地址以接收合约帐户中剩余的余额。看起来像这样：

```
selfdestruct(address recipient);
```

**添加一个构造函数和selfdestruct到我们的+Faucet+示例**

我们在[\[intro\]](broken-reference)中引入的+Faucet+示例合约没有任何构造函数或自毁函数。这是永恒的合约，不能从区块链中删除。让我们通过添加一个构造函数和selfdestruct函数来改变它。我们可能希望自毁仅由最初创建合约的EOA来调用。按照惯例，这通常存储在称为+owner+的地址变量中。我们的构造函数设置所有者变量，并且selfdestruct函数将首先检查是否是所有者调用它。

首先是我们的构造函数：

```
// Version of Solidity compiler this program was written for
pragma solidity ^0.4.22;

// Our first contract is a faucet!
contract Faucet {

	address owner;

	// Initialize Faucet contract: set owner
	constructor() {
		owner = msg.sender;
	}

[...]
```

我们已经更改了pragma指令，将v0.4.22指定为此示例的最低版本，因为我们使用的是仅存在于Solidity v.0.4.22中的constructor关键字。我们的合约现在有一个名为+owner+的+address+类型变量。名称“owner”不是特殊的。我们可以将这个地址变量称为“potato”，仍然以相同的方式使用它。名称+owner+只是简单明了的目的和目的。

然后，作为合约创建交易的一部分运行的constructor函数将+msg.sender+的地址分配给+owner+变量。我们使用 withdraw 函数中的 msg.sender 来 标识提款请求的来源。然而，在构造函数中，+msg.sender+是签署合约创建交易的EOA或合约地址。这是事实，因为这是一个构造函数：它只运行一次，并且仅作为合约创建交易的结果。

好的，现在我们可以添加一个函数来销毁合约。我们需要确保只有所有者才能运行此函数，因此我们将使用+require+语句来控制访问。看起来像这样：

```
// Contract destructor
function destroy() public {
	require(msg.sender == owner);
	selfdestruct(owner);
}
```

如果其他人用 owner 以外的地址调用 destroy 函数，则将失败。但是，如果构造函数存储在 owner 中的地址调用它，合约将自毁，并将剩余余额发送到 owner 地址。

**函数修饰器**

Solidity提供了一种称为\_函数修饰器\_的特殊类型的函数。通过在函数声明中添加修饰器名称，可以将修饰器应用于函数。修饰器函数通常用于创建适用于合约中许多函数的条件。我们已经在我们的+destroy+函数中有一个访问控制语句。让我们创建一个表达该条件的函数修饰器：

onlyOwner function modifier

```
modifier onlyOwner {
    require(msg.sender == owner);
    _;
}
```

在 [onlyOwner function modifier](broken-reference) 中，我们看到函数修饰器的声明，名为+onlyOwner+。此函数修饰器为其修饰的任何函数设置条件，要求存储为合约的+owner+的地址与交易的+msg.sender+的地址相同。这是访问控制的基本设计模式，只允许合约的所有者执行具有+onlyOwner+修饰器的任何函数。

你可能已经注意到我们的函数修饰器在其中有一个特殊的语法“占位符”，下划线后跟分号（\_;）。此占位符由正在修饰的函数的代码替换。本质上，修饰器“修饰”修饰过的函数，将其代码置于由下划线字符标识的位置。

要应用修饰器，请将其名称添加到函数声明中。可以将多个修饰器应用于一个函数，作为逗号分隔的列表，以声明的顺序应用。

让我们重新编写+destroy+函数来使用+onlyOwner+修饰器：

```
function destroy() public onlyOwner {
    selfdestruct(owner);
}
```

函数修饰器的名称（onlyOwner）位于关键字+public+之后，并告诉我们+destroy+函数由+onlyOwner+修饰器修饰。基本上你可以把它写成：“只有所有者才能销毁这份合约”。实际上，生成的代码相当于由+onlyOwner+ “包装” 的+destroy+代码。

函数修饰器是一个非常有用的工具，因为它们允许我们为函数编写前提条件并一致地应用它们，使代码更易于阅读，因此更易于审计安全问题。它们最常用于访问控制，如示例中的“function\_modifier\_onlyowner”，但功能很多，可用于各种其他目的。

在修饰函数内部，可以访问被修饰的函数的的所有可见符号（变量和参数）。在这种情况下，我们可以访问在合约中声明的+owner+变量。但是，反过来并不正确：你无法访问修饰函数中的任何变量。

**合约继承**

Solidity的合约对象支持 _继承_，这是一种用附加功能扩展基础合约的机制。要使用继承，请使用关键字+is+指定父合约：

```
contract Child is Parent {
}
```

通过这个构造，+Child+合约继承了+Parent+的所有方法，功能和变量。Solidity还支持多重继承，可以在关键字+is+之后用逗号分隔的合约名称指定多重继承：

```
contract Child is Parent1, Parent2 {
}
```

合约继承使我们能够以实现模块化，可扩展性和重用的方式编写我们的合约。我们从简单的合约开始，实现最通用的功能，然后通过在更具体的合约中继承这些功能来扩展它们。

在我们的+Faucet+合约中，我们引入了构造函数和析构函数，以及为构建时指定的owner提供的访问控制。这些功能非常通用：许多合约都有它们。我们可以将它们定义为通用合约，然后使用继承将它们扩展到+Faucet+合约。

我们首先定义一个基础合约+owned+，它拥有一个+owner+变量，并在合约的构造函数中设置：

```
contract owned {
	address owner;

	// Contract constructor: set owner
	constructor() {
		owner = msg.sender;
	}

	// Access control modifier
	modifier onlyOwner {
	    require(msg.sender == owner);
	    _;
	}
}
```

接下来，我们定义一个基本合约 mortal，继承自 owned：

```
contract mortal is owned {
	// Contract destructor
	function destroy() public onlyOwner {
		selfdestruct(owner);
	}
}
```

如你所见，mortal 合约可以使用在+owned+中定义的+ownOwner+函数修饰器。它间接地也使用+owner+ address变量和+owned+中定义的构造函数。继承使每个合约变得更简单，并专注于其类的特定功能，使我们能够以模块化的方式管理细节。

现在我们可以进一步扩展+owned+合约，在+Faucet+中继承其功能：

```
contract Faucet is mortal {
    // Give out ether to anyone who asks
    function withdraw(uint withdraw_amount) public {
        // Limit withdrawal amount
        require(withdraw_amount <= 100000000000000000);
        // Send the amount to the address that requested it
        msg.sender.transfer(withdraw_amount);
    }
    // Accept any incoming amount
    function () public payable {}
}
```

通过继承+mortal+，继而继承+owned+，+Faucet+合约现在具有构造函数和销毁函数以及定义的owner。这些功能与+Faucet+中的功能相同，但现在我们可以在其他合约中重用这些功能而无需再次写入它们。代码重用和模块化使我们的代码更清晰，更易于阅读，并且更易于审计。

**错误处理（assert, require, revert）**

合约调用可以终止并返回错误。Solidity中的错误由四个函数处理：assert, require, revert, 和 throw（现在已弃用）。

当合约终止并出现错误时，如果有多个合约被调用，则所有状态变化（变量，余额等的变化）都会恢复，直至合约调用链的源头。这确保交易是原子的，这意味着它们要么成功完成，要么对状态没有影响，并完全恢复。

assert+和+require+函数以相同的方式运行，如果条件为假，则评估条件并停止执行并返回错误。按照惯例，当结果预期为真时使用+assert，这意味着我们使用+assert+来测试内部条件。相比之下，在测试输入（例如函数参数或交易字段）时使用+require+，设置我们对这些条件的期望。

我们在函数修饰器+onlyOwner+中使用了+require+来测试消息发送者是合约的所有者：

```
require(msg.sender == owner);
```

require 函数充当\_守护条件\_，阻止执行函数的其余部分，并在不满足时产生错误。

从Solidity v.0.4.22开始，+require+还可以包含有用的文本消息，可用于显示错误的原因。错误消息记录在交易日志中。所以我们可以通过在我们的+require+函数中添加一条错误消息来改进我们的代码：

```
require(msg.sender == owner, "Only the contract owner can call this function");
```

revert 和 throw 函数，停止执行合约并还原任何状态更改。+throw+函数已过时，将在未来版本的Solidity中删除 - 你应该使用+revert+代替。+revert+函数还可以将作为唯一参数的错误消息记录在交易日志中。

无论我们是否明确检查它们，合约中的某些条件都会产生错误。例如，在我们的+Faucet+合约中，我们不检查是否有足够的ether来满足提款请求。这是因为如果没有足够的余额进行转账，+transfer+函数将失败并恢复交易：

The transfer function will fail if there is an insufficient balance

```
msg.sender.transfer(withdraw_amount);
```

但是，最好明确检查，并在失败时提供明确的错误消息。我们可以通过在转移之前添加一个require语句来实现这一点：

```
require(this.balance >= withdraw_amount,
	"Insufficient balance in faucet for withdrawal request");
msg.sender.transfer(withdraw_amount);
```

像这样的其他错误检查代码会略微增加gas消耗，但它比不检查提供了更好的错误报告。在gas量和详细错误检查之间取得适当的平衡是你需要根据合约的预期用途来决定的。在为测试网络设计的+Faucet+的情况下，即使额外报告成本更高，我们也不冒险犯错。也许对于一个主网合约，我们会选择节约gas用量。

**事件（Events）**

事件是便于生产交易日志的Solidity构造。当一个交易完成（成功与否）时，它会产生一个 _交易收据_ _transaction receipt_，就像我们在 [\[evm\]](broken-reference) 中看到的那样。交易收据包含\_log\_条目，用于提供有关在执行交易期间发生的操作的信息。事件是用于构造这些日志的Solidity高级对象。

事件在轻量级客户端和DApps中特别有用，它可以“监视”特定事件并将其报告给用户界面，或对应用程序的状态进行更改以反映底层合约中的事件。

事件对象接收序列化的参数并记录在区块链的交易日志中。你可以在参数之前应用关键字+indexed+，以使其值作为索引表（哈希表）的一部分，可以由应用程序搜索或过滤。

到目前为止，我们还没有在我们的+Faucet+示例中添加任何事件，所以让我们来做。我们将添加两个事件，一个记录任何提款，一个记录任何存款。我们将分别称这些事件+Withdrawal+和+Deposit+。首先，我们在+Faucet+合约中定义事件：

```
contract Faucet is mortal {
	event Withdrawal(address indexed to, uint amount);
	event Deposit(address indexed from, uint amount);

	[...]
}
```

我们选择将地址标记为+indexed+，以允许任何访问我们的+Faucet+的用户界面中搜索和过滤。

接下来，我们使用 emit 关键字将事件数据合并到交易日志中：

```
// Give out ether to anyone who asks
function withdraw(uint withdraw_amount) public {
    [...]
    msg.sender.transfer(withdraw_amount);
    emit Withdrawal(msg.sender, withdraw_amount);
}
// Accept any incoming amount
function () public payable {
    emit Deposit(msg.sender, msg.value);
}
```

Faucet.sol 合约现在看起来像：

Faucet8.sol: Revised Faucet contract, with events

```
link:code/Solidity/Faucet8.sol[]
// Version of Solidity compiler this program was written for
pragma solidity ^0.4.22;

contract owned {
	address owner;
	// Contract constructor: set owner
	constructor() {
		owner = msg.sender;
	}
	// Access control modifier
	modifier onlyOwner {
		require(msg.sender == owner, "Only the contract owner can call this function");
		_;
	}
}

contract mortal is owned {
	// Contract destructor
	function destroy() public onlyOwner {
		selfdestruct(owner);
	}
}

contract Faucet is mortal {
	event Withdrawal(address indexed to, uint amount);
	event Deposit(address indexed from, uint amount);

	// Give out ether to anyone who asks
	function withdraw(uint withdraw_amount) public {
		// Limit withdrawal amount
		require(withdraw_amount <= 0.1 ether);
		require(this.balance >= withdraw_amount,
			"Insufficient balance in faucet for withdrawal request");
		// Send the amount to the address that requested it
		msg.sender.transfer(withdraw_amount);
		emit Withdrawal(msg.sender, withdraw_amount);
	}
	// Accept any incoming amount
	function () public payable {
		emit Deposit(msg.sender, msg.value);
	}
}
```

**捕捉事件**

好的，所以我们已经建立了我们的合约来发布事件。我们如何看到交易的结果并“捕捉”事件？+web3.js+库提供一个数据结构，作为包含交易日志的交易的结果。在那里，我们可以看到交易产生的事件。

让我们使用+truffle+在修订的+Faucet+合约上运行测试交易。按照 [\[truffle\]](broken-reference) 中的说明设置项目目录并编译+Faucet+代码。源代码可以在本书的GitHub存储库中找到：

```
code/truffle/FaucetEvents
```

```
$ truffle develop
truffle(develop)> compile
truffle(develop)> migrate
Using network 'develop'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0xb77ceae7c3f5afb7fbe3a6c5974d352aa844f53f955ee7d707ef6f3f8e6b4e61
  Migrations: 0x8cdaf0cd259887258bc13a92c0a6da92698644c0
Saving successful migration to network...
  ... 0xd7bc86d31bee32fa3988f1c1eabce403a1b5d570340a3a9cdba53a472ee8c956
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying Faucet...
  ... 0xfa850d754314c3fb83f43ca1fa6ee20bc9652d891c00a2f63fd43ab5bfb0d781
  Faucet: 0x345ca3e014aaf5dca488057592ee47305d9b3e10
Saving successful migration to network...
  ... 0xf36163615f41ef7ed8f4a8f192149a0bf633fe1a2398ce001bf44c43dc7bdda0
Saving artifacts...

truffle(develop)> Faucet.deployed().then(i => {FaucetDeployed = i})
truffle(develop)> FaucetDeployed.send(web3.toWei(1, "ether")).then(res => { console.log(res.logs[0].event, res.logs[0].args) })
Deposit { from: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 18, c: [ 10000 ] } }
truffle(develop)> FaucetDeployed.withdraw(web3.toWei(0.1, "ether")).then(res => { console.log(res.logs[0].event, res.logs[0].args) })
Withdrawal { to: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 17, c: [ 1000 ] } }
```

用+deployed()函数获得部署的合约后，我们执行两个交易。第一笔交易是一笔存款（使用+send），在交易日志中发出+Deposit+事件：

```
Deposit { from: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 18, c: [ 10000 ] } }
```

接下来，我们使用+withdraw+函数进行提款。这会发出+Withdrawal+事件：

```
Withdrawal { to: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 17, c: [ 1000 ] } }
```

为了获得这些事件，我们查看了作为结果（res）返回的+logs+数组。第一个日志条目（logs\[0]）包含+logs\[0].event+的事件名称和+logs\[0].args+的事件参数。通过在控制台上显示这些信息，我们可以看到发出的事件名称和事件参数。

事件是一种非常有用的机制，不仅适用于合约内通信，还适用于开发过程中的调试。

**调用其他合约 (call, send, delegatecall, callcode)**

在合约中调用其他合约是非常有用但有潜在危险的操作。我们将研究你可以实现的各种方法并评估每种方法的风险。

**创建一个新的实例**

调用另一份合约最安全的方法是你自己创建其他合约。这样，你就可以确定它的接口和行为。要做到这一点，你可以简单地使用关键字+new+来实例化它，就像任何面向对象的语言一样。在Solidity中，关键字+new+将在区块链上创建合约并返回一个可用于引用它的对象。假设你想从另一个名为+Token+的合约中创建并调用+Faucet+合约：

```
contract Token is mortal {
	Faucet _faucet;

	constructor() {
		_faucet = new Faucet();
	}
}
```

这种合约建造机制确保你知道合约的确切类型及其接口。合约+Faucet+必须在+Token+范围内定义，如果定义位于另一个文件中，你可以使用+import+语句来执行此操作：

```
import "Faucet.sol"

contract Token is mortal {
	Faucet _faucet;

	constructor() {
		_faucet = new Faucet();
	}
}
```

\+new+关键字还可以接受可选参数来指定创建时传输的ether+值+以及传递给新合约构造函数的参数（如果有）：

```
import "Faucet.sol"

contract Token is mortal {
	Faucet _faucet;

	constructor() {
		_faucet = (new Faucet).value(0.5 ether)();
	}
}
```

如果我们赋予创建的+Faucet+一些ether，我们也可以调用+Faucet+函数，它们就像方法调用一样操作。在这个例子中，我们从+Token+的+destroy+函数中调用+Faucet+的+destroy+函数：

```
import "Faucet.sol"

contract Token is mortal {
	Faucet _faucet;

	constructor() {
		_faucet = (new Faucet).value(0.5 ether)();
	}

	function destroy() ownerOnly {
		_faucet.destroy();
	}
}
```

**访问现有的实例**

我们可以用来调用合约的另一种方法是将现有合约的地址转换为实例。使用这种方法，我们将已知接口应用于现有实例。因此，我们需要确切地知道，我们正在处理的事例实际上与我们所假设的类型相同，这一点非常重要。我们来看一个例子：

```
import "Faucet.sol"

contract Token is mortal {

	Faucet _faucet;

	constructor(address _f) {
		_faucet = Faucet(_f);
		_faucet.withdraw(0.1 ether)
	}
}
```

在这里，我们将地址作为参数提供给构造函数，并将其作为+Faucet+对象进行转换。这比以前的机制风险大得多，因为我们实际上并不知道该地址是否实际上是+Faucet+对象。当我们调用+withdraw+时，我们假设它接受相同的参数并执行与我们的+Faucet+声明相同的代码，但我们无法确定。就我们所知，在这个地址的+withdraw+函数可以执行与我们所期望的完全不同的事情，即使它的命名相同。因此，使用作为输入传递的地址并将它们转换成特定的对象中比自己创建合约要危险得多。

**原始调用, delegatecall**

Solidity为调用其他合约提供了一些更“低级”的功能。它们直接对应于具有相同名称的EVM操作码，并允许我们手动构建合约到合约的调用。因此，它们代表了调用其他合约最灵活和最危险的机制。

以下是使用 call 方法的相同示例：

```
contract Token is mortal {
	constructor(address _faucet) {
		_faucet.call("withdraw", 0.1 ether);
	}
}
```

正如你所看到的，这种类型的+call+，是一个函数的\_盲\_ _blind\_调用，就像构建一个原始交易一样，只是在合约的上下文中。它可能会使我们的合约面临一些安全风险，最重要的是 \_可重入性_ _reentrancy_，我们将在 [\[reentrancy\]](broken-reference) 中更详细地讨论。如果出现问题，+call+函数将返回false，所以我们可以评估返回值以进行错误处理：

```
contract Token is mortal {
	constructor(address _faucet) {
		if !(_faucet.call("withdraw", 0.1 ether)) {
			revert("Withdrawal from faucet failed");
		}
	}
}
```

call+的另一个变体是+delegatecall，它取代了更危险的+callcode+。+callcode+方法很快就会被弃用，所以不应该使用它。

正如[地址对象](broken-reference)中提到的，delegatecall+不同于+call，因为+msg+上下文不会改变。例如，call 将 msg.sender 的值更改为发起调用的合约，而+delegatecall+保持与发起调用的合约中的+msg.sender+相同。基本上，+delegatecall+在当前合约的上下文中运行另一个合约的代码。它最常用于从+library+调用代码。

应该谨慎使用+delegatecall+。它可能会有一些意想不到的效果，特别是如果你调用的合约不是作为库设计的。

让我们使用示例合约来演示+call+和+delegatecall+用于调用库和合约的各种调用语义。我们使用一个事件来记录每个调用的来源，并根据调用类型了解调用上下文如何变化：

CallExamples.sol: An example of different call semantics.

```
link:code/truffle/CallExamples/contracts/CallExamples.sol[]

pragma solidity ^0.4.22;

contract calledContract {
	event callEvent(address sender, address origin, address from);
	function calledFunction() public {
		emit callEvent(msg.sender, tx.origin, this);
	}
}

library calledLibrary {
	event callEvent(address sender, address origin,  address from);
	function calledFunction() public {
		emit callEvent(msg.sender, tx.origin, this);
	}
}

contract caller {

	function make_calls(calledContract _calledContract) public {

		// Calling the calledContract and calledLibrary directly
		_calledContract.calledFunction();
		calledLibrary.calledFunction();

		// Low level calls using the address object for calledContract
		require(address(_calledContract).call(bytes4(keccak256("calledFunction()"))));
		require(address(_calledContract).delegatecall(bytes4(keccak256("calledFunction()"))));
	}
}
```

我们的主要合约是+caller+，它调用库 calledLibrary 和合约 calledContract。被调用的库和合约有相同的函数 calledFunction，发送+calledEvent+事件。calledEvent+事件记录三个数据：+msg.sender, tx.origin, 和 this。每次调用+calledFunction+时，都会有不同的上下文（不同的 msg.sender）取决于它是直接调用还是通过 delegatecall 调用。

在+caller+中，我们首先直接调用合约和库的calledFunction()。然后，我们直接使用低级函数+call+和+delegatecall+调用+calledContract.calledFunction+。观察多种调用机制的行为。

让我们在truffle开发环境中运行并捕捉事件：

```
truffle(develop)> migrate
Using network 'develop'.
[...]
Saving artifacts...
truffle(develop)> web3.eth.accounts[0]
'0x627306090abab3a6e1400e9345bc60c78a8bef57'
truffle(develop)> caller.address
'0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f'
truffle(develop)> calledContract.address
'0x345ca3e014aaf5dca488057592ee47305d9b3e10'
truffle(develop)> calledLibrary.address
'0xf25186b5081ff5ce73482ad761db0eb0d25abfbf'
truffle(develop)> caller.deployed().then( i => { callerDeployed = i })

truffle(develop)> callerDeployed.make_calls(calledContract.address).then(res => { res.logs.forEach( log => { console.log(log.args) })})
{ sender: '0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f',
  origin: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  from: '0x345ca3e014aaf5dca488057592ee47305d9b3e10' }
{ sender: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  origin: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  from: '0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f' }
{ sender: '0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f',
  origin: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  from: '0x345ca3e014aaf5dca488057592ee47305d9b3e10' }
{ sender: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  origin: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  from: '0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f' }
```

让我们看看发生了什么。我们调用+make\_calls+函数并传递+calledContract+的地址，然后捕获不同调用发出的四个事件。查看+make\_calls+函数，让我们逐步了解每一步。

第一个调用：

```
_calledContract.calledFunction();
```

在这里，我们直接调用+calledContract.calledFunction+，使用称为callFunction的高级ABI。发出的事件是：

```
sender: '0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f',
origin: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
from: '0x345ca3e014aaf5dca488057592ee47305d9b3e10'
```

如你所见，msg.sender+是+caller+合约的地址。+tx.origin+是我们的钱包+web3.eth.accounts\[0]+的地址，钱包将交易发送给+caller。该事件由+calledContract+发出，我们从事件中的最后一个参数可以看到。

\+make\_calls+中的下一次调用是对库的调用：

```
calledLibrary.calledFunction();
```

它看起来与我们调用合约的方式完全相同，但行为非常不同。我们来看看发出的第二个事件：

```
sender: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
origin: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
from: '0x8f0483125fcb9aaaefa9209d8e9d7b9c8b9fb90f'
```

这一次，msg.sender+不是+caller+的地址。相反，它是我们钱包的地址，与交易来源相同。这是因为当你调用一个库时，这个调用总是+delegatecall+并且在调用者的上下文中运行。所以，当+calledLibrary+代码运行时，它继承+caller+的执行上下文，就好像它的代码在+caller+中运行一样。变量+this（在发出的事件中显示为+from+）是+caller+的地址，即使它是从+calledLibrary+内部访问的。

接下来的两个调用，使用低级+call+和+delegatecall+，验证我们的期望，发出与我们刚刚看到的事件相同的结果。

#### 安全考虑 <a href="#user-content-security_sec" id="user-content-security_sec"></a>

在编写智能合约时，安全是最重要的考虑因素之一。与其他程序一样，智能合约将完全按写入的内容执行，这并不总是程序员所期望的。此外，所有智能合约都是公开的，任何用户都可以通过创建交易来与他们进行交互。任何漏洞都可以被利用，损失几乎总是无法恢复。

在智能合约编程领域，错误代价高昂且容易被利用。因此，遵循最佳实践并使用经过良好测试的设计模式至关重要。

_防御性编程_ \_Defensive programming\_是一种编程风格，特别适用于智能合约编程，具有以下特点：

极简/简约

复杂性是安全的敌人。代码越简单，代码越少，发生错误或无法预料的效果的可能性就越小。当第一次参与智能合约编程时，开发人员试图编写大量代码。相反，你应该仔细查看你的智能合约代码，并尝试找到更少的方法，使用更少的代码行，更少的复杂性和更少的“功能”。如果有人告诉你他们的项目产生了“数千行代码”，那么你应该质疑该项目的安全性。更简单更安全。

代码重用

尽可能不要“重新发明轮子”。如果库或合约已经存在，可以满足你的大部分需求，请重新使用它。在你自己的代码中，遵循DRY原则：不要重复自己。如果你看到任何代码片段重复多次，请问自己是否可以将其作为函数或库进行编写并重新使用。已被广泛使用和测试的代码可能比你编写的任何新代码更安全。谨防“Not-Invented-Here”的态度，如果你试图通过从头开始构建“改进”某个功能或组件。安全风险通常大于改进值。

代码质量

智能合约代码是无情的。每个错误都可能导致经济损失。你不应该像通用编程一样对待智能合约编程。相反，你应该采用严谨的工程和软件开发方法论，类似于航空航天工程或类似的不容乐观的工程学科。一旦你“启动”你的代码，你就无法解决任何问题。

可读性/可审核性

你的代码应易于理解和清晰。阅读越容易，审计越容易。智能合约是公开的，因为任何人都可以对字节码进行逆向工程。因此，你应该使用协作和开源方法在公开场合开发你的工作。你应该编写文档良好，易于阅读的代码，遵循作为以太坊社区一部分的样式约定和命名约定。

测试覆盖

测试你可以测试的所有内容。智能合约运行在公共执行环境中，任何人都可以用他们想要的任何输入执行它们。你绝不应该假定输入（比如函数参数）是正确的，并且有一个良性的目的。测试所有参数以确保它们在预期的范围内并且格式正确。

**常见的安全风险**

智能合约程序员应该熟悉许多最常见的安全风险，以便能够检测和避免使他们面临这些风险的编程模式。

**重入 Re-entrancy**

重入是编程中的一种现象，函数或程序被中断，然后在先前调用完成之前再次调用。在智能合约编程的情况下，当合约A调用合约B中的一个函数时，可能会发生重入，合约B又调用合约A中的相同函数，导致递归执行。在合约状态在关键性调用结束之后才更新的情况下，这可能是特别危险的。

为了理解这一点，想象一下通过钱包合约调用银行合约的提现操作。合约A在合约B中调用提现功能，试图提取金额X。这种情况将涉及以下操作：

1. 合约B检查A是否有必要的余额来提取X。
2. B将X传送到A的地址（运行A的payable fallback函数）
3. B更新A的余额以反映此次提现

无论何时向合约发送付款（如本例中），接收方合约（A）都有机会执行\_payable\_函数，例如默认的fallback函数。但是，恶意攻击者可以利用这种执行。想象一下，在A的payable fallback中，合约A\_再次\_调用B银行的提款功能。B的提现功能现在将经历重入，因为现在相同的初始交易正在引发循环调用。

"(1) A 调用 B (2) B 调用 A 的 payable 函数 (1) A 再次调用 B "

在B的退出提现函数的第二次迭代中，B将再次检查A是否有可用余额。由于步骤3（其更新了A的余额）尚未执行，所以对于B来说，无论该函数被重新调用多少次，A仍然具有可用资金来提现。只要有gas可以继续运行，就可以重复该循环。当A检测到gas量不足时，它可以在payable函数中停止呼叫B. B将最终执行步骤3，从A的余额中扣除X. 然而，这时，B可能已经执行了数百次转账，并且只扣除了一次费用。在这次袭击中，A有效地洗劫了B的资金。

这个漏洞因其与DAO攻击的相关性而特别出名。用户利用了这样一个事实，即在调用转移并提取价值数百万美元的ether后，合约中的余额才发生变化。

为了防止重入，最好的做法是让程序员使用\_Checks-Effects-Interactions\_模式，在进行调用之前应用函数调用的影响（例如减少余额）。在我们的例子中，这意味着切换步骤3和2：在传输之前更新用户的余额。

在以太坊，这是完全没问题的，因为交易的所有影响都是原子的，这意味着在没有支付给用户的情况下更新余额是不可能的。要么都发生，要么抛出异常，都不会发生。这样可以防止重入攻击，因为所有后续调用原始提现函数的操作都会遇到正确的修改后余额。通过切换这两个步骤，可以防止A的提现金额超过其余额。

**设计模式**

任何编程范式的软件开发人员通常都会遇到以行为，结构，交互和创建为主题的重复设计挑战。通常这些问题可以概括并重新应用于未来类似性质的问题。当给定正式结构时，这些概括称为\*设计模式\*。智能合约有自己的一系列重复出现的设计问题，可以使用下面描述的一些模式来解决。

在智能合约的发展中存在着无数的设计问题，因此无法讨论所有这些问题 这里。因此，本节将重点讨论智能合约设计中最常见的三类问题分类：**访问控制（access control）**，**状态流（state flow）\*和\*资金支出（fund disbursement）**。

在本节中，我们将制定一份合约，最终将包含所有这三种设计模式。该合约将运行投票系统，允许用户对“真相”进行投票。该合约将提出一项声明，例如“小熊队赢得世界系列赛”。或者“纽约市正在下雨”，然后用户会有机会选择真或假。如果大多数参与者投票赞成"真"合约就认为该声明为真，如果大多数参与者投票赞成“假”，则合约将认为该声明为“假”。为了激励真实性，每次投票必须向合约发送100 ether，而失败的少数派出的资金将分给大多数。大多数参与者将从少数人中获得他们的部分奖金以及他们的初始投资。

这个“真相投票”系统实际上是Gnosis的基础，Gnosis是一个建立在以太坊之上的预测工具。有关Gnosis的更多信息，请访问：[https://gnosis.pm/](https://gnosis.pm)

**访问控制 Access control**

访问控制限制哪些用户可以调用合约功能。例如，真相投票合约的所有者可能决定限制那些可以参与投票的人。 为了达到这个目标，合约必须施加两个访问限制：

1. 只有合约的所有者可以将新用户添加到“允许的选民”列表中
2. 只有允许的选民可以投票

Solidity函数修饰器提供了一个简洁的方式来实现这些限制。

\_Note: 以下示例在修改器主体内使用下划线分号。这是Solidity的功能，用于告知编译器何时运行被修饰的函数的主体。开发人员可以认为被修饰的函数的主体将被复制到下划线的位置。

```
pragma solidity ^0.4.21;

contract TruthVote {

    address public owner = msg.sender;

    address[] true_votes;
    address[] false_votes;
    mapping (address => bool) voters;
    mapping (address => bool) hasVoted;

    uint VOTE_COST = 100;

    modifier onlyOwner() {
        require(msg.sender == owner);
        _;
    }

    modifier onlyVoter() {
        require(voters[msg.sender] != false);
        _;
    }

    modifier hasNotVoted() {
        require(hasVoted[msg.sender] == false);
        _;
    }

    function addVoter(address voter)
        public
        onlyOwner()
    {
        voters[voter] = true;
    }

    function vote(bool val)
        public
        payable
        onlyVoter()
        hasNotVoted()
    {
        if (msg.value >= VOTE_COST) {
            if (val) {
                true_votes.push(msg.sender);
            } else {
                false_votes.push(msg.sender);
            }
            hasVoted[msg.sender] = true;
        }
    }
}
```

**修饰器和函数的说明：**

* **onlyOwner**: 这个修饰器可以修饰一个函数，使得函数只能被地址与\*owner\*相同的发送者调用。
* **onlyVoter**: 这个修饰器可以修饰一个函数，使得函数只能被已登记的选举人调用。
* **addVoter(voter)**: 此函数用于将选民添加到选民列表。该功能使用\*onlyOwner\*修饰器，因此只有该合约的所有者可以调用它。
* **vote(val)**: 这个函数被投票者用来对所提出的命题投下真或假。它用\*onlyVoter\*修饰器装饰，所以只有已登记的选民可以调用它。

**状态流 State flow**

许多合约将需要一些操作状态的概念。合约的状态将决定合约的行为方式以及在给定的时间点提供的操作。让我们回到我们的真实投票系统来获得更具体的例子。

我们投票系统的运作可以分为三个不同的状态。

1. **Register**: 服务已创建，所有者现在可以添加选民。
2. **Vote**: 所有选民投票。
3. **Disperse**: 投票付款被分给大多数参与者。

以下代码继续建立在访问控制代码的基础上，但进一步将功能限制在特定状态。 在Solidity中，使用枚举值来表示状态是司空见惯的事情。

```
pragma solidity ^0.4.21;

contract TruthVote {
    enum States {
        REGISTER,
        VOTE,
        DISPERSE
    }

    address public owner = msg.sender;

    uint voteCost;

    address[] trueVotes;
    address[] falseVotes;


    mapping (address => bool) voters;
    mapping (address => bool) hasVoted;

    uint VOTE_COST = 100;

    States state;

    modifier onlyOwner() {
        require(msg.sender == owner);
        _;
    }

    modifier onlyVoter() {
        require(voters[msg.sender] != false);
        _;
    }

    modifier isCurrentState(States _stage) {
        require(state == _stage);
        _;
    }

    modifier hasNotVoted() {
        require(hasVoted[msg.sender] == false);
        _;
    }

    function startVote()
        public
        onlyOwner()
        isCurrentState(States.REGISTER)
    {
        goToNextState();
    }

    function goToNextState() internal {
        state = States(uint(state) + 1);
    }

    modifier pretransition() {
        goToNextState();
        _;
    }

    function addVoter(address voter)
        public
        onlyOwner()
        isCurrentState(States.REGISTER)
    {
        voters[voter] = true;
    }

    function vote(bool val)
        public
        payable
        isCurrentState(States.VOTE)
        onlyVoter()
        hasNotVoted()
    {
        if (msg.value >= VOTE_COST) {
            if (val) {
                trueVotes.push(msg.sender);
            } else {
                falseVotes.push(msg.sender);
            }
            hasVoted[msg.sender] = true;
        }
    }

    function disperse(bool val)
        public
        onlyOwner()
        isCurrentState(States.VOTE)
        pretransition()
    {
        address[] memory winningGroup;
        uint winningCompensation;
        if (trueVotes.length > falseVotes.length) {
            winningGroup = trueVotes;
            winningCompensation = VOTE_COST + (VOTE_COST*falseVotes.length) / trueVotes.length;
        } else if (trueVotes.length < falseVotes.length) {
            winningGroup = falseVotes;
            winningCompensation = VOTE_COST + (VOTE_COST*trueVotes.length) / falseVotes.length;
        } else {
            winningGroup = trueVotes;
            winningCompensation = VOTE_COST;
            for (uint i = 0; i < falseVotes.length; i++) {
                falseVotes[i].transfer(winningCompensation);
            }
        }

        for (uint j = 0; j < winningGroup.length; j++) {
            winningGroup[j].transfer(winningCompensation);
        }
    }
}
```

**修饰器和函数的说明：**

* **isCurrentState**: 在继续执行装饰函数之前，此修饰器将要求合约处于指定状态。
* **pretransition**: 在执行装饰函数的其余部分之前，此修饰器将转换到下一个状态
* **goToNextState**: 将合约转换到下一个状态的函数
* **disperse**: 计算大多数以及相应的瓜分奖金的功能。只有owner可以调用这个函数来正式结束投票。
* **startVote**: 所有者可用于开始投票的功能。

注意到允许所有者随意关闭投票流程可能会导致合约的滥用很重要。在更真实的实现中，投票期应在公众理解的时间段后结束。对于这个例子，这没问题。

现在增加的内容确保只有在owner决定开始投票阶段时才允许投票，用户只能在投票前由owner注册，并且在投票结束后才能分配资金。

**提现 Withdraw**

许多合约将为用户从中提取资金提供一些方法。在我们的示例中，属于大多数的用户在合约开始分配资金时直接接收资金。虽然这看起来有效，但它是一种欠考虑的解决方案。在\*disperse\*中\*addr.send()**调用的接收地址可以是一个合约，具有一个会失败的fallback函数，会打断\*disperse**。这有效地阻止了更多的参与者接收他们的收入。 一个更好的解决方案是提供一个用户可以调用来收取收入的提款功能。

```
...

enum States {
    REGISTER,
    VOTE,
    DETERMINE,
    WITHDRAW
}

mapping (address => bool) votes;
uint trueCount;
uint falseCount;

bool winner;
uint winningCompensation;

modifier posttransition() {
    _;
    goToNextState();
}

function vote(bool val)
    public
    onlyVoter()
    isCurrentStage(State.VOTE)
{
    if (votes[msg.sender] == address(0) && msg.value >= VOTE_COST) {
        votes[msg.sender] = val;
        if (val) {
            trueCount++;
        } else {
            falseCount++;
        }
    }
}

function determine(bool val)
    public
    onlyOwner()
    isCurrentState(State.VOTE)
    pretransition()
    posttransition()
{
    if (trueCount > falseCount) {
        winner = true;
        winningCompensation = VOTE_COST + (VOTE_COST*false_votes.length) / true_votes.length;
    } else if (falseCount > trueCount) {
        winner = false;
        winningCompensation = VOTE_COST + (VOTE_COST*true_votes.length) / false_votes.length;
    } else {
        winningCompensation = VOTE_COST;
    }
}

function withdraw()
    public
    onlyVoter()
    isCurrentState(State.WITHDRAW)
{
    if (votes[msg.sender] != address(0)) {
        if (votes[msg.sender] == winner) {
            msg.sender.transfer(winningCompensation);
        }
    }
}

...
```

**修饰器和（更新）功能的说明：**

* **posttransition**: 函数调用后转换到下一个状态。
* **determine**: 此功能与以前的\*disperse\*功能非常相似，除了现在只计算赢家和获胜赔偿金额，实际上并未发送任何资金。
* **vote**: 投票现在被添加到votes mapping，并使用真/假计数器。
* **withdraw**: 允许投票者提取胜利果实（如果有）。

这样，如果发送失败，则只在一个特定的调用者上失败，不影响其他用户提取他们的胜利果实。

**合约库**

**安全最佳实践**

也许最基本的软件安全原则是最大限度地重用可信代码。在区块链技术中，这甚至会凝结成一句格言：“Do not roll your own crypto”。就智能合约而言，这意味着尽可能多地从经社区彻底审查的免费库中获益。

**进一步阅读**

应用程序二进制接口（ABI）是强类型的，在编译时和静态时都是已知的。所有合约都有他们打算在编译时调用的任何合约的接口定义。
