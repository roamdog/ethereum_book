# 第十四章

#### 这是什么？ <a href="#user-content-evm_description" id="user-content-evm_description"></a>

实际处理内部状态和计算的协议部分称为以太坊虚拟机（EVM）。从实际角度来看，EVM可以被认为是包含数百万个对象的大型去中心化计算机。

**比较**

* 虚拟机（Virtual Machine）（Virtualbox, QEMU, 云计算）
* Java 虚拟机（VM）

虚拟机技术（如Virtualbox和QEMU / KVM）与EVM的不同之处在于它们的目的是提供管理程序功能，或者处理客户操作系统与底层主机操作系统和硬件之间的系统调用，任务调度和资源管理的软件抽象。

然而，Java VM（JVM）规范的某些方面确实包含与EVM的相似之处。从高级概述来看，JVM旨在提供与底层主机操作系统或硬件无关的运行时环境，从而实现各种系统的兼容性。在JVM上运行的高级程序语言（如Java或Scala）被编译到相应的指令集字节码中。这与编译要在EVM上运行的Solidity源文件相当。

**EVM机器语言（字节码操作）**

EVM机器语言分为特定的指令集组，例如算术运算，逻辑和比较运算，控制流，系统调用，堆栈操作和存储器操作。除典型的字节码操作外，EVM还必须管理账户信息（即地址和余额），当前gas价格和区块信息。

```
POP     // 项目出栈
PUSH    // 项目入栈
MLOAD   // 将项目加载到内存中
MSTORE  // 在内存中存储项目
JUMP    // 改变程序计数器的位置
PC      // 程序计数器
MSIZE   // 活动的内存大小
GAS     // 交易可用的gas数量
DUP     // 复制栈项目
SWAP    // 交换栈项目
```

```
CREATE  // 创建新的账户
CALL    // 在账户间传递消息的指令
RETURN  // 执行停机
REVERT  // 执行停机，恢复状态更改
SELFDESTRUCT // 执行停机，并标记账户为删除的
```

```
添加//添加
MUL //乘法
SUB //减法
DIV //整数除法
SDIV //有符号整数除法
MOD // Modulo（剩余）操作
SMOD //签名模运算
ADDMOD //模数加法
MULMOD //模数乘法
EXP //指数运算
STOP //停止操作
```

```
ADDRESS //当前执行账户的地址
BALANCE	//账户余额
CALLVALUE //执行环境的交易值
ORIGIN //执行环境的原始地址
CALLER //执行调用者的地址
CODESIZE //执行环境代码大小
GASPRICE //gas价格状态
EXTCODESIZE //账户的代码大小
RETURNDATACOPY //从先前的内存调用输出的数据的副本
```

**状态**

与任何计算系统一样，状态概念也很重要。就像CPU跟踪执行过程一样，EVM必须跟踪各种组件的状态以支持交易。这些组件的状态最终会推动总体区块链的变化程度。这方面导致将以太坊描述为\_基于交易的状态机\_，包含以下组件：

World State

160位地址标识符和账户状态之间的映射，在不可变的\_Merkle Patricia Tree\_数据结构中维护。

Account State

包含以下四个组件：

* _nonce_：表示从该相应账户发送的交易数量的值。
* _balance_：账户地址拥有的\_wei\_的数量。
* _storageRoot_：Merkle Patricia Tree根节点的256位哈希值。
* _codeHash_：各个账户的EVM代码的不可变哈希值。

Storage State

在EVM上运行时维护的账户特定状态信息。

Block State

交易所需的状态值包括以下内容：

* _blockhash_：最近完成的块的哈希值。
* _coinbase_：收件人的地址。
* _timestamp_：当前块的时间戳。
* _number_：当前块的编号。
* _difficulty_：当前区块的难度。
* _gaslimit_：当前区块的gas限制。

Runtime Environment Information

用于使用交易的信息。

* _gasprice_：当前汽油价格，由交易发起人指定。
* _codesize_：交易代码库的大小。
* _caller_：执行当前交易的账户的地址。
* _origin_：当前交易原始发件人的地址。

状态转换使用以下函数计算：

以太坊状态转换函数

用于计算\_valid state transition\_。

区块终结状态转换函数

用于确定最终块的状态，作为挖矿过程的一部分，包含区块奖励。

区块级状态转换函数

应用于交易状态时的区块终结状态转换函数的结果状态。

**将Solidity编译为EVM字节码**

可以通过命令行完成将Solidity源文件编译为EVM字节码。有关其他编译选项的列表，只需运行以下命令：

使用\_—​opcodes\_命令行选项可以轻松实现生成Solidity源文件的原始操作码流。此操作码流会遗漏一些信息（\_—​asm\_选项会生成完整信息），但这对于第一次介绍是足够的。例如，编译示例Solidity文件\_Example.sol\_并将操作码输出填充到名为\_BytecodeDir\_的目录中，使用以下命令完成：

```
$ solc -o BytecodeOutputDir --opcodes Example.sol
```

或

```
$ solc -o BytecodeOutputDir --asm Example.sol
```

以下命令将为我们的示例程序生成字节码二进制文件：

```
$ solc -o BytecodeOutputDir --bin Example.sol
```

生成的输出操作码文件将取决于Solidity源文件中包含的特定合约。我们的简单Solidity文件\_Example.sol\_ [\[simple\_solidity\_example\]](broken-reference)只有一个名为“example”的合约。

```
pragma solidity ^0.4.19;

contract example {

  address contractOwner;

  function example() {
    contractOwner = msg.sender;
  }
}
```

如果查看\_BytecodeDir\_目录，你将看到操作码文件\_example.opcode\_（请参阅[\[simple\_solidity\_example\]](broken-reference)），其中包含“example”合约的EVM机器语言操作码指令。在文本编辑器中打开\_example.opcode\_文件将显示以下内容：

```
PUSH1 0x60 PUSH1 0x40 MSTORE CALLVALUE ISZERO PUSH1 0xE JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST CALLER PUSH1 0x0 DUP1 PUSH2 0x100 EXP DUP2 SLOAD DUP2 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF MUL NOT AND SWAP1 DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND MUL OR SWAP1 SSTORE POP PUSH1 0x35 DUP1 PUSH1 0x5B PUSH1 0x0 CODECOPY PUSH1 0x0 RETURN STOP PUSH1 0x60 PUSH1 0x40 MSTORE PUSH1 0x0 DUP1 REVERT STOP LOG1 PUSH6 0x627A7A723058 KECCAK256 JUMP 0xb9 SWAP14 0xcb 0x1e 0xdd RETURNDATACOPY 0xec 0xe0 0x1f 0x27 0xc9 PUSH5 0x9C5ABCC14A NUMBER 0x5e INVALID EXTCODESIZE 0xdb 0xcf EXTCODESIZE 0x27 EXTCODESIZE 0xe2 0xb8 SWAP10 0xed 0x
```

使用\_—​asm\_选项编译示例会在\_BytecodeDir\_目录中生成一个文件 _example.evm_。这包含详细的EVM机器语言说明：

```
/* "Example.sol":26:132  contract example {... */
  mstore(0x40, 0x60)
    /* "Example.sol":74:130  function example() {... */
  jumpi(tag_1, iszero(callvalue))
  0x0
  dup1
  revert
tag_1:
    /* "Example.sol":115:125  msg.sender */
  caller
    /* "Example.sol":99:112  contractOwner */
  0x0
  dup1
    /* "Example.sol":99:125  contractOwner = msg.sender */
  0x100
  exp
  dup2
  sload
  dup2
  0xffffffffffffffffffffffffffffffffffffffff
  mul
  not
  and
  swap1
  dup4
  0xffffffffffffffffffffffffffffffffffffffff
  and
  mul
  or
  swap1
  sstore
  pop
    /* "Example.sol":26:132  contract example {... */
  dataSize(sub_0)
  dup1
  dataOffset(sub_0)
  0x0
  codecopy
  0x0
  return
stop

sub_0: assembly {
        /* "Example.sol":26:132  contract example {... */
      mstore(0x40, 0x60)
      0x0
      dup1
      revert

    auxdata: 0xa165627a7a7230582056b99dcb1edd3eece01f27c9649c5abcc14a435efe3bdbcf3b273be2b899eda90029
}
```

_--bin_ 选项产生以下内容：

```
60606040523415600e57600080fd5b336000806101000a81548173
ffffffffffffffffffffffffffffffffffffffff
021916908373
ffffffffffffffffffffffffffffffffffffffff
160217905550603580605b6000396000f3006060604052600080fd00a165627a7a7230582056b99dcb1e
```

让我们检查前两条指令（参考[\[common\_stack\_opcodes\]](broken-reference)）：

这里我们有\_mnemonic\_“PUSH1”，后跟一个值为“0x60”的原始字节。这对应于EVM指令，该操作将操作码之后的单字节解释为文字值并将其推入堆栈。可以将大小最多为32个字节的值压入堆栈。例如，以下字节码将4字节值压入堆栈：

第二个push操作码将“0x40”存储到堆栈中（在那里已存在的“0x60”之上）。

接下来的两个指令：

MSTORE是一个堆栈/内存操作（参见[\[common\_stack\_opcodes\]](broken-reference)），它将值保存到内存中，而CALLVALUE是一个环境操作码（参见[\[common\_environment\_opcodes\]](broken-reference)），它返回正在执行的消息调用的存放值。

**执行EVM字节码**

**Gas，会计**

对于每个交易，都有一个关联的\_gas-limit\_和\_gas-price\_，它们构成了EVM执行的费用。这些费用用于促进交易的必要资源，例如计算和存储。gas还用于创建账户和智能合约。

**图灵完备性和gas**

简单来说，如果系统或编程语言可以解决你输入的任何问题，它是\_图灵完备的\_。这在以太坊黄皮书中讨论过：

> It is a _quasi_-Turing complete machine; the quasi qualification comes from the fact that the computation is intrinsically bounded through a parameter, gas, which limits the total amount of computation done.

— Gavin Wood\
ETHEREUM: A SECURE DECENTRALISED GENERALISED TRANSACTION LEDGER

虽然EVM理论上可以解决它收到的任何问题，但gas可能会阻止它这样做。这可能在以下几个方面发生：

1）在以太坊开采的块具有与之相关的gas限制; 也就是说，区块内所有交易所使用的总gas不能超过一定限度。 2）由于gas和gas价格齐头并进，即使取消了gas限制，高度复杂的交易也可能在经济上不可行。

但是，对于大多数用例，EVM可以解决提供给它的任何问题。

**字节码与运行时字节码**

编译合约时，你可以获得\_合约字节码\_或\_运行时字节码\_。

合约字节码包含实际上最终位于区块链上的字节码\_以及\_将字节码放在区块链上并运行合约构造函数所需的字节码。

另一方面，运行时字节码只是最终位于区块链上的字节码。这不包括初始化合约并将其放在区块链上所需的字节码。

让我们以前面创建的简单\`Faucet.sol\`合约为例。

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

要获得合约字节码，我们将运行\`solc --bin Faucet.sol\`。如果我们只想要运行时字节码，我们将运行\`solc --bin-runtime Faucet.sol\`。

如果比较这些命令的输出，你将看到运行时字节码是合约字节码的子集。换句话说，运行时字节码完全包含在合约字节码中。

**反汇编字节码**

反汇编EVM字节码是了解高级别Solidity在EVM中的作用的好方法。你可以使用一些反汇编程序来执行此操作：

* **Porosity** 是一个流行的开源反编译器：[https://github.com/comaeio/porosity](https://github.com/comaeio/porosity)
* **Ethersplay** 是Binary Ninja的EVM插件，一个反汇编程序：[https://github.com/trailofbits/ethersplay](https://github.com/trailofbits/ethersplay)
* **IDA-Evm** 是IDA的EVM插件，另一个反汇编程序：[https://github.com/trailofbits/ida-evm](https://github.com/trailofbits/ida-evm)

在本节中，我们将使用 Binary Ninja 的 **Ethersplay** 插件。

在获取Faucet.sol的运行时字节码后，我们可以将其提供给Binary Ninja（在导入Ethersplay插件之后）以查看EVM指令。



Figure 1. Disassembling the Faucet runtime bytecode

当你将交易发送到智能合约时，交易首先会与该智能合约的**调度员（dispatcher）**进行交互。调度程序读入交易的数据字段并将其发送到适当的函数。

在熟悉的MSTORE指令之后，我们在编译的Faucet.sol合约中看到以下创建：

```
PUSH1 0x4
CALLDATASIZE
LT
PUSH1 0x3f
JUMPI
```

"PUSH1 0x4" 将0x4置于堆栈顶部，栈初始为空。“CALLDATASIZE”获取接收到的交易的calldata的大小（以字节为单位）并将其推送到堆栈中。当前堆栈如下所示：

Table 1. Current stack

| Stack                                 |
| ------------------------------------- |
| 0x4                                   |
| length of calldata from tx (msg.data) |

下一条指令是“LT”，是“小于（less than）”的缩写。LT指令检查堆栈上的顶部项是否小于堆栈上的下一项。在我们的例子中，它检查CALLDATASIZE的结果是否小于4个字节。

为什么EVM会检查交易的calldata是否至少为4个字节？因为函数标识符的工作原理。每个函数由其keccak256哈希的前四个字节标识。通过将函数的名称和它所采用的参数放入keccak256哈希函数，我们可以推导出它的函数标识符。在我们的合约中，我们有：

```
keccak256("withdraw(uint256)") = 0x2e1a7d4d...
```

因此，“withdraw（uint256）”函数的函数标识符是0x2e1a7d4d，因为它们是结果哈希的前四个字节。函数标识符总是4个字节长，所以如果发送给合约的交易的整个数据字段小于4个字节，那么除非定义了\_fallback函数\_，否则没有交易可能与之通信的函数。因为我们在Faucet.sol中实现了这样的fallback函数，所以当calldata的长度小于4个字节时，EVM会跳转到此函数。

如果msg.data字段少于4个字节，LT将弹出堆栈的前两个值并将1推到其上。否则，它会推入0。在我们的例子中，让我们假设发送给我们的合约的transaciton的msg.data字段\_was\_少于4个字节。

“PUSH1 0x3f”指令将字节“0x3f”压入堆栈。在此指令之后，堆栈如下所示：

Table 2. Current stack

| Stack |
| ----- |
| 1     |
| 0x3f  |

下一条指令是“JUMPI”，代表“jump if”。它的工作原理如下：

```
jumpi(label, cond) // Jump to "label" if "cond" is true
```

在我们的例子中，“label”是0x3f，这是我们的fallback函数存在于我们的智能合约中的地方。“cond”参数为1，它来自之前LT指令的结果。要将整个序列放入单词中，如果交易数据少于4个字节，则合约将跳转到fallback函数。



Figure 2. JUMPI instruction leading to fallback function

我们来看一下调度员的核心代码块。假设我们收到的长度大于4个字节的calldata，“JUMPI”指令不会跳转到回退函数。相反，代码执行将遵循下一条指令：

```
PUSH1 0x0
CALLDATALOAD
PUSH29 0x1000000...
SWAP1
DIV
PUSH4 0xffffffff
AND
DUP1
PUSH4 0x2e1a7d4d
EQ
PUSH1 0x41
JUMPI
```

“PUSH1 0x0”将0压入堆栈，否则为空。“CALLDATALOAD”接受发送到智能合约的calldata中的索引作为参数，并从该索引读取32个字节，如下所示：

```
calldataload(p) // call data starting from position p (32 bytes)
```

由于0是从PUSH1 0x0命令传递给它的索引，因此CALLDATALOAD从字节0开始读取32字节的calldata，然后将其推送到堆栈的顶部（在弹出原始0x0之后）。在“PUSH29 0x1000000 …​”指令之后，堆栈如下所示：

Table 3. Current stack

| Stack                                   |
| --------------------------------------- |
| 32 bytes of calldata starting at byte 0 |
| 0x1000000…​ (29 bytes in length)        |

“SWAP1”用它后面的\_第i个\_元素交换堆栈顶部元素。在这里，它与密钥数据交换0x1000000 …​ 新堆栈如下所示：

Table 4. Current stack

| Stack                                   |
| --------------------------------------- |
| 0x1000000…​ (29 bytes in length)        |
| 32 bytes of calldata starting at byte 0 |

下一条指令是“DIV”，其工作方式如下：

在这里，x = 32字节的calldata从字节0开始，y = 0x100000000 …​（总共29个字节）。你能想到调度员为什么要进行划分吗？这是一个提示：我们从索引0开始从calldata读取32个字节。该calldata的前四个字节是函数标识符。

我们之前推送的0x100000000 …​.长度为29个字节，由开头的1组成，后跟全0。将我们的32字节的calldata除以此0x100000000 …​.将只留下从索引0开始的callataload的\_topmost 4字节\_这四个字节 - 从索引0开始的calldataload中的前四个字节 - 是函数标识符，并且这就是EVM如何提取该字段。

如果你不清楚这一部分，可以这样想：在base10，1234000/1000 = 1234。在base16中，这没有什么不同。不是每个地方都是10的倍数，它是16的倍数。正如在我们的较小的例子中除以103（1000）只保留最顶部的数字，将我们的32字节基数16值除以1629做同样的事。

DIV（函数标识符）的结果被推送到堆栈上，我们的新堆栈如下：

Table 5. Current stack

| Stack                                |
| ------------------------------------ |
| function identifier sent in msg.data |

由于“PUSH4 0xffffffff”和“AND”指令是冗余的，我们可以完全忽略它们，因为堆栈在完成后将保持不变。“DUP1”指令复制堆栈上的1st项，这是函数标识符。下一条指令“PUSH4 0x2e1a7d4d”将抽取（uint256）函数的计算函数标识符推送到堆栈。堆栈现在看起来如下：

Table 6. Current stack

| Stack                                |
| ------------------------------------ |
| function identifier sent in msg.data |
| function identifier sent in msg.data |
| 0x2e1a7d4d                           |

下一条指令“EQ”弹出堆栈的前两项并对它们进行比较。这是调度程序完成其主要工作的地方：它比较交易的msg.data字段中发送的函数标识符是否与withdraw（uint256）匹配。如果它们相等，则EQ将1推入堆栈，这最终将用于跳转到fallback函数。否则，EQ将0推入堆栈。

假设发送给我们合约的交易确实以withdraw（uint256）的函数标识符开头，我们的新栈看起来如下：

Table 7. Current stack

| Stack                                |
| ------------------------------------ |
| function identifier sent in msg.data |
| 1                                    |

接下来，我们有“PUSH1 0x41”，这是withdraw（uint256）函数在合约中的地址。在此指令之后，堆栈如下所示：

Table 8. Current stack

| Stack                                |
| ------------------------------------ |
| function identifier sent in msg.data |
| 1                                    |
| 0x41                                 |

接下来是JUMPI指令，它再次接受堆栈上的前两个元素作为参数。在这种情况下，我们有“jumpi（0x41,1）”，它告诉EVM执行跳转到withdraw（uint256）函数的位置。
