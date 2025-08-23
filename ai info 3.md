# Glossary

## Account

An account is a unique identifier and a requirement to interact with a Wire blockchain. Unlike most other cryptocurrencies, transfers are sent to a human-readable account name rather than a public key, while keys attributed to the account are used to sign transactions.

## Account Name

An account name is a human-readable identifier that is stored on the blockchain. Account names can only contain the characters .abcdefghijklmnopqrstuvwxyz12345. a-z (lowercase), 1-5 and . (period), must start with a letter or a number; cannot start or end with period. It can be 13 characters and one of them has to be a period.

The ability to choose a username is granted to T4 tier.

## Action

Functionality exposed by a smart contract that is exercised by passing the correct parameters via an approved transaction to Wire network.

## Application Binary Interface

A JSON-based description on how to convert user actions between their JSON and binary representations. The ABI may also describe how to convert the database state to/from JSON. Once you have described your contract via an ABI this allows developers and users to interact with your contract seamlessly via JSON.

Abbreviation: ABI

## Authority

On the Wire platform, the authority relates a public key and the authorization factors for an account and an account permission. The authority is a data structure linking account permissions to keys, thresholds, weights, delegated account permissions, and time waits.

Related:

- [Permission](https://docs.wire.network/docs/introduction/glossary"%20\l%20"permission)
- [Account](https://docs.wire.network/docs/introduction/glossary"%20\l%20"account)
- [Permission Level](https://docs.wire.network/docs/introduction/glossary"%20\l%20"permission-level)
- [Permission Weight](https://docs.wire.network/docs/introduction/glossary"%20\l%20"permission-weight)
- [Permission Threshold](https://docs.wire.network/docs/introduction/glossary"%20\l%20"permission-threshold)

## Bancor Relay

Wire adopts a free-market approach to allocating scarce resources such as RAM. The Wire system contract allows users to buy RAM from the system and sell RAM back to the system in exchange for the blockchain's native tokens. This provides liquidity in the RAM market while facilitating price discovery. The less unallocated RAM available to the market maker the higher the market maker prices the remaining RAM. The algorithm used for this market maker is known as a Bancor Relay. A Bancor Relay does not set the price of RAM. It only offers to buy and sell at previously established market rates. Anytime the current market rate is different than the current price offered by the Bancor Relay, traders will buy or sell RAM pushing to closer to the market determined price.

## Block

A confirmable unit of a blockchain. Each block contains zero or more transactions, as well as a cryptographic connection to all prior blocks. When a block becomes "irreversibly confirmed" it's because a supermajority of node operators have agreed that the given block contains the correct transactions. Once a block is irreversibly confirmed, it becomes a permanent part of the immutable blockchain.

## Block Header

A part of the block which holds metadata related to the block. In an Wire block header this includes things like the transaction Merkle root, the action Merkle root, the producer who produced the block, the block id of the previous block, the block id of the current block, and the block timestamp.

Related [Block Merkle Tree](https://docs.wire.network/docs/introduction/glossary"%20\l%20"merkle-tree)

## Block Log

The block log is an append-only log of blocks written to disk and contains all the irreversible blocks.

## Node Operator

A Node Operator Producer is an identifiable entity composed of one or more individuals that express interest in participating in running an Wire network. By participating it is meant these entities will provide a full node, gather transactions, verify their validity, add them into blocks, and propose and confirm these blocks. A Node Operator is generally required to have experience with system administration and security as it is expected that their full-node have constant availability.

## Node Operator Schedule

The list of block producers who currently have the possibility of being selected to produce the next block. This list changes with every new block.

Related [Node Operator](https://docs.wire.network/docs/introduction/glossary"%20\l%20"node-operator)

## Block-Producing Node

A full node running nodeop that is actively producing blocks. A producing node, if voted out, will become a producing node on "standby". Standby operators are synced with the nextwork but they will only start producing blocks and earn rewards if they are selected to be part of the 21 Node Operators.

## Blockchain Application

A blockchain application is a software application that has integrated a blockchain in its architecture as the storage layer for part of, or, all of its data. This includes software applications that do not own their own contract on the blockchain and instead only interact with the system contracts of the blockchain.

## Byzantine Fault Tolerance

In the context of distributed systems, Asyncronous Byzantine Fault Tolerance (aBFT) is the ability of a distributed computer network to function as desired and correctly reach a sufficient consensus despite malicious components (nodes) of the system failing or propagating incorrect information to other peers. In an Wire based blockchain aBFT is achieved using a combination of Appointed Proof of Stake, the last irreversible block, and the fact that a producer cannot sign two blocks with the same block number.

## CPU

CPU is processing power granted to an account by an Wire based blockchain. The amount of CPU an account has is measured in microseconds, and represents the amount of processing time an account has at its disposal when executing its actions.

## Chain State

The chain state (or "database" as it is often called) is a memory mapped file, which stores the blockchain state of each block (account details, deferred transactions, transactions, data stored using multi index tables in smart contracts, etc.). Once a block becomes irreversible the chain state is no longer cached.

## clio

clio is a command line tool that interfaces with the REST api exposed by nodeop, in other words clio is the command line tool through which you can interface with an Wire based blockchain; clio contains documentation for all of its commands. For a list of all commands known to clio, simply run it with no arguments. clio = command line + eos

## Confirmed Transaction

On completion of the transaction, a transaction receipt is generated. Receiving a transaction hash does not mean that the transaction has been confirmed, it only means that the node accepted it without error, which also means that there is a high probability other producers will accept it. A transaction is considered confirmed when a nodeop instance has received, processed, and written it to a block on the blockchain, i.e. it is in the head block or an earlier block.

## Core

The core is used to refer to the Wire blockchain native components, e.g. native actions, chain libraries, nodeop daemon, etc. The core is the Wire platform on which Wire based blockchains can be instantiated and tailored by means of deploying smart contracts (including the system smart contracts). Therefore, the system smart contracts are not considered part of the core or native blockchain implementation.

## Cryptographic Hash

A cryptographic hash function is a hash function which takes an input (or 'message') and returns a fixed-size alphanumeric string. The alphanumeric string is called the 'hash value', 'message digest', 'digital fingerprint', 'digest' or 'checksum'.

## Custom Permission

In addition to the native permissions, owner and active, an account can possess custom named permissions that are available to further extend account management. Custom permissions are incredibly flexible and address numerous possible use cases when implemented. Custom permissions are arbitrary and impotent until they have been linked to an action.

## Deferred Action

Deferred actions are actions sent to a peer action that are scheduled to run, at best, at a later time, at a block producer's discretion. There is no guarantee that a deferred action will be executed. From the perspective of the originating action, i.e., the action that creates the deferred action, it can only determine whether the create request was submitted successfully or whether it failed (if it fails, it will fail immediately). Deferred actions carry the authority of the contract that sends them. A deferred action can also be cancelled by another action.

## Appointed Proof of Stake(APoS)

Wire Network's consensus algorithm that builds upon a Delegated Proof of Stake, which was originally developed by Daniel Larimer. APoS addresses DPoS consensus challenges by separating roles and responsibilities of Node Owners from Node Operators,

## Deserialization

Deserialization is the reverse process of serialization. It turns a stream of bytes into an object in memory. Wire structures are enhanced with two operators which implement the serialization and deserialization of data to and from the database.

## Digital Signature

A digital signature is a mathematical scheme for verifying the authenticity of digital messages or documents. A valid digital signature, where the prerequisites are satisfied, gives a recipient very strong reason to believe that the message was created by a known sender (authentication), and that the message was not altered in transit (integrity). Digital signatures are a standard element of most cryptographic protocol suites, and are commonly used for software distribution, financial transactions, contract management software, and in other cases where it is important to detect forgery or tampering.

## Dispatcher

Every smart contract must provide an apply action handler. The apply action handler is a function that listens to all incoming actions and performs the desired behavior. In order to respond to a particular action, code is required to identify and respond to specific action requests. apply uses the receiver, code, and action input parameters as filters to map to the desired functions that implement particular actions.

## Dispatcher Hooks

In addition to actions and notification handlers, two "hooks" are available. The pre_dispatch hook will fire when the dispatcher is run and allow the smart contract to do some pre-validation and exit early if need be by returning false. If the function returns true then the dispatcher continues to dispatch the actions or notification handlers. The post_dispatch hook will only fire when the dispatcher has failed to match any notification handlers, this allows the user to do some meaningful last ditch validation.

## Distributed Ledger Technology

A consensus of replicated, shared, and synchronized digital data geographically spread across multiple sites, countries, or institutions. DLT is also called a shared ledger.

Abbreviation : DLT

## Wire Types

Wire source code defines a list of types which ease the developer's work when writing smart contracts, plugins, or when extending the Wire source code. Example types include account_name, permission_name, table_name, action_name, scope_name, weight_type, public_key, etc.

## Wire CDT

The toolchain to build WebAssembly (WASM) and set of tools to facilitate smart contract development for the Wire platform.

## Genesis Block

The genesis block is the very first block in the Wire blockchain. The subsequent block added after the genesis block becomes block 1 and continues the sequence. The genesis block lays the foundation for other blocks to be added to form a blockchain.

Related [Block](https://docs.wire.network/docs/introduction/glossary"%20\l%20"block)

## Genesis Node

The genesis node is the first node in the blockchain network. The genesis node is used to perform a set of actions such as creating system accounts, initializing system, and token contracts in order to create a fully-functional blockchain with varying capabilities such as governance, resource allocation, and more.

Synonyms Single Producer Node

## Governance

Blockchain governance is a lot like other kinds of governance, except that it's underpinned by smart contracts and transparent voting on the blockchain. Governance, the mechanism by which collective decisions are made, of a Wire based blockchain is achieved through 21 active Node Operators which are appointed by token holders. The 21 active Node Operators continuously create the blockchain via block creation, secure the blocks by validating them, and reach consensus on the state of the blockchain as a whole. Consensus is reached when 2/3+ active node operators agree on validity of a block , therefore on all transactions contained in it and their order.

Related [Irreversible Block](https://docs.wire.network/docs/introduction/glossary"%20\l%20"irreversible-block)

## Head Block

The head block is the last block written to the blockchain, stored in reversible_blocks.

## Indices

In the context of a multiple index table, an index is a particular ordering of the elements in the table. Multiple index indices allow the same data in one table to be viewed as different data structures by specifying the specific index on the table. Wire multiple index tables allow for up to 16 unique indices.

## Inline Action

Inline actions request other actions that need to be executed as part of the original calling action. Inline actions operate with the same scopes and authorities of the original transaction, and are guaranteed to execute with the current transaction. These can effectively be thought of as nested transactions within the calling transaction. If any part of the transaction fails, the inline actions will unwind with the rest of the transaction.

## Irreversible Block

Irreversible blocks are blocks that contain confirmed, final transactions. A block is considered irreversible (i.e., immutable) on an Wire-based blockchain when a supermajority, consisting of 2/3rds plus 1 of the currently elected node operators have confirmed the block.

Related: [Block](https://docs.wire.network/docs/introduction/glossary"%20\l%20"block)

## Kiod

kiod is the component that securely stores Wire keys in wallets. kiod = key + eos

## Merkle Tree

A Merkle tree is a tree in which every leaf node is labelled with the hash of a data block, and every non-leaf node is labelled with the cryptographic hash of the labels of its child nodes. Hash trees allow efficient and secure verification of the contents of large data structures.

Synonyms Hash tree Related: [Block Header](https://docs.wire.network/docs/introduction/glossary"%20\l%20"block-header)

## Multi-Index

Wire wraps the [boost multi-index C++](https://www.boost.org/doc/libs/1_75_0/libs/multi_index/doc/index.html) library to provide in memory data persistence. A subset of the functionality provided by the boost multi- index is provided in the Wire multi-index.

## Multi Index Table

Multi Index Tables, are a way to cache state and/or data in RAM for fast access. Multi index tables support create, read, update, and delete (CRUD) operations, something which the blockchain doesn't (it only supports create and read). Multi index tables are stored in Wire RAM and each smart contract using a multi index table reserves a partition of the RAM cache. Access to each partition is controlled using the table name, code, and scope, and can have up to 16 indexes or indices defined.

Synonyms Multiple Index Tables

Related [Indices](https://docs.wire.network/docs/introduction/glossary"%20\l%20"indices)

## Multisig

Multisig is a short term for multiple signatures. It’s used to describe the case in which one requires more than one account's permission to execute a transaction. Wire provides the system account sysio.msig, which can be used to push onto the blockchain the multisig proposals and their corresponding account's permission required to approve the proposal. Multisig, when used properly, increases the security of an account, the security of a smart contract, and it's also the method by which producers are able to affect changes within an Wire blockchain.

Synonyms msig multiple signatures

## NET

NET is required to store transactions on an Wire based blockchain. The amount of NET an account has is measured in bytes, representing the amount of transaction storage an account has at its disposal when creating a new transaction. NET is recalculated after each block is produced, based on the system tokens staked for NET bandwidth by the account. The amount allocated to an account is proportional with the total system tokens staked for NET by all accounts. Do not confuse NET with RAM, although it is also storage space, NET measures the size of the transactions and not contract state.

## Nodeop

nodeop is the core Wire node daemon that can be configured with plugins to run a node. Example uses are block production, dedicated API endpoints, and local development.

## Non-Producing Node

A full node running nodeop that is only watching and verifying for itself each block, and maintaining its own local full copy of the blockchain. A non-producing node that is in the "standby pool" can, through the process of being voted in, become a Producing Node. A producing node, if voted out, will become a non-producing node. For large Wire changes, non-producing nodes are outside the realm of the "standby pool".

Related [Block Producing Node](https://docs.wire.network/docs/introduction/glossary"%20\l%20"block-producing-node)

## Oracle

An oracle, in the context of blockchains and smart contracts, is an agent that finds and verifies real-world occurrences and submits this information to a blockchain to be used by smart contracts.

## Packed Transaction

In order to transfer transaction content between nodes faster and to save storage space when storing transaction content in and Wire based blockchain database, the transactions are 'translated' from json into a packed form which is smaller in size. To get the packed version of a transaction one can use the clio convert command.

## Peer-to-peer

Peer-to-peer computing or networking is a distributed application architecture that partitions tasks or workloads between peers. If peers are equally privileged, equipotent participants in an application, they are said to form a peer-to-peer network of nodes.

## Pending Block

The pending block is the block currently being built by each node. Transactions are added to the pending block as they are received and processed. The pending block becomes the head block once it is written to the blockchain. Note that a head block is initially reversible.

## Pending Blocks

The pending block is an in memory block containing transactions as they are processed into a block, this will/may eventually become the head block. If this instance of nodeop is the producing node then the pending block will eventually be distributed to other nodeop instances.

## Permission

A weighted security mechanism that determines whether or not a message is properly authorized by evaluating its signature(s) authority. Every account has two default permissions, owner and active, but can also have custom permissions to further secure communications from an account to contracts. Every permission name has a "parent." Parents possess the authority to change any of the permissions settings for any and all of their children.

## Permission Threshold

The sum of permission weights necessary for a signature to be considered valid.

## Permission Weight

A permission weight is a value given to an account for authorization purposes. This is typically used in the context of a mutli-sig to give one or more accounts more control over a multi-sig than others.

Synonyms Authorization

## Permission level

Permissions are arbitrary names used to define the requirements for a transaction sent on behalf of that permission. Permissions can be assigned for authority over specific contract actions by "linking authorization" or linkauth. Every account has two native named permissions, owner and active. Every permission name has a "parent." Parents possess the authority to change any of the permission settings for any and all of their children. In addition to the native permissions, an account can possess custom named permissions that are available to further extend account management. Custom permissions are incredibly flexible and address numerous possible use cases when implemented correctly. Given this context permission level is used to identify a specific permission, either active, or owner, or a custom one.

## Plugin

nodeop plugins are software components that implement features that complement the native Wire blockchain basic implementation. They can be enabled or disabled through the nodeop configuration file or specifying them in the command line that launches the nodeop daemon.

## Private Key

A private key is a secret key used to sign transactions. In Wire, a private key's authority is determined by it's mapping to an Wire account name.

## Private Network

A private network is a production network, or a test network, to which access is private, that is, the API endpoints, and node operators connectivity URLs and IPs are private. Access to a private network is done via invitation, or, upon request to join, is granted by the owners of the private network.

## Privileged

Privileged accounts are accounts which can execute transactions while skipping the standard authorization check. To ensure that this is not a security hole, the permission authority over these accounts is granted to the sysio.prods account. An account can be set as privileged by sending the action setpriv to an Wire based blockchain, specifying the account to be set as privileged, and providing the correct permission, or, by using clio command line utility.

## Privileged Account

At the genesis of an Wire based blockchain, there is only one account present, Wire which is the main system account.

Related [Account](https://docs.wire.network/docs/introduction/glossary"%20\l%20"account)

## Public Key

A publicly available key that can be authorized to permissions of an account and can be used to identify the origin transaction. A public key can be inferred from a signature.

## Public Network

A public network is a production network instantiated with the Wire platform. For a public network, the tokens have value on public markets, and all of the features required to run and maintain the network, such as consensus and governance, are enabled. To contrast a public network, in a private network typically tokens are not traded on public markets, and there is less emphasis placed on governance.

## RAM

RAM is required to store account information such as keys, balances, and contract state on an Wire based blockchain. Because the amount of RAM available to a single computer is limited by Moore’s Law and other technological advances, RAM is fundamentally scarce and must be purchased on a free-market inside an Wire based blockchain.

Related [Bancor Relay](https://docs.wire.network/docs/introduction/glossary"%20\l%20"bancor-relay)

## RAM Market

In order to persist data on an Wire based blockchain, a user must first purchase RAM. The Wire RAM market uses the Bancor Relay algorithm in a system smart contract to offer to buy and sell RAM from users at previously established market rates.

Related [Bancor Relay](https://docs.wire.network/docs/introduction/glossary"%20\l%20"bancor-relay)

## REX

The REX (Resource Exchange) is a CPU and Network resource rental market in which holders of the core token of a blockchain can buy and sell slices of the REX pool in the form of REX tokens. Blockchain users can then rent CPU and Network resources from the REX pool.

## ROA(Resource Owners Association)

A REX extension.

## Updog 🐕

The mechanism/process for exchanging data between chains. It is responsible for block production schedule and verification of Node Operators.

## Read Mode

An Wire based blockchain allows contract developers to persist state across actions, and consequently transaction, boundaries. For example the sample sysio.token contract keeps balances for all users in the database. Each instance of nodeop keeps the database in memory, so contracts can read and write data quickly. However, at any given time there can be multiple correct ways, called modes, to query that data.

## Retired Action

An action within a validated transaction, that is, an action whose transaction was executed and pushed to a block, but may or may not be final yet.

## Reversible Block

Any block on an Wire based blockchain with a block number greater than the last irreversible block. Reversible blocks are blocks that are not currently guaranteed to be on the blockchain.

Related [Irreversible Block](https://docs.wire.network/docs/introduction/glossary"%20\l%20"irreversible-block)

## Ricardian Contract

In the Wire based blockchain context Ricardian Contract is a digital document that accompanies a smart contract and defines the terms and conditions of an interaction between the smart contract and its users, written in human readable text, which is then cryptographically signed and verified. It is easily readable for both humans and programs, and aids in providing clarity to any situations that may arise in the interactions between smart contract and its users.

## SYS

SYS is the blockchain default token name for an Wire based blockchain. Any fork of the Wire open source has the option to rename it to any token name that meets the symbol validation rules.

## Scope

Scope is a region of data within a contract. Contracts can only write to regions in their own contracts but they can read from any other contract's regions. Proper scoping allows transactions to run in parallel for the same contract because they do not write to the same regions. Scope is not to be conflated with an account name, but contracts can use the same value for both for convenience.

## Serialization

Serialization is the process of turning an object in memory into a stream of bytes so you can store it on disk or send it over the network.

## Signature

A signature is a mathematical scheme for demonstrating the authenticity of digital messages or documents.

## Smart Contract

A smart contract is a computer protocol intended to facilitate, verify, or enforce the negotiation or performance of a contract.

## Staking

Staking is the act of locking tokens for resources on an Wire network. This includes but is not limited to, CPU time, RAM, and on-chain governance.

## Standard Account Name

Standard account names can only contain the characters .abcdefghijklmnopqrstuvwxyz12345. a-z (lowercase), 1-5 and. (period), must start with a letter and must be 12 characters in length.

## Standby Pool

A set of about 100 full nodes that have expressed the desire to be selected as Node Operators, and are capable of doing so on demand. Whenever the chain needs to replace an existing Node Operator with a new one, the new one is drawn from the standby pool.

## System

Everything that is part of Wire which is not part of core, is referred to as system, e.g. system accounts, privileged accounts, system contracts. From an architectural point of view system components sit on top of the core/native components.

## System Contract

The design of the Wire blockchain calls for a number of smart contracts that are run at a privileged permission level in order to support functions such as node operator registration, multi-sig, etc. These smart contracts are referred to as the system contracts and are the following, sysio.bios, sysio.system, sysio.token, sysio.msig and sysio.wrap contracts.

## Tables

Tables on an Wire-based blockchain are achieved via Multiple Index Table.

Related [Multiple Index Table](https://docs.wire.network/docs/introduction/glossary"%20\l%20"multi-index-table)

## Test Network

A test network or testnet is an instantiation of the Wire platform that is intended for testing purposes. Generally, the native token has no value and is given away to developers so they can test. Some features of a testnet may be disabled such as consensus and governance.

## Transaction

A complete all-or-nothing change to the Blockchain. A combination of one or more actions. Usually the execution result of a Smart Contract.

## Transaction Receipt

On completion of a transaction, a transaction receipt is generated. This receipt takes the form of a hash. Receiving a transaction hash does not mean that the transaction has been confirmed, it simply means that the node accepted it without error, which also means that there is a high probability other producers will accept it.

## Transaction Trace

Transaction trace is a log of all the actions that took place as a result of an initial action (inline actions, deferred actions, context free actions, etc), including the initial action, for all actions that are processed on the blockchain. A transaction trace for one transaction includes among other things, the transaction id, the block id that the transaction is part of, the time when the block was produced, the producer id, the time elapsed to process the transaction, and a list of all actions contained in the transactions.

## Unconfirmed Transaction

A transaction is considered unconfirmed as long as no nodeop instance has received, processed, and written it to a block on the blockchain, i.e. it is not in the head block or a block earlier than the head block.

## Wait

Wait is measured in seconds and it is the time to wait until a delayed transaction is executed. Its value can not be higher than the max_transaction_delay which is set in the global configuration file.

## Wallet

Wallets are clients that store keys that may or may not be associated with the permissions of one or more accounts. Ideally a wallet has a locked (encrypted) and unlocked (decrypted) state that is protected by a high entropy password.

## Wallet Import Format

An encoding for a private EDSA key. Wire uses the same version, checksum, and encoding scheme as the Bitcoin WIF addresses and should be compatible with existing libraries.

Example of a WIF Private Key: 5HpHagT65TZzG1PH3CSu63k8DbpvD8s5ip4nEB3kEsreAbuatmU

Abbreviation : WIF

## WebAssembly

The Wire based blockchains execute user-generated applications and code using WebAssembly. WASM is an emerging web standard with widespread support of Google, Microsoft, Apple, and others. At the moment the most mature toolchain for building applications that compile to WASM is clang/llvm with their C/C++ compiler. For best compatibility, it is recommended that you use the Wire toolchain to generate WASM.

Synonyms Web-Assembly Machine Abbreviation : Wasm