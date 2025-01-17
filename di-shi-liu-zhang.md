# 第十六章

Permalink

Cannot retrieve contributors at this time

### Vyper: 面向合约的编程语言 <a href="#user-content-viper_chap" id="user-content-viper_chap"></a>

Vyper是一种面向合约的实验性编程语言，面向以太坊虚拟机（EVM）。Vyper致力于通过简化代码并使其对人类可读而提供卓越的审计能力。Vyper的一个原则是让开发人员几乎不可能编写误导性代码。这可以通过多种方式完成，我们将在下面介绍。

#### 与 Solidity 比较 <a href="#user-content-comparison_to_solidity_sec" id="user-content-comparison_to_solidity_sec"></a>

本节是那些正在考虑使用Vyper编程语言开发智能合约的人的参考。该部分主要对比了Vyper与Solidity的对比； 概览，合理的推理，为什么Vyper不包括以下传统的面向对象编程（OOP）概念：

Modifiers

在Solidity中，你可以使用修饰器编写函数。例如，以下函数\`changeOwner\`将在一个名为\`onlyBy\`的修饰器中运行代码，作为其执行的一部分。

```
function changeOwner(address _newOwner)
    public
    onlyBy(owner)
{
    owner = _newOwner;
}
```

正如我们在下面看到的，名为\`onlyBy\`的修饰器强制执行与所有权相关的规则。虽然修饰器很强大（能够改变函数体中发生的事情），但它们也可能导致误导性的代码执行。例如，确保\`changeOwner\`函数逻辑的唯一方法是每次实现代码时检查并测试\`onlyBy\`修饰器。显然，如果将来更改修改器，则调用它的函数可能会产生与最初预期不同的结果。

```
modifier onlyBy(address _account)
{
    require(msg.sender == _account);
    _;
}
```

总的来说，修饰器的通常用例是在函数执行之前执行单个检查。鉴于这种情况，Vyper的建议是完全取消修饰器，并简单地使用内联检查和断言作为函数的一部分。这样做将提高审计能力和可读性，因为Vyper函数将在明显的视线中遵循逻辑内联序列，而不必引用已在别处编写的修饰器代码。

类继承

继承允许程序员通过从现有软件库中获取预先存在的功能，属性和行为来利用预先编写的代码。继承功能强大，可以促进代码的重用。Solidity支持多重继承以及多态，虽然这些被认为是面向对象编程的一些最重要的特性，但Vyper并不支持它们。Vyper坚持认为继承的实现要求编码人员和审计人员在多个文件之间跳转，以便了解程序正在做什么。Vyper还了解优先级规则以及多个继承如何使代码过于复杂而无法理解。鉴于Solidity [关于继承的文档](https://github.com/ethereum/solidity/blob/release/docs/contracts#inheritance)给出了多重继承为何有问题的例子，这是一个公平的陈述。

内联汇编

内联汇编为开发人员提供了以低级别访问以太坊虚拟机（EVM）的机会。使用内联汇编代码（在更高级别的源代码中）时，开发人员可以通过直接访问EVM操作码指令来执行操作。例如，以下内联汇编代码通过使用EVM操作码mload在内存位置0x80处添加3。

```
3 0x80 mload add 0x80 mstore
```

如前所述，Vyper致力于为开发人员和代码审计人员提供最易读的代码。虽然内联汇编可以提供强大的细粒度控制，但Vyper编程语言不支持它。

函数重载

具有相同名称和不同参数选项的多个函数定义会导致在任何给定时间调用哪个函数时会产生很多混淆。随着函数重载，编写误导代码会更容易（ foo（“hello”）记录“hello”但foo（“hello”，“world”）窃取你的资金。）函数重载的另一个问题是它使代码更难以搜索，因为你必须跟踪哪个调用指的是哪个功能。

变量类型转换

类型转换是一种允许程序员将变量从一种数据类型转换为另一种数据类型的机制。

前置条件和后置条件

Vyper明确处理前置条件，后置条件和状态更改。虽然这会产生冗余代码，但它也允许最大的可读性和安全性。在Vyper中编写智能合约时，开发人员应遵守以下3点。理想情况下，应仔细考虑3个点中的每个点，然后在代码中进行详细记录。这样做将改进代码的设计，最终使代码更具可读性和可审计性。

* 条件 - 以太坊状态变量的当前状态/条件是什么
* 效果 - 这个智能合约代码对执行状态变量的条件有什么影响，即什么会影响，什么不会受到影响？这些影响是否与智能合约的意图一致？
* 交互 - 现在已经详尽地处理了前两个步骤，现在是运行代码的时候了。在部署之前，逻辑上逐步执行代码并考虑执行代码的所有可能的永久结果，后果和方案，包括与其他合约的交互。

#### 一种新的编程范式 <a href="#user-content-a_new_programming_paradigm_sec" id="user-content-a_new_programming_paradigm_sec"></a>

Vyper的创作为新的编程范式打开了大门。例如，Vyper正在删除类继承以及其他功能，因此可以说Vyper偏离了传统的面向对象编程（OOP）范例，这很好。

历史上，OOP提供了一种表示现实世界对象的机制。例如，OOP允许实例化可以从person类继承的employee对象。然而，从价值转移和/或智能合约的角度来看，那些渴望功能性编程范式的人会同意，交易性编程绝不适合上述传统的OOP范式。简而言之，交易计算是与现实世界对象分开的世界。例如，你最后一次持有交易或正向链接业务规则的时间是什么时候？

似乎Vyper没有与OOP范例或函数式编程范例完全一致（完整的原因列表超出了本章的范围）。出于这个原因，在开发的早期阶段，我们能够如此大胆地推出新的软件开发范例吗？一个致力于未来证明区块链可执行代码的人。一个可以防止在不可改变的环境中造成灾难性资金损失的人。区块链革命中经历的过去事件有机地为这一领域的进一步研究和发展创造了新的机会。也许这种研究和开发的结果最终可能导致软件开发的新的不变性范式分类。

#### 装饰符 <a href="#user-content-decorators_sec" id="user-content-decorators_sec"></a>

向 `@private` `@public` `@constant` `@payable` 这样的装饰符在每个函数的开头声明。

Private

`@private` 使合约外部的函数无法访问此函数。

Public

`@public` 使该函数公开可见和可执行。例如，即使是以太坊钱包也会在查看合约时显示公共函数。

Constant

以 `@constant` 开始的函数不允许状态变量的改变，实际上，如果函数尝试更改状态变量，编译器将拒绝整个程序（带有适当的警告）。如果该函数用于更改状态变量，则不要在函数的开头使用\`@ constant\`。

Payable

只有以 `@payable` 开头声明的函数才能接收价值。

Vyper明确地实现了装饰符的逻辑。例如，如果一个函数前面有一个\`@appay\`装饰符和一个\`@ constant\`装饰符，那么Vyper代码编译过程就会失败。当然，这是有道理的，因为常量函数（仅从全局状态读取的函数）永远不需要参与值的转移。此外，每个Vyper函数必须以\`@ public\`或\`@private\`装饰符开头，以避免编译失败。同时使用\`@public\`装饰符和\`@private\`装饰符的Vyper函数也会导致编译失败。

#### 在线代码编辑器和编译器 <a href="#user-content-online_code_editor_and_compiler_sec" id="user-content-online_code_editor_and_compiler_sec"></a>

Vyper在以下URL \<https://vyper.online> 上有自己的在线代码编辑器和编译器。这个Vyper在线编译器允许你仅使用Web浏览器编写智能合约，然后将其编译为字节码，ABI和LLL。Vyper在线编译器具有各种预先编写的智能合约，以方便你使用。这些包括简单的公开拍卖，安全的远程购买，ERC20 token等。

#### 使用命令行编译 <a href="#user-content-compiling_using_the_command_line_sec" id="user-content-compiling_using_the_command_line_sec"></a>

每个Vyper合约都保存在扩展名为.v.py的单个文件中。 安装完成后，Vyper可以通过运行以下命令来编译和提供字节码

vyper \~/hello\_world.v.py

通过运行以下命令可以获得人类可读的ABI代码（JSON格式）

vyper -f json \~/hello\_world.v.py

#### 读写数据 <a href="#user-content-reading_and_writing_data_sec" id="user-content-reading_and_writing_data_sec"></a>

智能合约可以将数据写入两个地方，即以太坊的全球状态查找树或以太坊的链数据。虽然存储，读取和修改数据的成本很高，但这些存储操作是大多数智能合约的必要组成部分。

全局状态

给定智能合约中的状态变量存储在以太坊的全局状态查找树中，给定的智能合约只能存储，读取和修改与该合约地址相关的数据（即智能合约无法读取或写入其他智能合约）。

Log

如前所述，智能合约也可以通过日志事件写入以太坊的链数据。虽然Vyper最初使用 \_\_log\_\_ 语法来声明这些事件，但已经进行了更新，使Vyper的事件声明更符合Solidity的原始语法。例如，Vyper声明的一个名为MyLog的事件最初是 `MyLog: __log__({arg1: indexed(bytes[3])})`，Vyper的语法现在变为 `MyLog: event({arg1: indexed(bytes[3])})`。需要注意的是，在Vyper中执行日志事件仍然是如下 `log.MyLog("123")`。

虽然智能合约可以写入以太坊的链数据（通过日志事件），但智能合约无法读取他们创建的链上日志事件。尽管如此，通过日志事件写入以太坊的链数据的一个好处是，可以在公共链上由轻客户端发现和读取日志。例如，挖到的块中的logsBloom值可以指示是否存在日志事件。一旦建立，就可以通过日志路径获取 logs → data inside a given transaction receipt。

#### ERC20令牌接口实现 <a href="#user-content-erc20_token_interface_implementation_sec" id="user-content-erc20_token_interface_implementation_sec"></a>

Vyper已将ERC20实施为预编译合约，并允许默认使用它。 Vyper中的合约必须声明为全局变量。声明ERC20变量的示例可以是

token: address(ERC20)

#### 操作码（OPCODES） <a href="#user-content-opcodes_sec" id="user-content-opcodes_sec"></a>

智能合约的代码主要使用Solidity或Vyper等高级语言编写。编译器负责获取高级代码并创建它的低级解释，然后可以在以太坊虚拟机（EVM）上执行。编译器可以提取代码的最低表示（在EVM执行之前）是操作码。在这种情况下，需要高级语言（如Vyper）的每个实现来提供适当的编译机制（编译器）以允许（除其他之外）将高级代码编译到通用预定义的EVM操作码中。一个很好的例子是Vyper实现了以太坊的分片操作码。



<details>

<summary></summary>



</details>
