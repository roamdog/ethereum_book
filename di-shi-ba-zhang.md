# 第十八章

[EIP-1](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1.md)

EIP Purpose and Guidelines

Martin Becze, Hudson Jameson

Meta

Final

[EIP-2](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-2.md)

Homestead Hard-fork Changes

Vitalik Buterin

Core

Final

[EIP-5](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-5.md)

Gas Usage for `RETURN` and `CALL`

Christian Reitwiessner

Core

Draft

[EIP-6](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-6.md)

Renaming Suicide Opcode

Hudson Jameson

Interface

Final

[EIP-7](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7.md)

`DELEGATECALL`

Vitalik Buterin

Core

Final

[EIP-8](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-8.md)

devp2p Forward Compatibility Requirements for Homestead

Felix Lange

Networking

Final

[EIP-20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md)

ERC-20 Token Standard. Describes standard functions a token contract may implement to allow DApps and Wallets to handle tokens across multiple interfaces/DApps. Methods include: `totalSupply()`, `balanceOf(address)`, `transfer`, `transferFrom`, `approve`, `allowance`. Events include: `Transfer` (triggered when tokens are transferred), `Approval` (triggered when `approve` is called).

Fabian Vogelsteller, Vitalik Buterin

ERC

Final

Frontier

[EIP-55](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-55.md)

ERC-55 Mixed-case checksum address encoding

Vitalik Buterin

ERC

Final

[EIP-86](https://github.com/ethereum/EIPs/blob/bd136e662fca4154787b44cded8d2a29b993be66/EIPS/abstraction.md)

Setting the stage for "abstracting out" account security, and allowing users creation of "account contracts" toward a model where in the long-term all accounts are contracts that can pay for gas, and users are free to defined their own security model (that perform any desired signature verification and nonce checks instead of using the in-protocol mechanism where ECDSA and default nonce scheme are the only "standard" way to secure an account, which is currently hard-coded into transaction processing).

Vitalik Buterin

Core

Deferred (to be replaced)

Constantinople

[EIP-96](https://github.com/ethereum/EIPs/pull/210)

Setting the Blockhash and state root refactoring to store blockhashes in the state to reduce protocol complexity and need for client implementation complexity necessary to process the `BLOCKHASH` opcode. Extends range of how far back blockhash checking may go, with the side effect of creating direct links between blocks with very distant block numbers to facilitate much more efficient initial Light Client syncing.

Vitalik Buterin

Core

Deferred

Constantinople

[EIP-100](https://github.com/ethereum/EIPs/issues/100)

Change formula that computes the difficulty of a block (difficulty adjustment algorithm) to target mean block time and take uncles into account.

Vitalik Buterin

Core

Final

Metropolis Byzantinium

[EIP-101](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-101.md)

Serenity Currency and Crypto Abstraction. Abstracting Ether up a level with the benefit of allowing Ether and sub-Tokens to be treated similarly by contracts, reducing level of indirection required for custom-policy accounts such as Multisigs, and purifying the underlying Ethereum protocol by reducing the minimal consensus implementation complexity

Vitalik Buterin

Active

Serenity feature

Serenity Casper

[EIP-105](https://blog.ethereum.org/2016/03/05/serenity-poc2/)

"Sharding scaffolding" EIP to allow Ethereum transactions to be parallelised using a binary tree sharding mechanism, and to set the stage for a later sharding scheme. Research in progress: [https://github.com/ethereum/sharding](https://github.com/ethereum/sharding)

Vitalik Buterin

Active

Serenity feature

Serenity Casper

[EIP-137](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-137.md)

Ethereum Domain Name Service - Specification

Nick Johnson

ERC

Final

[EIP-140](https://github.com/ethereum/EIPs/pull/206)

Add `REVERT` opcode instruction, which stops execution and rolls back the EVM execution state changes without consuming all provided gas (instead the contract only has to pay for memory) or losing logs, and returning to the caller a pointer to the memory location with the error code or message.

Alex Beregszaszi, Nikolai Mushegian

Core

Final

Metropolis Byzantinium

[EIP-141](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-141.md)

Designated invalid EVM instruction

Alex Beregszaszi

Core

Final

[EIP-145](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-145.md)

Bitwise shifting instructions in EVM

Alex Beregszaszi, Paweł Bylica

Core

Deferred

[EIP-150](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-150.md)

Gas cost changes for IO-heavy operations

Vitalik Buterin

Core

Final

[EIP-155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-155.md)

Simple Replay Attack Protection. Replay Attack allows any transaction using a pre-EIP155 Ethereum Node or Client to become signed so it is valid and executed on both the Ethereum and Ethereum Classic chains.

Vitalik Buterin

Core

Final

Homestead

[EIP-158](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-158.md)

State clearing

Vitalik Buterin

Core

Superseded

[EIP-160](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-160.md)

EXP cost increase

Vitalik Buterin

Core

Final

[EIP-161](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-161.md)

State trie clearing (invariant-preserving alternative\[EIP-161]

Gavin Wood

Core

Final

[EIP-162](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-162.md)

ERC-162 ENS support for reverse resolution of Ethereum addresses

Maurelian, Nick Johnson

ERC

Final

[EIP-165](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-165.md)

ERC-165 Standard Interface Detection

Christian Reitwiessner

Interface

Draft

[EIP-170](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-170.md)

Contract code size limit

Vitalik Buterin

Core

Final

[EIP-181](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-181.md)

ERC-181 ENS support for reverse resolution of Ethereum addresses

Nick Johnson

ERC

Final

[EIP-190](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-190.md)

ERC-190 Ethereum Smart Contract Packaging Standard

Merriam, Coulter, Erfurt, Catalano, Matias

ERC

Final

[EIP-196](https://github.com/ethereum/EIPs/pull/213)

Precompiled contracts for addition and scalar multiplication operations on the elliptic curve alt\_bn128, which are required in order to perform zkSNARK verification within the block gas limit

Christian Reitwiessner

Core

Final

Metropolis Byzantinium

[EIP-197](https://github.com/ethereum/EIPs/pull/212)

Precompiled contracts for optimal Ate pairing check of a pairing function on a specific pairing-friendly elliptic curve alt\_bn128 and is combined with EIP 196

Vitalik Buterin, Christian Reitwiessner

Core

Final

Metropolis Byzantinium

[EIP-198](https://github.com/ethereum/EIPs/pull/198)

Precompile to support big integer modular exponentiation enabling RSA signature verification and other cryptographic applications

Vitalik Buterin

Core

Final

Metropolis Byzantinium

[EIP-211](https://github.com/ethereum/EIPs/pull/211)

New opcodes: `RETURNDATASIZE` and `RETURNDATACOPY`. Support for returning variable-length values inside the EVM with simple gas charging and minimal change to calling opcodes using new opcodes `RETURNDATASIZE` and `RETURNDATACOPY`. Handles similar to existing `calldata`, whereby after a call, return data is kept inside a virtual buffer from which the caller can copy it (or parts thereof) into memory, and upon the next call, the buffer is overwritten.

Christian Reitwiessner

Core

Final

Metropolis Byzantinium

[EIP-214](https://github.com/ethereum/EIPs/pull/214)

New opcode: `STATICCALL`. Permits non-state-changing calls to itself or other contracts whilst disallowing any modifications to state during the call (and its sub-calls, if present) to increase smart contract security and assure developers that re-entrancy bugs cannot arise from the call. Calls the child with `STATIC` flag set `true` for execution of child, causing exception to be thrown upon any attempts to make state-changing operations inside an execution instance where `STATIC` is set `true`, and resets flag once call returns.

Vitalik Buterin, Christian Reitwiessner

Core

Final

Metropolis Byzantinium

[EIP-225](https://github.com/ethereum/EIPs/issues/225)

Rinkeby Testnet using Proof-of-Authority where blocks only mined by trusted signers

Homestead

[EIP-234](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-234.md)

Add `blockHash` to JSON-RPC filter options

Micah Zoltu

Interface

Draft

[EIP-615](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-615.md)

Subroutines and Static Jumps for the EVM

Greg Colvin

Core

Draft

[EIP-616](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-616.md)

SIMD Operations for the EVM

Greg Colvin

Core

Draft

[EIP-681](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-681.md)

ERC-681 URL Format for Transaction Requests

Daniel A. Nagy

Interface

Draft

[EIP-649](https://github.com/ethereum/EIPs/pull/669)

Metropolis Difficulty Bomb Delay and Block Reward Reduction - Delay of the Ice Age (aka the Difficulty Bomb by 1 year), and reduction of the block reward from 5 to 3 ether.

Afri Schoedon, Vitalik Buterin

Core

Final

Metropolis Byzantinium

[EIP-658](https://github.com/ethereum/EIPs/pull/658)

Embedding transaction status code in receipts. Fetch and embed status field indicative of success or failure state to transaction receipts for callers, as was no longer able to assume the transaction failed if and only if (iff) it consumed all gas after the introduction of the `REVERT` opcode in EIP-140.

Nick Johnson

Core

Final

Metropolis Byzantinium

[EIP-706](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-706.md)

DEVp2p snappy compression

Péter Szilágyi

Networking

Final

[EIP-721](https://github.com/ethereum/EIPs/issues/721)

ERC-721 Non-Fungible Token (NFT) Standard. It is a standard API that would allow smart contracts to operate as unique tradable non-fungible tokens (NFT) that may be tracked in standardised wallets and traded on exchanges as assets of value, similar to ERC-20. CryptoKitties was the first popularly-adopted implementation of a digital NFT in the Ethereum ecosystem.

William Entriken, Dieter Shirley, Jacob Evans, Nastassia Sachs

Standard

Draft

[EIP-758](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-758.md)

Subscriptions and filters for transaction return data

Jack Peterson

Interface

Draft

[EIP-801](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-801.md)

ERC-801 Canary Standard

ligi

Interface

Draft

[EIP-827](https://github.com/ethereum/EIPs/issues/827)

ERC-827 A extension of the standard interface ERC20 for tokens with methods that allows the execution of calls inside transfer and approvals. This standard provides basic functionality to transfer tokens, as well as allow tokens to be approved so they can be spent by another on-chain third party. Also it allows to execute calls on transfers and approvals.

Augusto Lemble

ERC

Draft

[EIP-930](https://github.com/ethereum/EIPs/issues/930)

ERC-930 The ES (Eternal Storage) contract is owned by an address that have write permissions. The storage is public, which means everyone has read permissions. It store the data on mappings, using one mapping per type of variable. The use of this contract allows the developer to migrate the storage easily to another contract if needed.

Augusto Lemble

ERC

Draft
