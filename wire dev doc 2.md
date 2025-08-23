# Overview

## Understanding Blockchain: Challenges and Limitations

Blockchain is a decentralized ledger technology that enables secure, transparent, and immutable recording of transactions across a distributed network of computers. By eliminating the need for a central authority, blockchain has revolutionized digital currencies and decentralized applications, as seen with pioneering networks like Bitcoin and Ethereum. However, despite their groundbreaking impact, these early blockchain systems face significant challenges that hinder the industry's advancement.

A primary issue is the blockchain trilemma, which posits that a blockchain can optimize only two out of three key properties: decentralization, security, and scalability. Bitcoin and Ethereum prioritize decentralization and security but struggle with scalability, leading to slow transaction speeds and high fees. This scalability constraint becomes a bottleneck as the demand for blockchain applications grows, necessitating the development of more efficient, faster, and cost-effective protocols.

Beyond the trilemma, other critical hurdles impede the blockchain industry's progress. Onboarding is a significant challenge, as the complexity of blockchain technologies can deter users and developers from adopting and interacting with them. Enhancing accessibility and ease of use is essential for widespread adoption. Interoperability is another major concern—the ability for diverse blockchain networks to communicate and collaborate seamlessly is vital for a cohesive ecosystem. Without it, the fragmentation of blockchain networks can stifle innovation and limit the potential benefits of decentralization.

## About Wire Network

Wire Network aims to address all of the major problems holding back the blockchain industry as the world's first Universal Transaction Layer (UTL). The UTL is an innovative infrastructure that seamlessly integrates a high-performance layer-1 blockchain (i.e., the settlement layer), Wire Name Service, and the Universal Polymorphic Address Protocol (UPAP). This combination effectively forms the UTL and enables smart contracts to interact with assets across multiple connected blockchains, effectively connecting isolated ecosystems and fostering a more efficient decentralized environment.

By keeping assets securely locked within their native chains and transacting ownership rights within Wire Network's settlement layer, the UTL eliminates the need for traditional bridges or oracle-based interoperability systems. This approach maintains the security and consensus integrity of the original blockchains while providing rapid transaction speeds and low or zero transaction costs within the network. Users can interact with Wire Network using their existing wallets through the technology enabled by UPAP, simplifying the onboarding process and enhancing user experience.

Moreover, Wire Network's novel Appointed Proof-of-Stake consensus mechanism enhances decentralization and security by distinctly separating governance, staking, and block production roles. Wire’s hierarchical node structure ensures optimal network performance while minimizing the risk of centralization. By addressing critical issues such as scalability, security, onboarding, and interoperability, Wire Network is poised to facilitate enterprise adoption of blockchain technology and consumer mass adoption, as well as support the future growth of decentralized applications and the emerging Ai-driven economy.

# Interoperability & WNS

## Introduction

Blockchain interoperability refers to the ability of different blockchain networks to communicate and exchange data while maintaining decentralization. With the proliferation of diverse blockchain projects over the past decade—each employing unique protocols and architectures—the challenge of seamless cross-chain interoperability has become increasingly complex. The lack of standardization in this domain has made the vision of a universal solution elusive. Various organizations have attempted to address interoperability through methods such as traditional bridges, side-chains, parachains, messaging protocols, and other innovations.

While these solutions offer different approaches, they often share common drawbacks. Many introduce potential security vulnerabilities and may compromise decentralization by relying on third-party entities for cross-chain transactions. Bridges and oracles, for example, have been prime targets for malicious activities due to architectural flaws that create centralized points of failure. Dependence on centralized components not only poses security risks but also diverges from the decentralized ideals that underpin blockchain technology. Such models can also diminish transparency within transaction systems.

Moreover, the heterogeneous nature of blockchain technology presents ongoing compatibility issues with both new and existing networks. Many interoperability solutions are inherently limited by the number of chains they can support, restricting their effectiveness in a rapidly evolving ecosystem.

At its core, Wire Network is designed to overcome these challenges. Wire Name Service (WNS), when combined with the Wire layer-1 settlement layer and the Universal Polymorphic Address Protocol, collectively forms to create a Universal Transaction Layer (UTL).

This article explores the architecture and processes of Wire Network and WNS, detailing how it addresses the inherent challenges of blockchain interoperability and sets a new standard for seamless cross-chain transactions.

## Design

The UTL's design is a hub-and-spoke model (see diagram below). This design enables transactions between different blockchain networks through a universal hub, providing a seamless, secure and cost-efficient way for environment for assets to interact & move between chains.

## Settlement Layer

Wire's layer-1 blockchain operates as the settlement layer for Wire Network. It is the backbone of the system, responsible for tracking the flow of assets into, within, and out of the network.

The settlement layer leverages high-performance blockchain technology to ensure rapid transaction speeds and substantial throughput, essential for supporting enterprise-grade applications and high-frequency trading. It utilizes the settle.wns smart contracts to maintain a comprehensive ledger of all assets deposited into the UTL and their ownership details. These contracts update ownership records with each transaction, ensuring transparency, security, and immutability of the transaction history.

WNS is comprised of native settlement and target chain ('escrow' or 'bucket') contracts, each with distinct functions at the different stages of an asset’s lifecycle.

## Security Principles

The security framework of WNS is robust, relying on multiple checks and balances to prevent malicious activities. Key features are the use of standard cryptographic proofs to verify transactions, implementation of UTXO model to track transaction outputs; as well utilizing a completely independent sub-chain to aid with the transaction verification process. This sub-chain, also knowns as S-chain (stands for settlement) includes only the relevant transactions and data needed for the target chain, allowing for fast and efficient processing.

### UTXO

The UTXO (Unspent Transaction Output) model views each token amount as a distinct, single-use account that is fully spent in every transaction. Every time a transaction occurs, the involved UTXOs are completely used and split into new UTXOs. In Wire Network, for example, instead of maintaining a single large balance, users have multiple UTXOs representing different amounts. This model supports efficient backtracking to specific deposits and is useful in scenarios where transactions need to be challenged or verified.

Example:

Bob wants to send 15 USDC to Alice. To complete the transaction, Bob’s wallet selects UTXOs that equal or exceed the required amount. UTXO #1 (12 USDC) and UTXO #2 (5 USDC) are selected, which together are total of 17 USDC.

The transaction consumes these UTXOs fully, creating two new outputs:

1. A new UTXO of 15 USDC for Alice, reflecting the amount Bob sent.
2. A new UTXO of 2 USDC for Bob, which is the leftover or “change” from the original UTXOs.

After the transaction, Bob now holds a new UTXO of 2 USDC, and Alice has a new UTXO of 15 USDC.

# Basic Components

Wire Network blockchain platform comes with various components and tooling. See the table below for a brief explanation of each component.

| Name | Function |
| --- | --- |
| nodeop | nodeop is the core service daemon that runs on every Wire node, responsible for processing smart contracts, validating transactions, producing blocks containing valid transactions, and confirming blocks to record them on the blockchain. It can be configured with various plugins to suit specific needs, including block production, dedicated API endpoints, and local development environments. As the main component of Wire, nodeop ensures efficient and secure operation of the blockchain network by leveraging its capabilities for transaction validation, smart contract processing, and block confirmation. |
| kiod | kiod is the key manager service daemon that securely stores private keys and signs digital messages. It ensures that keys are encrypted at rest in the associated wallet file and provides a secure enclave for signing transactions created by clio or third-party libraries. |
| clio | clio is a CLI that interfaces with the REST API exposed by nodeop. It also allows developers to deploy and test Wire smart contracts. |
| CDT | The Contract Development Toolkit is a C/C++ toolchain targeting WebAssembly (WASM) and a set of tools to facilitate development and deployment of smart contracts written in C/C++. In addition to being a general-purpose WebAssembly toolchain, Wire-specific optimizations are available to support building Wire smart contracts. This new toolchain is built around Clang 7, which means that CDT has most of the current optimizations and analyses from LLVM. |

The basic relationship between these components is illustrated in the following diagram:

Smart Contract Code

CDT

clio

nodeop

kiod

Wire Blockchain

## Reference

- [nodeop](https://docs.wire.network/docs/api-reference/tooling/nodeop)
- [clio](https://docs.wire.network/docs/api-reference/tooling/clio)
- [kiod](https://docs.wire.network/docs/api-reference/tooling/kiod)

NOTE

kiod can be accessed using the Wallet API, but it is important to note that the intended usage is for local light client applications. kiod is not for cross network access by web applications trying to access users' wallets.

- [CDT Contract Development Kit](https://docs.wire.network/docs/api-reference/tooling/cdt)

NOTE

Wire also provides a collection of JavaScript libraries published under [@wireio npm org](https://www.npmjs.com/org/wireio).

# Install Dependencies

## Linux Distributions

### Ubuntu

Currently supported versions:

- Ubuntu 22.04 Jammy
- Ubuntu 20.04 Focal

#### Installation via wire-cli

The quickest way to install Wire Sysio and Wire CDT softare is by using the [wire-cli](https://github.com/Wire-Network/wire-install?tab=readme-ov-file"%20\l%20"genesis-node-setup). Refer to the installation instructions outlined in the README.md.

#### Binary Installation

If you’d prefer to install the binaries yourself, follow along with the instructions provided below.

##### Install Wire Sysio

You can download Wire Sysio software from the [Official releases page](https://github.com/Wire-Network/wire-sysio/releases) or check the [Release tags page](https://github.com/Wire-Network/wire-sysio/tags) to download a specific version of Wire Sysio.

Once you have a \*.deb file, you can install it by running:

sudo apt install ./wire-sysio-\*.deb

##### Verify installation

nodeop --full-version

You should see a semantic version string followed by a commit hash with no errors. For example:

v3.1.6-8f6875608efc9aceab9218360822bba3bc664cfb

info

Wire Sysio executables are located at /usr/local/bin.

##### Install Wire CDT

You can download Wire Sysio software from the [Official releases page](https://github.com/Wire-Network/wire-cdt/releases) or check the [Release tags page](https://github.com/Wire-Network/wire-cdt/tags) to download a specific version of Wire CDT.

Once you have a \*.deb file, you can install it by running:

sudo apt install ./wire-cdt-\*.deb

##### Verify installation

which cdt-cpp

Expected Output -> /usr/bin/cdt-cpp

or

cdt-cpp _\--version_

Expected Output -> cdt-cpp version 3.1.0

info

Wire CDT is located at /usr/opt with symlinks to each of its executable in /usr/bin. You can list the contents using ls -la usr/opt/cdt/&lt;version&gt;/bin.

&nbsp;

#### Removing Wire Sysio and Wire CDT

##### Uninstall Wire Sysio

To uninstall it, run:

sudo apt remove wire-sysio

If uninstalling has failed or if didn't remove all core components, you can manually delete them with the following command:

sudo rm _\-rf_ /usr/local/bin/clio \\

/usr/local/bin/kiod \\

/usr/local/bin/nodeop \\

/usr/local/bin/sysio-blocklog \\

/usr/local/bin/trace_api_util \\

.local/share/sysio \\

~/sysio-wallet

danger

The uninstall command above will also remove the default wallet installed with Wire Sysio. To keep any imported keys, make sure to back them up before proceeding with deletion.

##### Uninstall Wire CDT

To uninstall Wire CDT, run:

sudo apt remove cdt

&nbsp;

### Troubleshooting

If you are missing certain dependencies and when trying to install the binaries you are getting an error similar to:

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

Note, selecting 'wire-sysio' instead of './wire-sysio-3.1.6_amd64.deb'

Some packages could not be installed. This may mean that you have

requested an impossible situation or _if_ you are using the unstable

distribution that some required packages have not yet been created

or been moved out of Incoming.

The following information may help to resolve the situation:

The following packages have unmet dependencies:

sysio : Depends: libssl1.1 but it is not installable

Depends: libicu60 but it is not installable

E: Unable to correct problems, you have held broken packages.

- Try and resolve it by looking for exact dependencies at Index of /ubuntu/pool/main/o/openssl
- Find the exact version of libssl , in this case libssl1.1
- Download it:

wget <http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1-1ubuntu2.1\\~18.04.amd64.deb>

- Install the downloaded package:

sudo dpkg _\-i_ libssl1.1_1.1.1-1ubuntu2.1~18.04.amd64.deb

Repeat the same for any other packages that appear in the error message.

wget <http://mirrors.edge.kernel.org/ubuntu/pool/main/i/icu/libicu60_60.2-3ubuntu3.1_amd64.deb>

sudo dpkg _\-i_ libicu60_60.2-3ubuntu3.2_amd64.deb

After successfully installing all missing packages, attempt to install the binaries again.

# Launching Local Node

This section explains launching a local node by starting up the nodeop and kiod services.

## Prerequisites

- You have successfully installed Wire Sysio and Wire CDT on your computer without using the wire-cli automation script. The steps below are only relevant if you followed the [Binary Installation](https://docs.wire.network/docs/getting-started/install-dependencies"%20\l%20"binary-installation) instructions.

## Starting kiod

Typically a user would just create a wallet first and in doing so it would start up [kiod](https://docs.wire.network/docs/introduction/glossary"%20\l%20"kiod).

You can use kiod command to start and restart the process.

kiod

info 2024-05-29T13:48:18.634 kiod wallet_plugin.cpp:38 plugin_initialize \] initializing wallet plugin

info 2024-05-29T13:48:18.635 kiod wallet_api_plugin.cpp:69 plugin_startup \] starting wallet_api_plugin

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/create

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/create_key

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/get_public_keys

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/import_key

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/list_keys

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/list_wallets

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/lock

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/lock_all

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/open

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/remove_key

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/set_timeout

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/sign_digest

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/sign_transaction

info 2024-05-29T13:48:18.635 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/wallet/unlock

info 2024-05-29T13:48:18.636 kiod http_plugin.cpp:927 add_handler \] add api url: /v1/node/get_supported_apis

Verify that kiod is running by:

pidof kiod

### Troubleshooting

If you encounter a message similar to the one below:

info 2024-09-25T13:51:58.918 kiod wallet_plugin.cpp:38 plugin_initialize \] initializing wallet plugin

warn 2024-09-25T13:51:58.918 kiod wallet_plugin.cpp:65 plugin_initialize \] 3120000 wallet_exception: Wallet exception

Failed to lock access to wallet directory; is another kiod running?

{}

kiod wallet_manager.cpp:304 initialize_lock

Failed to initialize

This is because another instance of kiod process might be running in the background.

Kill all instances: pkill kiod and the restart it.

## Starting nodeop

To start nodeop, run:

nodeop _\-e_ _\-p_ sysio \\

_\--plugin_ sysio::producer_plugin \\

_\--plugin_ sysio::producer_api_plugin \\

_\--plugin_ sysio::chain_api_plugin \\

_\--plugin_ sysio::http_plugin \\

_\--plugin_ sysio::state_history_plugin \\

\--access-control-allow-origin='\*' \\

\--contracts-console \\

\--http-validate-host=false --disable-replay-opts \\

\--verbose-http-errors >> ~/nodeop.log 2>&1 &

Command breakdown:

- starts nodeop with essential plugins;
- configures the server address;
- enables CORS without restrictions (\*) and includes development logging; logs will be saved to ~/nodeop.log;

For more information on nodeop flags, see nodeop --help or the output of this command [here](https://docs.wire.network/docs/api-reference/tooling/nodeop/nodeop-cli).

NOTE

CORS is enabled for all (\*) for development only. Never enable unrestricted CORS on publicly accessible nodes!

### Troubleshooting

#### Database dirty flag error

If you see error that looks like the examples below:

info timestamp nodeop chain_plugin.cpp:461 operator() \] Support _for_ builtin protocol feature 'GET_SENDER' (with digest of 'f0af56d2c5a48d60a4a5b5c903edfb7db3a736a94ed589d0b797df33ff9d3e1d') is enabled with preactivation required

info timestamp nodeop chain_plugin.cpp:955 plugin_initialize \] Starting fresh blockchain state using genesis state extracted from blocks.log.

warn timestamp nodeop chain_plugin.cpp:1237 plugin_initialize \] 13 N5boost10wrapexceptISt12system_errorEE: Database dirty flag set

rethrow Database dirty flag set:

{"what":"Database dirty flag set"}

nodeop chain_plugin.cpp:1237 plugin_initialize

error timestamp nodeop main.cpp:153 main \] database dirty flag set (likely due to unclean shutdown): replay required

Database dirty flag set (likely due to unclean shutdown): replay required

Try and include --replay-blockchain or --hard-replay-blockchain flag to the nodeop startup command.

nodeop _\-e_ _\-p_ sysio \\

_\--plugin_ sysio::producer_plugin \\

_\--plugin_ sysio::producer_api_plugin \\

_\--plugin_ sysio::chain_api_plugin \\

_\--plugin_ sysio::http_plugin \\

_\--plugin_ sysio::state_history_plugin \\

\--access-control-allow-origin='\*' \\

\--contracts-console \\

\--http-validate-host=false --replay-blockchain --disable-replay-opts \\

\--verbose-http-errors >> ~/nodeop.log 2>&1 &

If you want to a clean fresh state of the chain, you may want to use --delete-all-blocks.

More details on troubleshooting nodeop can be found [here](https://docs.wire.network/docs/api-reference/tooling/nodeop/troubleshooting).

You could also change nodeop.log file's location to whatever directory you want.

If there isn't a process running, use the [startup command](https://docs.wire.network/docs/getting-started/launch-local-node"%20\l%20"starting-nodeop).

### Validating nodeop

Check that nodeop is producing blocks. Run the following command:

tail _\-f_ ~/nodeop.log

You should see some output in the console similar to:

info \[timestamp\] nodeop producer_plugin.cpp:2293 produce_block \] Produced block b50adde5943bdde1... #44 at \[timestamp\] signed by sysio \[trxs: 0, lib: 43, confirmed: 0\]

info \[timestamp\] nodeop producer_plugin.cpp:2293 produce_block \] Produced block 39b2a4fef9db084f... #45 at \[timestamp\] signed by sysio \[trxs: 0, lib: 44, confirmed: 0\]

info \[timestamp\] nodeop producer_plugin.cpp:2293 produce_block \] Produced block cd23d3646d0166dc... #46 at \[timestamp\] signed by sysio \[trxs: 0, lib: 45, confirmed: 0\]

info \[timestamp\] nodeop producer_plugin.cpp:2293 produce_block \] Produced block 14bd99c3c3ffd441... #47 at \[timestamp\] signed by sysio \[trxs: 0, lib: 46, confirmed: 0\]

info \[timestamp\] nodeop producer_plugin.cpp:2293 produce_block \] Produced block 2e5fb9d0f2dce119... #48 at \[timestamp\] signed by sysio \[trxs: 0, lib: 47, confirmed: 0\]

Verify the \[timestamp\] is a recent one and that you aren't looking at a stale logs.

To exit logs: Ctrl + C

### Check the Wallet

Open the shell and run the clio wallet list command to list available wallets. We need to validate the installation and see that the command line client clio is working as intended.

You should see a response with an empty list of wallets:

Wallets:

\[\]

From this point forward, you'll be executing commands from your local system.

### Check nodeop endpoints

This step ensures that the RPC API is functioning properly. You can choose one of the following methods:

#### 3.1. Using clio

clio get info

#### 3.2. HTTP GET request to /get_info

Use your browser to access the get_info endpoint from the chain_api_plugin. Simply click <http://localhost:8888/v1/chain/get_info>.

{

"server_version": "1dd2fd86",

"chain_id": "8a34ec7df1b8cd06ff4a8abbaa7cc50300823350cadc59ab296cb00d104d2b8f",

"head_block_num": 1769,

"last_irreversible_block_num": 1768,

"last_irreversible_block_id": "000006e810b62ae346aa0066d7e3d5fe152285692c4d15dc742e1733b61eb27b",

"head_block_id": "000006e931c346d88fc5cb63ce025bfd5f0843656761ac074b35c1c941684f64",

"head_block_time": "2024-09-25T15:43:18.000",

"head_block_producer": "sysio",

"virtual_block_cpu_limit": 1170419,

"virtual_block_net_limit": 6146775,

"block_cpu_limit": 200000,

"block_net_limit": 1048576,

"server_version_string": "v3.1.6",

"fork_db_head_block_num": 1769,

"fork_db_head_block_id": "000006e931c346d88fc5cb63ce025bfd5f0843656761ac074b35c1c941684f64",

"server_full_version_string": "v3.1.6-1dd2fd862c04c1b49df6b2314eb1a621d0301c9f",

"total_cpu_weight": 0,

"total_net_weight": 0,

"earliest_available_block_num": 1,

"last_irreversible_block_time": "&lt;timestamp&gt;"

}

Alternatively, check the endpoint directly from your terminal using the command:

curl <http://localhost:8888/v1/chain/get_info> | jq .

Third-party tools used in the steps above:

- [JSON Formatter Chrome Extension](https://chromewebstore.google.com/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa?hl=en)
- [curl](https://curl.se/)
- [jq](https://jqlang.github.io/jq/download/)

# System Requirements

## Info

The subsequent tutorials are up to date with the following Wire components.

| Component | Version |
| --- | --- |
| Wire Sysio Core Version | 3.1.6 |
| Wire CDT | 3.1.0 |
| sysio.contracts | 3.1.1 |
| skd-core | 1.0.0 |

### Supported Operating Systems

The Wire platform is supported on the following environments:

Linux Distributions:

- Ubuntu v22 & v20

## Development Experience

Wire based blockchains execute user-generated applications and code using WebAssembly (WASM). WASM is an emerging web standard with widespread support from Google, Microsoft, Apple, and industry leading companies.

At the moment the most mature toolchain for building applications that compile to WASM is clang/llvm with their C/C++ compiler.

### Command Line Knowledge

There are a variety of tools provided along with Wire core and CDT packages which requires you to have a basic command line knowledge in order to interact with them.

### Development Tools

We recommend using an Integrated Development Environment (IDE) rather than a text editor, as IDEs offer a more sophisticated code completion and a more comprehensive development experience. While you can use any text editor that supports C++ syntax highlighting, such as Sublime Text or Atom, IDEs provide additional features that can enhance your coding efficiency. You are welcome to use the software of your personal preference, but if you're unsure what to use, we've provided some options for you to explore.

### IDEs

- [Visual Studio Code](https://code.visualstudio.com/)
- [CLion](https://www.jetbrains.com/clion/)
- [Eclipse](https://eclipseide.org/)

NOTE

The resources mentioned above are developed, offered, and maintained by third parties, not by Wire Network. Sharing information, materials, or commentaries about these third-party resources does not constitute an endorsement or recommendation by us. We disclaim any responsibility or liability for your use of or reliance on these resources. Third-party resources may be updated, changed, or terminated at any time, which could render the information below outdated or inaccurate. Your use and reliance on these resources are entirely at your own risk.

## What you will learn

- Manage wallets and keys
- Create accounts
- Write your first contract
- Compilation and ABI
- Contracts deployment
- Utilizing a block explorer

# Create Development Wallet

## Overview

Wallets store public-private key pairs, which are needed for signing operations performed on the blockchain. They can be accessed through the use of clio command line tool. This section explains how to create, manage, and unlock wallets using the clio CLI, including generating and importing keys into wallets. For more information on clio commands and usage, refer to [clio's CLI Reference](https://docs.wire.network/docs/api-reference/tooling/clio/command-reference).

## Create a Wallet

To create a wallet using clio, you can either print the password to the console or save it in a specific file. For simplicity and recommended only for development, use the --to-console option:

clio wallet create --to-console

For production environments, it is safer to use the --file option to avoid having your wallet password recorded in your bash history.

clio wallet create _\--file_ my-secret-pass.txt

In both cases, ensure you save the password securely, as it will be needed later in the tutorial.

Note the location of my-secret-pass.txt. You will need it later.

## Open the Wallet

Wallets are closed by default when starting a kiod instance, to begin, run the following

clio wallet open

Run the following to return a list of wallets.

clio wallet list

and it will return

Wallets:

\[

"default"

\]

## Unlock a Wallet

The kiod wallet(s) have been opened, but is still locked.

clio wallet unlock

You will be prompted for your wallet password you saved earlier, paste it and press enter. You could also use a one-liner below:

clio wallet unlock --password $(cat /path/to/password_file)

Execute the command below:

clio wallet list

This should output the following result:

Wallets:

\[

"default \*"

\]

The asterisk (\*) next to the name means that the wallet is currently unlocked.

## Import keys into your wallet​

To generating a key pair directly within the wallet, you could use clio wallet create_key command.

clio wallet create_key

Output:

Created new private key with a public key of: "SYS8PEJ5FM42xLpHK...X6PymQu97KrGDJQY5Y"

IMPORTANT

Save the public key somewhere safe as you would need it in the upcoming tutorials.

You could set it as environment variable:

export PUBLIC_KEY=public-key-value

## Import the Development Key​

Every new Wire chain has a default system user called sysio. This account is used to setup the chain by deploying system contracts that handle essential functions related to resource management, governance and consensus of the chain. Every new Wire chain also comes with a development key, and this key is the same and it is used to sign transactions on behalf of the sysio user.

clio wallet import

You'll be prompted for a private key, enter the sysio development key provided below:

5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

WARNING

Never use the development key for a production account! Doing so will most certainly result in the loss of access to your account.

# Create Development Accounts

## Overview

This article gives a brief summary of the concept of account and provides instructions on how to create a new account.

## Account

An account on the blockchain holds a set of authorizations and serves to identify a sender or recipient. Its flexible authorization framework allows ownership by individuals or groups ,depending on the configured permissions. An account is required to send or receive a valid transaction on the blockchain.

In this practical tutorial series, we utilize two user accounts, bob and alice, along with the default sysio account for configuration purposes. Additional accounts are also created for various contracts in the future articles.

## Creating an account

### Prerequisites

- public key from the key pair you've created in [Create Development Wallet](https://docs.wire.network/docs/getting-started/create-development-wallet"%20\l%20"import-keys-into-your-wallet) tutorial.
- Ensure your wallet is [unlocked](https://docs.wire.network/docs/getting-started/create-development-wallet"%20\l%20"unlock-a-wallet)

### Steps

#### Step 1: Use clio to create test accounts

clio create account sysio bob _$PUBLIC_KEY_

clio create account sysio alice _$PUBLIC_KEY_

Here is the output of the first command, confirming that the transaction has been broadcast:

If you encounter errors ensure you are correctly loading environment variables and that your wallet is unlocked.

- inspect value of $PUBLIC_KEY by echo $PUBLIC_KEY

#### Step 2

You can retrieve the account by executing:

clio get account alice

## Quick Account Facts

For a clear understanding of how Wire accounts and their associated public keys function, please refer to the table below:

| Label | Details |
| --- | --- |
| Account Identification | Each account is uniquely identified by its account name, not by its public key. |
|     | Changing the public key does not alter the ownership of the sysio account. |
| Owner and Active Public Keys | The account (e.g., alice) has both an owner and an active public key. |
|     | sysio’s authorization structure uses separate keys for owner and active permissions for enhanced security. |
| Security Practices | Store the owner key in a cold wallet to minimize exposure. |
|     | If the active key is compromised, the owner key can be used to regain control of the account. |
| Authorization Hierarchy | With owner permission, you can change the private key of the active permission. |
|     | The active permission cannot change the owner key. |

## Troubleshooting

### \[clio: Failed to connect to nodeop at \](<http://127.0.0.1:8888/>); is nodeop running?

Doublecheck if nodeop is running; and [restart](https://docs.wire.network/docs/getting-started/launch-local-node"%20\l%20"starting-nodeop) the process if needed.

pidof nodeop

# Overview

The following tutorials are built with the purpose of familiarizing you with smart contract terminology and basic C++ contract development.

# Accounts & Permissions

A Wire account is a digital entity on the blockchain that identifies a participant, which can be an individual or a group. An account also represents the smart contract actors that send and receive actions to and from other accounts on the blockchain. Actions, which are the fundamental units of execution, are always encapsulated within transactions, allowing for one or more atomic actions to be grouped together.

## Public & Private Keys

Every Wire account is ultimately controlled by a key pair (public and corresponding private key). While the public key is used to identify the account on the blockchain and can be publicly known, the private key which is used to sign each transaction must be kept secret at all times.

If you lose your private key, you will lose access to your account and all of its assets, smart contracts, and any other data associated with it.

## Permissions

Each account has a set of hierarchical permissions that control what that account can do and how actions are authorized. By default, each account comes with two base permissions - owner and active. These two permissions are mandatory and they cannot be removed. A permission can only modify its own controls (keys or accounts) or those of its children, but never those of its parent.

### Owner Permission

The owner permission is the highest in an account’s hierarchy, usually reserved for recovery scenarios when lower permissions are compromised. It can perform any action that lower permissions can, but keys for this permission are generally stored offline in cold storage to avoid misuse.

### Active Permission

The active permission is the default for all actions, sitting just below the owner permission. It handles typical account activities, but cannot alter owner keys. Custom permissions usually are created under the active and linked to specific contracts or actions.

A permission is linked to and controlled by either a public key or another account. This allows for the creation of complex account control structures, where multiple parties may control a single account while still having full autonomy over their own account's security.

See the diagram below as an example, where the account jack@active is controlled by both nick@active and daniel@active, and on the other hand, daniel@active is also controlled by katey@active.

### Permission Mapping

It is possible to create custom permissions scoped to specific actions within a designated contract, also known as permission mapping. That permission will then only ever be able to interact with the contract action you specified. Such setup allows for very granular access permissions across accounts and hierarchical structures tailored to your needs.

### Permission Evaluation

When determining whether an action is authorized to be executed, the wire-sysio software:

- first checks whether the signatures provided in the transaction are valid.
- then it proceeds to check the authorization of all the actions included in the transaction. This is where permissions are evaluated. If any action fails to be authorized, the transaction fails.

#### Authority Table

Each account's permission can be linked to an authority table used to determine whether a given action authorization can be satisfied. The authority table contains the target permission name and threshold, the factors and their weights, all of which are used in the evaluation to determine whether the authorization can be satisfied. The permission threshold is the target numerical value that must be reached to satisfy the action authorization (see authority schema below).

#### authority schema

| Name | Type | Description |
| --- | --- | --- |
| threshold | uint32_t | threshold value to satisfy authorization |
| keys | array of key_weight | list of public keys and weights |
| accounts | array of permission_level_weight | list of account@permission levels and weights |
| waits | array of wait_weight | list of time waits and weights |

The key_weight type contains the actor's public key and associated weight. The permission_level_weight type consists of the actor's account@permission level and associated weight. The wait_weight contains the time wait and associated weight (used to satisfy action authorizations in delayed user transactions. All of these types allow to define lists of authority factors that are used for satisfaction of action authorizations.

#### Authority Factors

Every authority table linked to a given permission lists potential factors explicitly used in the evaluation of the action authorization. A factor type can be one of the following:

- Actor's account name and permission level
- Actor's public key
- Time wait

The potential actors who may execute the action are specified by either public key or account name in the authority table. Time waits are special factors which are satisfied by publishing a transaction with a delay in excess of the defined time. These carry weights as well that may contribute to satisfy the threshold.

#### Authority Threshold

Authorization over a given action is determined by satisfying all explicit authorizations specified in the action instance. Those are in turn individually satisfied by evaluating each factor (account, public key, wait) for satisfaction and summing the weights of those that are satisfied. If the sum equals or exceeds the weight threshold, the action is authorized.

Example:

The authority table for jack's release-code named permission is shown in the diagram below. In order to authorize an action under that permission, a threshold of 2 must be reached.

Since both katey@active and kyle@active factors have a weight of 2, either one can satisfy the action authorization. This means that either katey or kyle with a permission level of active or higher can independently execute any action under jack's release-code permission.

Alternatively, it would require two acounts each with weight of 1 to satisfy the action authorization - in this case account with public key SYS7Hnv4iBfcw2... and nick@active.

# Anatomy of Wire Smart Basics

## Development Language

C++ is the primary language for developing smart contracts on the Wire blockchain. The required C++ expertise for writing smart contracts on Wire is minimal, which makes it accessible if you have prior experience with languages such as C, Java, C#, or TypeScript.

## Project Structure

### Flexibility in Structure

Smart contract development on Wire offers significant flexibility regarding how you structure your project. You can opt for a single monolithic .cpp file or divide your code across multiple files. For more complex projects, a build system like CMake can be used to manage the project components effectively.

#### Single File Example

Below is an example of a simple smart contract contained within a single file. This basic setup requires no additional files to compile:

project/contractname.cpp

# _include_ &lt;sysio/sysio.hpp&gt;

CONTRACT contractname : _public_ contract {

_public_:

_using_ contract::contract;

ACTION dosomething() {

// Action implementation

}

};

#### Multi-File Structure

For developers who prefer to organize their code more granularly, splitting the project into multiple files is also an option.

Header File (contractname.hpp):

project/include/contractname.hpp

# _pragma_ once

# _include_ &lt;sysio/sysio.hpp&gt;

CONTRACT contractname : _public_ contract {

_public_:

_using_ contract::contract;

ACTION dosomething()

}

The code snippet above are essentially equivalent to:

project/include/contractname.hpp

# _pragma_ once

// Import built-in classes and utilities

# _include_ &lt;sysio/sysio.hpp&gt;

// Class definition

_class_ \[\[sysio::contract\]\] contractname : _public_ sysio::contract {

_public_:

_using_ contract::contract;

\[\[sysio::action\]\]

_void_ dosomething();

};

Source File (contractname.cpp):

project/src/contractname.cpp

_void_ contractname::dosomething() {

// Actual function implementation goes here

}

### Header vs. Source Files

In C++, code is typically split into header files (.hpp or .h) and source files (.cpp), especially when projects get large. This helps with code organization and readibility.

- Header files are used to declare functions, classes, structs, and other types.
- Source files are used for the implementation of functions declared in header files.

### Managing Include Directories

When compiling your project, you will need to tell the compiler where to find your header files.

Generally, you will want to put your header files in a directory called include/, and your source files in a directory called src/.

Directory Structure Example:

project/

include/

contractname.hpp

src/

contractname.cpp

### Additional directories

#### /ricardian

This directory stores Ricardian contracts, which are written in human-readable language (.md) and describe what the contract actions intend to achieve, clarifying the technical and legal terms of the contract. They are typically included alongside the smart contract code, ensuring that each action within the smart contract is accompanied by a corresponding Ricardian contract that clearly states its purpose and implications.

/project/ricardian/contractname.md

\## \`dosomething\` Action

\### Description

...

\### Intent

...

\### Authorization

...

&nbsp;

&nbsp;

# Basic Contract Structure

Smart contracts resemble classes in traditional object-oriented programming. Here's a basic overview of how you structure a smart contract.

project/contractname.cpp

# _include_ &lt;sysio/sysio.hpp&gt;

CONTRACT contractname : _public_ sysio::contract {

_public_:

_using_ contract::contract; // Inherit constructor

};

### Key Components

#### CONTRACT Definition

The CONTRACT keyword is utilized to inform the compiler that we are defining an Wire smart contract. It is followed by the contract's name and the base class from which this contract inherits.

project/contractname.cpp

CONTRACT contractname : _public_ sysio::contract {

// Contract code here

};

Good to Know:

- It's a common practice to keep the contract name the same as the .cpp file name. Some build systems enforce this, and errors related to discrepancies can be obscure.

#### Access Modifiers

Access modifiers in C++ define the scope of accessibility for elements within your contract. All elements under an access modifier will inherit that scope.

- public: Elements are visible and accessible from any part of the program, as well as by other programs that interact with the contract.
- private: Accessibility is restricted solely to the contract itself.
- protected: This modifier allows visibility of elements to the contract and any inheriting contracts.

_public_:

// Public elements here

_private_:

// Private elements here

warning

Access modifiers in C++ do not control the external accessibility of the contract's elements like actions and tables, which are always publicly accessible outside your contract.

## Primary Elements of Smart Contracts

Smart contracts primarily consist of:

- Actions: These are the entry points for your contract. Actions are functions that you define to interact with and modify data.
- Tables: These are used to store persistent data within your smart contract on the blockchain.

We’ll explore these topics in greater detail in the future sections.

# Types

## Basic Types

These are the basic types that come built-in with C++.

Unless otherwise specified, the types below are imported from the &lt;sysio/sysio.hpp&gt; header.

# _include_ &lt;sysio/sysio.hpp&gt;

### Integer Types

Integer types are used to represent whole numbers. They can be either signed (positive or negative) or unsigned (positive only).

| Integer Types | Description |
| --- | --- |
| bool | Boolean |
| int8_t | Signed 8-bit integer |
| int16_t | Signed 16-bit integer |
| int32_t | Signed 32-bit integer |
| int64_t | Signed 64-bit integer |
| int128_t | Signed 128-bit integer |
| uint8_t | Unsigned 8-bit integer |
| uint16_t | Unsigned 16-bit integer |
| uint32_t | Unsigned 32-bit integer |
| uint64_t | Unsigned 64-bit integer |
| uint128_t | Unsigned 128-bit integer |

#### Other Integer Types

| Integer Types | Description |
| --- | --- |
| signed_int | Variable-length signed 32-bit integer |
| unsigned_int | Variable-length unsigned 32-bit integer |

info

You must include required header #include &lt;sysio/varint.hpp&gt; for signed_int and unsigned_int:

### Floating-Point Types

Floating-point types are used to represent decimal numbers.

warning

Floating-point types are not precise. They are not suitable for storing currency values, and are often problematic for storing other types of data as well. Use them with caution!

| Float Types | Description |
| --- | --- |
| float | 32-bit floating-point number |
| double | 64-bit floating-point number |

### Byte Types

Byte types are used to represent raw byte sequences, such as binary data or strings.

| Blob Types | Description |
| --- | --- |
| bytes | Raw byte sequence |
| string | String |

### Time Types

Time types are used to represent time, specifically relating to blocks.

| Time Types | Description |
| --- | --- |
| time_point | Point in time in microseconds |
| time_point_sec | Point in time in seconds |
| block_timestamp | Block timestamp |

#### Utility Functions

| Function | Description |
| --- | --- |
| time_point sysio::current_time_point() | Get the current time point |
| const microseconds& time_point.time_since_epoch() | Get the microseconds since the epoch |
| uint32_t time_point.sec_since_epoch() | Get the seconds since the epoch |
| block_timestamp sysio::current_block_time() | Get the current block time |

### Hash Types

Hash types are used to represent cryptographic hashes such as SHA-256.

| Checksum Types | Description |
| --- | --- |
| checksum160 | 160-bit checksum |
| checksum256 | 256-bit checksum |
| checksum512 | 512-bit checksum |

## Custom Types

These are the custom types that come built-in with Wire Sysio. You will likely use some of these types often in your smart contracts.

### Name Type

The name type is used to represent account names. It is a 64-bit integer, but it's displayed as a string.

A variety of system functions require names as parameters.

You have three ways of turning a string into a name:

- name{"string"}
- name("string")
- "string"\_n

If you want to get the uint64_t value of a name, you can use the value method.

name a = name("hello");

_uint64_t_ b = a.value;

### Key and Signature Types

The public_key and signature types are used to represent cryptographic keys and signatures.

#### Recovering a key from a signature

# _include_ &lt;sysio/crypto.hpp&gt;

function recover(checksum256 hash, signature sig) {

public_key recovered_key = recover_key(hash, sig);

}

### Asset Types

The asset type is used to represent a quantity of a digital asset. It is a 64-bit integer with a symbol, but it's displayed as a string.

It is resistent to overflow and underflow, and has various methods for performing arithmetic operations easily.

| Asset Types | Description |
| --- | --- |
| symbol | Asset symbol |
| symbol_code | Asset symbol code |
| asset | Asset |

info

You must include required header #include &lt;sysio/asset.hpp&gt; for asset types.

#### Creating an asset

There are two parts to an asset: the quantity, and the symbol. The quantity is a 64-bit integer, and the symbol is a combination of a string and a precision.

// symbol(&lt;symbol (string)&gt;, &lt;precision (1-18)&gt;)

symbol mySymbol = symbol("TKN", 4);

// asset(&lt;quantity (int64_t)&gt;, &lt;symbol&gt;)

asset myAsset = asset(1'0000, mySymbol);

#### Performing arithmetic operations

You can easily do arithmetic operations on assets.

asset a = asset(1'0000, symbol("TKN", 4));

asset b = asset(2'0000, symbol("TKN", 4));

asset c = a + b; // 3'0000 TKN

asset d = a - b; // -1'0000 TKN

asset e = a \* 2; // 2'0000 TKN

asset f = a / 2; // 0'5000 TKN

Symbol matching

Doing arithmetic operations on assets with different symbols will throw an error, but only during runtime. Make sure that you are always doing operations on assets with the same symbol.

#### Asset Methods

You can convert an asset to a string using the to_string method.

std::string result = a.to_string(); // "1.0000 TKN"

You can also get the quantity and symbol of an asset using the amount and symbol methods.

_int64_t_ quantity = a.amount; // 1'0000

symbol sym = a.symbol; // symbol("TKN", 4)

When using an asset, you always want to ensure that it is valid, i.e. the amount is within range.

_bool_ valid = a.is_valid();

#### Symbol Methods

You can convert a symbol to a string using the to_string method.

std::string result = mySymbol.to_string(); // "4,TKN"

You can also get the raw uint64_t value of a symbol using the value method.

_uint64_t_ value = mySymbol.value;

When using a symbol by itself, you always want to make sure that it is valid. However, when using asset, it already checks the validity of the symbol within its own is_valid method.

_bool_ valid = mySymbol.is_valid();

#### Symbol Limitations

Symbols have a precision between 1 and 18. This means that you can have a maximum of 18 decimal places.

// Valid

symbol mySymbol = symbol("TKN", 4);

// Invalid

symbol mySymbol = symbol("TKN", 19);

Symbol codes are limited to 7 characters.

// Valid

symbol mySymbol = symbol("TKN", 4);

// Invalid

symbol mySymbol = symbol("ISTOOLONG", 4);

## Structs

Structs are used to represent complex data. They are similar to classes, but are simpler and more lightweight(similar to JSON ojects).

_struct_ myStruct {

_uint64_t_ id;

};

# Actions

An action is a specific function or operation that can be executed on a smart contract. Smart contracts are self-executing programs with predefined rules and conditions, and actions are the entry points that allow accounts or other contracts to interact with them.

## Defining an Action in Wire Smart Contracts

- Action with specified return type

If you want the action to have a return type, you must use the \[\[sysio::action\]\] syntax followed by the desired return type.

\[\[sysio::action\]\] std::string myaction() {

// ...

_return_ "Hello";

}

warning

Return values are only usable outside the blockchain and cannot currently be used within Wire for smart contract composability.

- Simple Action: A shorthand method that always returns void

If you don’t need to specify the return type, you can use the ACTION macro, which is a shorthand for \[\[sysio::action\]\] void.

ACTION myaction() {

//...

}

## Inline Actions

Inline actions allow a contract to call an action of another contract from within its own code. This is useful for building functionality on top of existing contracts.

Let’s demonstrate this with two simple contracts: seller and buyer. In this example we will define an inline action notifysale on seller contract which would be called within buyitem action on the buyer contract.

# _include_ &lt;sysio/sysio.hpp&gt;

_using_ _namespace_ sysio;

# _include_ &lt;sysio/sysio.hpp&gt;

# _include_ &lt;sysio/asset.hpp&gt;

_using_ _namespace_ sysio;

CONTRACT seller : _public_ contract {

_public_:

_using_ contract::contract;

ACTION notifysale(name buyer_name, _uint64_t_ item_id, asset price) {

require_auth(get_self()); // Only the seller contract can call this action

// ...business logic to process the sale

print("Item ", item_id, " sold to ", buyer_name, " for ", price);

}

};

# _include_ &lt;sysio/sysio.hpp&gt;

# _include_ &lt;sysio/asset.hpp&gt;

_using_ _namespace_ sysio;

CONTRACT buyer : _public_ contract {

_public_:

_using_ contract::contract;

ACTION buyitem(name buyer_account, name seller_account, _uint64_t_ item_id, asset price) {

require_auth(buyer_account);

// ...business logic

// Notify seller of the purchase

action(

permission_level{get_self(), "active"\_n},

seller_account, // Seller's contract account

"notifysale"\_n, // Action on the seller contract

std::make_tuple(buyer_account, item_id)

).send();

print("Buyer: Purchased item ", item_id, " from ", seller_account);

}

};

### Inline Action Constructor

The action constructor takes four arguments:

action(

&lt;permission_level&gt;,

&lt;contract&gt;,

&lt;action&gt;,

&lt;data&gt;

).send();

#### Parameters of the action constructor

| Parameter | Type | Description |
| --- | --- | --- |
| permission_level | permission_level | Specifies who is authorizing the action and at what permission level. Constructed using {actor, permission}. |
| contract | name | The account name where the target action is deployed. This is the contract you are calling. |
| action_name | name | The name of the action you want to invoke on the target contract. |
| data | std::tuple | The data to be passed to the action, packaged as a tuple containing the arguments required by the target action. Use std::make_tuple to create it. |

TIP

- To convert a string into a name type for parameters like contract and action_name, use the name() function.
- Use std::make_tuple() to package multiple arguments together into the data parameter that matches the target action’s expected structure.
  - std::make_tuple(arg1, arg2, arg3, ...);

##### Setting Up the Permission Level

The permission_level argument specifies the permission level under which the action will be executed. It consists of two components:

permission_level(

account,

permission

)

- account (name type): The account authorizing the action.
- permission (name type): The permission level of the account (e.g., "active"\_n).

IMPORTANT

When you call an inline action, the contract initiating the call becomes the new sender. For security reasons, the original authorization is not passed to the called contract. This prevents the called contract from performing actions on behalf of the original sender, such as transferring tokens without explicit permission.

###### Setting Up Special Permission (eosio.code)

To allow your contract to call inline actions on other contracts,you need to grant it the special eosio.code permission. Without this permission, your contract cannot execute actions on other contracts.

This permission is on the active permission level so that it allows other contracts using the require_auth() to verify that your contract has the authority to perform the action.

###### How to Add the eosio.code Permission

Add the eosio.code permission to the contract account active permission to enable calling inline actions by the contract account's active permission.

clio set account permission yourcontract active --add-code _\-p_ yourcontract@active

Example of post-update permission's hierarchy:

owner

• YOUR_PUBLIC_KEY

↳ active

• YOUR_PUBLIC_KEY

• &lt;<yourcontract@eosio.code>&gt;

# State Data

There are two types of data in a smart contract: state data and transient data. State data is persistent data that is stored on the blockchain. Transient data is only stored during the execution of a transaction.

## Data Models

Data model is a serializable C++ struct that represents the data object to be stored on the blockchain. It can contain any data type that is also serializable. All common data types are serializable, and you can also create your own serializable data types, such as other models that start with the TABLE keyword.

TABLE UserModel {

_uint64_t_ id;

name account_name;

_uint64_t_ primary_key() _const_ { _return_ id; }

};

### Defining a model

Defining a model in Wire smart contracts is similar to defining a C++ struct, but there are some important differences:

1. Use the TABLE Macro instead of Struct: Instead of using the Struct keyword, you must use the TABLE macro. This macro tells the Wire system that you’re defining a data table that can be stored on the blockchain.
2. Define a primary_key Function: You must include a primary_key() that returns a uint64_t. This function specifies the primary key for the table, which is crucial for indexing and lookup.

#### Primary Key

- The primary key must be a uint64_t (you can also use name.value since it evaluates to a uint64_t).
- It must be unique for each row in the table.

#### Secondary Key

A secondary index is more flexible than a primary key and it's primaraly used when you intend to associate multiple rows with the same key. It can be any of the following data types:

- uint64_t
- uint128_t
- double
- long double
- checksum256

💰 Cost considerations

Each index costs RAM per row, so you should only use secondary indices with caution.

### Scope

The scope of a table is a way to partition the data in the table using a uint64_t, that determines which partition the data is stored in.

If we were to imagine the database as a JSON object, it might look like this:

tables.json

{

"users": {

1: \[

{

"id": 1,

"account_name": "jack"

},

{

"id": 2,

"account_name": "nick"

}

\],

2: \[

{

"id": 1,

"account_name": "daniel"

}

\]

}

}

By design, the same primary key can be used in different scopes without causing any conflicts. This is a useful approach because it allows you to partition your data logically within the same table, offering flexibility to organize data according to your needs.

## Multi-Index Table

The multi-index table is the most common way to store data on the Wire blockchain. It is a persistent key-value store that can be indexed in multiple ways, but always has a primary key.

### Defining a Multi-Index Table

To create a multi-index table you must have a model defined with at least a primary key. You can then create a multi-index table by using the multi_index template, and passing in the name of the table/collection and the model you want to use.

TABLE UserModel ...

_using_ users_table = multi_index&lt;"users"\_n, UserModel&gt;;

This will create a table called users that uses the UserModel model. You can then use this table to store and retrieve data from the blockchain.

### Instantiating a table

To do anything with a table, you must first instantiate it. To do this, you must pass in the contract that owns the table, and the scope that you want to use.

ACTION myaction() {

name mycontractaccount = get_self();

users_table users(mycontractaccount, mycontractaccount.value);

}

### Inserting data

To insert data, use the emplace(), which takes a lambda/anonymous function that accepts a reference to the model that you want to insert.

users.emplace(mycontractaccount, \[&\](_auto_& row) {

row.id = 1;

row.account_name = "jack"\_n;

});

You can also define a model first, and insert it into the entire row.

UserModel user = {

.id = 1,

.account_name = name("jack")

};

users.emplace(mycontractaccount, \[&\](_auto_& row) {

row = user;

});

### Retrieving data

To retrieve data from a table, you will use the find() method on the table, which takes the primary key of the row that you want to retrieve. This will return an iterator (reference) to the row.

_auto_ iterator = users.find(1);

Always Check If the Row Exists

When you retrieve data from a table using the find() method, you must check whether the row actually exists. If the row is not found, the iterator returned will be equal to users.end(), which is a special iterator representing the end of the table.

_if_ (iterator != users.end()) {

// You found the row

}

#### Access the data

You have two ways to access the data in the row from the iterator:

- Using the \* (dereference) Operator: This gives you a reference to the row’s data object.

UserModel user = \*iterator;

_uint64_t_ id = user.id;

name account = user.account_name;

- Using the -> (member access) Operator: This allows you to access the members of the row directly through the iterator.

UserModel user = \*iterator;

_uint64_t_ id = iterator->id;

name account = iterator->account_name;

### Modifying data

To modify data in a table, you must use the modify method, which takes a reference to the iterator you want to modify, a RAM payer, and a lambda/anonymous function that allows us to modify the data.

users.modify(iterator, mycontractaccount, \[&\](_auto_& row) {

row.account_name = name("nick");

});

### Removing data

To remove data from a table, use the erase method, which takes a reference to the iterator you want to remove.

users.erase(iterator);

### Using a secondary index

Using a secondary index will allow you to query your table in a different way. For example, if you wanted to query your table by the account_name field, you will need to create a secondary index on that field.

#### Redefining our model and table

To use a secondary index, you must first define it in your model. You do this by using the indexed_by template, and passing in the name of the index, and the type of the index.

TABLE UserModel {

_uint64_t_ id;

name account_name;

_uint64_t_ primary_key() _const_ { _return_ id; }

_uint64_t_ account_index() _const_ { _return_ account_name.value; }

};

_using_ users_table = multi_index<"users"\_n, UserModel,

indexed_by<"byaccount"\_n, const_mem_fun<UserModel, _uint64_t_, &UserModel::account_index>>

\>;

The indexed_by template can be a bit confusing, so let's break it down.

indexed_by<

&lt;name_of_index&gt;,

const_mem_fun<

&lt;model_to_use&gt;,

&lt;index_type&gt;,

&lt;pointer_to_index_function&gt;

\>

\>

The name_of_index is the name of the index that you want to use. This can be anything, but it's best to use something that describes what the index is for.

The model_to_use is the model that you want to use for the index. This is usually the same model that you are using for the table, but it doesn't have to be. This is useful if you want to use a different model for the index, but still want to be able to access the data in the table.

The index_type is the type of the index, and is limited to the types we discussed earlier.

The pointer_to_index_function is a pointer to a function that returns the value that you want to use for the index. This function must be a const_mem_fun function, and must be a member function of the model that you are using for the index.

#### Using the secondary index

To query your table by a secondary index , you must get the index from the table first, and then use find() on the index.

_auto_ index = users.get_index&lt;"byaccount"\_n&gt;();

_auto_ iterator = index.find(name("jack").value);

To modify data in the table using the secondary index, you use the modify() method on the index.

index.modify(iterator, mycontractaccount, \[&\](_auto_& row) {

row.account_name = name("foobar");

});

## Singleton Table

A singleton table is a special type of table that can only have one row per scope. This is useful for storing data that you only want to have one instance of.

The primary differences between a singleton table and a multi-index table are:

- Singletons do not need a primary key on the model.
- Singletons can store any type of data, not just predefined models.
- Singletons do not support secondary indices.

### Defining a Siggleton Table

To define a singleton table, you use the singleton template, and pass in the name of the table, and the type of the data that you want to store.

# _include_ &lt;sysio/singleton.hpp&gt;

TABLE ConfigModel {

_bool_ is_active;

};

_using_ config_table = singleton&lt;"config"\_n, ConfigModel&gt;;

_using_ is_active_table = singleton<"isactive"\_n, _bool_\>;

n the example above, both tables are identical; however, the is_active table will be more efficient and performant since it eliminates the overhead associated with storing the entire ConfigModel struct.

### Instantiating a table

Just like the multi_index table, you must first instantiate the table, and then you can use it.

name mycontractaccount = get_self();

config_table configs(mycontractaccount, mycontractaccount.value);

The singleton table takes two parameters in its constructor. The first parameter is the contract that the table is owned by, and the second parameter is the scope.

### Retrieving data

There are a few ways to fetch data from a singleton.

#### Get or fail

This will error out at runtime if there is no existing data. To prevent this, you can use the exists method to check if there is existing data.

_if_ (!configs.exists()) {

// handle error

}

ConfigModel config = configs.get();

_bool_ isActive = config.is_active;

#### Get or default

This will return a default value, but will not persist the value.

ConfigModel config = configs.get_or_default(ConfigModel{

.is_active = true

});

#### Get or create

This will return a default value, and will persist the value.

ConfigModel config = configs.get_or_create(ConfigModel{

.is_active = true

});

### Inserting data

To persist data in a singleton, you can use the set method, which takes a reference to the data that you want to set.

configs.set(ConfigModel{

.is_active = true

}, mycontractaccount);

### Removing data

Once you've instantiated a singleton, it's easy to remove it. Just called the remove method on the instance itself.

configs.remove();

# Using EOS Block Explorer

### What is a block explorer?

A block explorer is an online application that enables individuals to interact with and examine information stored on the blockchain. Such tools provide a straightforward interface for users to view transaction histories, account balances, and additional relevant data on a blockchain. Block explorers catalog and display all transactions on a specific network.

As we develop and refine our code, we'll regularly use the EOS Authority Block Explorer. This tool will be invaluable for monitoring our transactions and observing the real-time effects of our interactions with the blockchain, as well as get copy-ready clio commands and inspect data in our tables.

### Using EOS Authority Block Explorer

#### Step 1: Access the Website

Begin by navigating to the [EOS Authority Block Explorer](https://eosauthority.com/) website.

#### Step 2: Select the Local Testnet

Once on the site, from the network selection dropdown menu select Local Testnet. This option allows you to connect to a locally running EOS-based testnet, which is ideal for development and testing purposes.

#### Step 3: Enter Your RPC URL

By default once local testnet has been selected,the default RPC URL, <http://127.0.0.1:8888>. The explorer uses the RPC URL to access the RPC API, allowing it to retrieve data and interact with contracts deployed on your local Wire node.

#### Step 4: Confirm and Explore

Once connected, search for a deployed contract. Here, you can view its details, transactions, tables, and interact with its actions.

# Quick Start: Hello World Contract

## Prerequisites

- [Installation and Development Environment Setup](https://docs.wire.network/docs/getting-started/install-dependencies"%20\l%20"binary-installation).
- This page assumes you are familiar with [Smart Contract Basics](https://docs.wire.network/docs/smart-contract-development/smart-contract-basics).

## Steps

### 1\. Clone the Contract Repository

Start by cloning the existing GitHub repository containing the Hello World contract to your local environment:

git clone <https://github.com/Wire-Network/guides.git> && cd guides/hello-world-contract

Then open the code into your favorite code editor and inspect the files.

### 2\. Compile the Contract

Compile it using the ./build.sh. This script uses the Wire Contract Development Toolkit (CDT) the Hello World contract into WebAssembly (WASM) format. The script will create a compilation folder hello/ with the WASM and ABI files.

./build.sh

Upon successful compilation, you will see a hello folder with hello.abi and hello.wasm files.

hello-world-contract/

| ....

├── hello

│ ├── hello.abi

│ └── hello.wasm

| ...

### 3\. Deploy the Contract

Before deploying, ensure you have an account to deploy the contract to. Create an account if necessary and replace YOUR_PUBLIC_KEY with your actual public key when you created a wallet(see [Import Keys](https://docs.wire.network/docs/getting-started/create-development-wallet"%20\l%20"import-keys-into-your-wallet)). Your wallet must be also unlocked before using it(see [Unlock a wallet](https://docs.wire.network/docs/getting-started/create-development-wallet"%20\l%20"unlock-a-wallet))

#### 3.1. Create an account using clio

clio create account sysio hello _$PUBLIC_KEY_ _\-p_ sysio@active

This command enables the sysio system account to create a new account named hello on the Wire blockchain. The -p sysio@active specifies that the active permission of the sysio account is used to authorize the account creation.

#### 3.2. Deploy the contract

./deploy.sh

### 4\. Push a Transaction

Invoke the hi action within the contract:

clio push action hello hi '\["bob"\]' _\-p_ bob@active

This command triggers the hi action for the user bob, and if authorized by bob, it prints "Hello, bob".

Repeat the same passing "alice" as data to the action and using the same permissions:

clio push action hello hi '\["alice"\]' _\-p_ bob@active

### 5\. Change the contract code

Next, let's change the contract code by enabling require_auth() function and see firsthand how checks and permissions work in contract actions. If there's a mismatch between the authorizing user and the user parameter, the contract will not execute due to the require_auth check.

Comment out Line 5 in hello.cpp

hello.cpp

# _include_ &lt;hello.hpp&gt;

_void_ hello::hi(name user) {

require_auth(user);

print("Hello, ", user);

}

[Recompile](https://docs.wire.network/docs/smart-contract-development/hello-world-contract-short"%20\l%20"2-compile-the-contract) and [redeploy](https://docs.wire.network/docs/smart-contract-development/hello-world-contract-short"%20\l%20"3-deploy-the-contract) the contract. Then execute:

clio push action hello hi '\["alice"\]' _\-p_ bob@active

This will result in an authorization error since bob is trying to execute an action that requires alice's permission.

CLI output:

## Bonus ⭐️

### Inspect the contract on EOS Authority Block Explorer

Feel free to explore your contract on [EOS Authority](https://docs.wire.network/docs/smart-contract-development/block-explorer), which also provides tools to generate ready-to-use clio commands, making it easier to push transactions and interact with your contracts directly. This is a great way to get hands-on experience and deepen your understanding of smart contracts.

info

Remember to replace cleos with clio in any generated commands to ensure compatibility with the Wire Sysio software.

# Company Contract

## Overview

This page will guide you to creating and developing a simple contract using Wire CDT and C++ language. While prior knowledge of C++ is not necessary for this tutorial, we encourage you to familiarize yourself with the basics of C++ to enhance your understanding.

## Prerequisites

- [Smart Contract Basics](https://docs.wire.network/docs/smart-contract-development/smart-contract-basics)

## Step-by-Step Guide to Creating a Company Contract Smart Contract

### 1\. Set Up Your Contract Workspace

Navigate to a directory of your choice and create a new subdirectory for your contract, along with its content include/ and src/.

/your-contracts-workspace

mkdir company-contract && cd company-contract && mkdir include src company && touch include/company.hpp src/company.cpp

Open company-contract in your preferred text editor to begin coding.

### 2\. Write the Contract Code

In C++, splitting class declarations and definitions into separate header (.hpp) and source (.cpp) files is a common practice that promotes better code organization, readability, and compile time-efficiency. This approach helps segregating interface from implementation; as well hiding the implementation details from other parts of the program and exposing only what is necessary. For the purposes of this and future tutorials, we will stick to that approach.

2.1. Define contract interfaces in company.hpp

- The sysio/sysio.hpp header file contains necessary classes and built-in utility functions for contract development.

/your-contracts-workspace/company-contract/company.hpp

# _pragma_ once

# _include_ &lt;sysio/sysio.hpp&gt;

# _include_ &lt;string&gt;

_using_ _namespace_ sysio;

#### 2.1. Define the employees contract class

You can use either the simplified or the long syntax for defining contracts. In this tutorial we will be using primarily the short syntax for better readability. We would also define two actions upsertemp() and getallemp().

/your-contracts-workspace/company-contract/company.hpp

# _pragma_ once

# _include_ &lt;sysio/sysio.hpp&gt;

# _include_ &lt;string&gt;

_using_ _namespace_ sysio;

// Using short syntax for structs

CONTRACT company : _public_ contract {

_public_:

_using_ contract::contract;

// Action to upsert (insert or update) an employee record

ACTION upsertemp(name user, _const_ std::string& name, _const_ std::string& email, _const_ std::string& status);

// Action to retrieve and print all employee records

ACTION getallemp();

}

info

Long syntax

// Using long syntax for structs

_class_ \[\[sysio::contract("employees")\]\] employees : _public_ contract {

_public_:

_using_ contract::contract; // Inherits the base contract constructor.

employees(name receiver, name code, datastream<_const_ _char_\*> ds) : contract(receiver, code, ds) {}

};

LEARN

The short syntax in C++ contracts, such as those used in the Wire blockchain framework, is possible due to the language’s support for preprocessor's directive like #define. This directive is a preprocessor command that creates macros, serving as symbolic names or aliases for code fragments. Before compilation, the preprocessor scans the source code and replaces these macros with their defined sequences. Essentially, #define allows developers to define constants, create function-like macros, or insert code snippets, improving readability and maintainability by eliminating repetitive code segments.

[Source code](https://github.com/Wire-Network/wire-cdt/blob/main/libraries/sysiolib/contracts/sysio/contract.hpp"%20\l%20"L18)

# _define_ CONTRACT _class_ \[\[sysio::contract\]\]

#### 2.2. Define the Employee Struct and Multi-Index Table

Within the employees contract class, let's add a struct named employee to represent the table that holds individual employee records. We will define it with several fields:

• user: The name of the employee, which will serve as the primary key for the table. It uniquely identifies each employee record.

• name: A string that stores the full name of the employee.

• email: A string representing the employee’s email address.

• status: A string that indicates the current status of the employee within the organization. (e.g., “active”, “inactive").

The primary_key() function within the struct returns the user.value, which is the numeric representation of the user. The multi_index container named employee_index is defined to manage the storage of these records. It allows for efficient storing, updating, and querying of employee data based on the primary key.

/your-contracts-workspace/company-contract/company.hpp

# _pragma_ once

# _include_ &lt;sysio/sysio.hpp&gt;

# _include_ &lt;string&gt;

_using_ _namespace_ sysio;

CONTRACT company : _public_ contract {

_public_:

_using_ contract::contract;

// Action to upsert (insert or update) an employee record

ACTION upsertemp(name user, _const_ std::string& name, _const_ std::string& email, _const_ std::string& status);

// Action to retrieve and print all employee records

ACTION getallemp();

_private_:

// Employee struct representing a record in the employees table.

TABLE employee {

name user;

std::string name;

std::string email;

std::string status;

_uint64_t_ primary_key() _const_ { _return_ user.value; }

};

// Type definition for the multi-index table handling employee records.

_using_ employee_index = sysio::multi_index&lt;"employees"\_n, employee&gt;;

};

Next let's define the implementation for the actions upsertemp and getallemp.

#### 2.3. Defining the upsertemp() action

upsertemp will be used for upserting an employee record. Refer to the comments within the code for more explanation of what each line/block do.

/your-contracts-workspace/company-contract/company.cpp

# _include_ &lt;sysio/print.hpp&gt;

# _include_ &lt;company.hpp&gt;

_void_ company::upsertemp(name user, _const_ std::string& name, _const_ std::string& email, _const_ std::string& status) {

require_auth(user); //built-in method that only the authenticated user can execute this action

// Including the require_auth() method in this action ensures that only authenticated users, typically those verified to be the smart contract’s account or another authorized account, can initiate these actions. This method is typically used for actions that involve sensitive operations like updating a user record. By requiring authentication, you can safeguard customer-specific actions, ensuring that such operations are performed exclusively by the account owner and not by unauthorized parties.

// Access the table with \`get_self()\` as the scope

employee_index emp_table(get_self(), get_self().value);

// Find the record with PK matching the user

_auto_ employee_itr = emp_table.find(user.value);

_if_ (employee_itr == emp_table.end()) {

// If no record is found, create a new one

emp_table.emplace(user, \[&\](_auto_& new_employee) {

new_employee.user = user;

new_employee.name = name;

new_employee.email = email;

new_employee.status = status;

});

print("Employee added: ", user);

} _else_ {

// Modify the record if the user matches

emp_table.modify(employee_itr, user, \[&\](_auto_& mod_employee) {

mod_employee.name = name;

mod_employee.email = email;

mod_employee.status = status;

});

print("Employee updated: ", user);

}

}

#### 2.4. Defining the getall() action

The action below will retrieve all employee records from the employees multi-index table.

/your-contracts-workspace/company-contract/company.cpp

_void_ company::getallemp() {

employee_index emp_table(get_self(), get_self().value);

_for_ (_auto_ itr = emp_table.begin(); itr != emp_table.end(); itr++) {

print("Employee ID: ", itr->user, ", Name: ", itr->name, ", Email: ", itr->email, ", Status: ", itr->status, "\\n");

}

}

### 3\. Compile the Contract

Compile your contract into WebAssembly (WASM) format using the Wire Contract Development Toolkit (CDT). This command also generates the ABI file in the company folder.

cdt-cpp _\-abigen_ _\-contract_ company _\-o_ company/company.wasm src/company.cpp _\-I_ include

### 4\. Deploy the Contract

Before deploying, ensure you have an open wallet and account to deploy the contract to.

note

In Wire ecosystem, deploying a smart contract requires an account; an account can own one smart contract instance and a smart contract instance must be deployed to an account. Each account functions as a distinct namespace for the contract, which means that the contract’s code and its state are encapsulated within that account.

#### 4.1 Retrieve public key

Before proceeding, make sure you have the public key available from the key pair that was created when setting up your wallet. If you haven’t yet created a wallet or a key pair, you can do so by following the instructions [here](https://docs.wire.network/docs/getting-started/create-development-wallet).

export _PUBLIC_KEY_\=&lt;public-key-value&gt;

clio create account sysio company _$PUBLIC_KEY_ _\-p_ sysio@active

#### 4.2 Deploy the compiled contract

\[account\] \[WASM dir\] \[permission level\]

clio set contract company company _\-p_ company@active

The smart contract should now be live on your local blockchain. You can inspect through [Block Explorer](https://eosauthority.com/).

# Smart Contract Interactions using clio

## Overview

In the article you’ll learn how to execute actions on a contract with the clio tool. It guides you through inserting and updating records, checking updates, and testing out behavior on unauthorized change attempt.

## Prerequisites

- [Installation and Development Environment Setup](https://docs.wire.network/docs/getting-started/install-dependencies"%20\l%20"binary-installation)
- [Company contract tutorial](https://docs.wire.network/docs/smart-contract-development/company-contract)
- Two new accounts jack and nick

clio create account sysio jack _$PUBLIC_KEY_ _\-p_ sysio@active

clio create account sysio nick _$PUBLIC_KEY_ _\-p_ sysio@active

## Steps

### Step 1: Insert a record

First, let’s have Jack insert or update his own record.

clio push action company upsertemp '\["jack", "Jack Sparrow", "<jack@example.com>", "active"\]' _\-p_ jack@active

Output:

You could use block explorer to inspect the table and the transactions.

### Step 2: Perfom an update

Next, we update Jack’s record,

clio push action company upsertemp '\["jack", "Jack Nicholson", "<jack@example.com>", "active"\]' _\-p_ jack@active

Output:

Post-Action Check:

• Inspect Logs to ensure the update was executed. • Inspect Table to see Jack’s updated record.

### Step 3: Retrieve all users

clio push action company getallemp '{}' _\-p_ jack@active

Ouput:

### Step 4: Attempt unauthorized transaction

clio push action company upsertemp '\["nick", "Nick Fury", "<nick@example.com>", "active"\]' _\-p_ jack@active

This should fail since Jack should not be able to add records for other users because the contract enforces proper authorization via require_auth().

To insert Nick's record execute the following command:

clio push action company upsertemp '\["nick", "Nick Fury", "<nick@example.com>", "active"\]' _\-p_ nick@active

# Smart Contract Interactions with sdk-core JS library

## Prerequisites

Before starting this tutorial, ensure the following software is installed on your machine:

Dependencies Used:

| Dependency | Version | Purpose | Installation Link |
| --- | --- | --- | --- |
| Node.js | 18.8.0 | Runtime environment for executing JavaScript outside the browser. | [Install Node.js](https://nodejs.org/) |
| npm | 9.8.1 | Package manager for managing and installing JavaScript libraries. | Included with Node.js installation |
| TypeScript | 5.1.6 | Adds static types to JavaScript to enhance developer productivity and code quality. | [Install TypeScript](https://www.npmjs.com/package/typescript) |

You should also install and use [NVM](https://github.com/nvm-sh/nvm), to set a specific Node version in your project.

Once installed, you can use it like:

nvm use 18.18.0

## Steps

### 1\. Create & set up ts-dapp-sdk-wire

mkdir _\-p_ ts-dapp-sdk-wire && cd ts-dapp-sdk-wire && npm init _\-y_ && npm install --save-dev typescript@5.1.6 ts-node node-fetch && mkdir _\-p_ src && touch src/index.ts && touch .gitignore tsconfig.json && echo _\-e_ "node_modules/\\ndist/" >> .gitignore

#### 1.1. Add tsconfig.json

tsconfig.json

{

"compilerOptions": {

"target": "ES2022",

"module": "CommonJS",

"lib": \["ES2022", "DOM"\],

"allowJs": true,

"esModuleInterop": true,

"forceConsistentCasingInFileNames": true,

"moduleResolution": "Node",

"strict": false,

"outDir": "dist"

}

}

#### 1.2. Get your private key

Note your private key from the key pair generated earlier. You could output key pair value by running:

clio wallet private_keys _\--password_\=_$(cat_ _~/my-secret-pass.txt)_

#### 1.3. Add scripts to package.json

Modify scripts in package.json to:

package.json

{

"scripts": {

"watch": "tsc -w",

"exec": "node dist/index.js"

}

}

## 2\. Write the code

In this section, we will set up our application to interact with our local node from [Company Contract Tutorial](https://docs.wire.network/docs/smart-contract-development/company-contract).

### 2.1. Initialize ApiClient()

index.ts

_import_ { API, APIClient, FetchProvider, PrivateKey, SignedTransaction, Transaction, AnyAction, Action, PackedTransaction } _from_ "@wireio/core";

_const_ privateKey = "&lt;your-private-key&gt;"

_const_ endpoint = "<http://localhost:8888>"

_const_ apiClient = _new_ APIClient(

{ provider: _new_ FetchProvider(endpoint) }

);

#### API Client Initialization

- We import necessary modules like APIClient, FetchProvider, and transaction-related classes. You can see full SDK reference [here](https://wire-network.github.io/sdk-core).
- A private key is defined for signing transactions (make sure to replace it with your actual key).
- We specify the blockchain node’s API endpoint, in this case, a locally running node at <http://localhost:8888>.
- Finally, we initialize an instance of APIClient, which communicates with the blockchain via the FetchProvider, allowing us to interact with smart contracts for operations like signing and sending transactions.

Open up a terminal and run npm watch to run TypeScript compilation in watch mode. You should see the compiled dist folder.

### 2.2. Write API calls

Below is a breakdown of the API calls performed in the [code snippet](https://docs.wire.network/docs/smart-contract-development/interacting-with-contracts/smart-contracts-wirejs"%20\l%20"code), along with the corresponding line numbers for each operation:

- Fetch Local Blockchain Info: Retrieves the current blockchain status. See line 14.
- Access Smart Contract Data: Fetches the current state of the employees table from the company smart contract, including the number of rows and user details. See line 20-28.
- Retrieve Contract ABI: Obtains and prints the ABI (Application Binary Interface) of the company smart contract, detailing its methods and structures. See line 36-39.
- Prepare Transaction: Constructs a transaction payload to update the details of an employee named “Jack” and constructs a signature required to authorize this transaction. See line 45-71.
- Execute Transaction: Sends the transaction to the blockchain. See line 73-76.

#### code

_import_ { API, APIClient, FetchProvider, PrivateKey, SignedTransaction, Transaction, AnyAction, Action, PackedTransaction } _from_ "@wireio/core";

_const_ privateKey = "&lt;your-private-key&gt;"

_const_ endpoint = "<http://localhost:8888>"

_const_ apiClient = _new_ APIClient(

{ provider: _new_ FetchProvider(endpoint) }

);

(_async_ () => {

_const_ info = _await_ apiClient.v1.chain.get_info()

console.log("\\nBlockchain Info:");

console.log(JSON.stringify(info, _null_, 2));

// Retrieve rows from employees table in our company contract

_const_ tableRows: API.v1.GetTableRowsResponse = _await_ apiClient.call({

path: '/v1/chain/get_table_rows',

params: {

code: "company",

table: "employees",

scope: "company",

json: true

},

});

console.log(tableRows)

console.log(\`\\nEmployees Table Info:\`);

console.log(\`- Number of rows: ${tableRows.rows.length}\`);

console.log(\`- User emails: ${tableRows.rows.map(a => a.email).join(", ")}\`);

_const_ abiRes: API.v1.GetAbiResponse = _await_ apiClient.call({

path: '/v1/chain/get_abi',

params: {account_name: untypedAction.account},

});

_const_ { abi } = abiRes;

console.log("\\nContract ABI:");

console.log(JSON.stringify(abi, _null_, 2));

_const_ untypedAction: AnyAction = {

account: "company",

name: "upsertemp",

authorization: \[

{

actor: "jack",

permission: "active"

}

\],

data: {

user: "jack",

name: "Jackson Smith!!",

email: "<jack@example.com>",

status: "active"

}

}

_const_ action = Action.from(untypedAction, abi);

_const_ header = info.getTransactionHeader()

_const_ transaction = Transaction.from({ ...header, actions: \[action\] })

_const_ digest = transaction.signingDigest(info.chain_id)

_const_ privKey = PrivateKey.from(privateKey)

_const_ signature = privKey.signDigest(digest).toString()

_let_ signedTrx = SignedTransaction.from({ ...transaction, signatures: \[signature\] })

_const_ packed = PackedTransaction.fromSigned(SignedTransaction.from(signedTrx));

_const_ trx = _await_ apiClient.call({

path: '/v1/chain/push_transaction',

params: packed

})

console.log("\\nTransaction Result:");

console.log(JSON.stringify(trx, _null_, 2));

})();

## 3.Execute the code

You can inspect the employees table on the [EOS Block Explorer](https://eosauthority.com/account/company?network=localtest&endpoint=http:%2F%2F127.0.0.1:8888&token_symbol=EOS&scope=company&table=employees&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables) before executing the script.

Run npm run exec and you should see output in the console with the logs like:

➜ ts-app-sdk-wire npm run

Blockchain Info:

{

"server_version": "c83d8e08",

"chain_id": "8a34ec7df1b8cd06ff4a8abbaa7cc50300823350cadc59ab296cb00d104d2b8f",

"head_block_num": 538955,

"last_irreversible_block_num": 538954,

"last_irreversible_block_id": "0008394a52821c9552c17f8620576d53fe417e29068aee6ba6fe91b31591d052",

"head_block_id": "0008394bd3b0ae2b818eed6a626ef66c3750a2a7cfff48e61f1bc6a8d5203076",

"head_block_time": "2024-09-30T13:09:22.000",

"head_block_producer": "sysio",

"virtual_block_cpu_limit": 200000000,

"virtual_block_net_limit": 1048576000,

"block_cpu_limit": 200000,

"block_net_limit": 1048576,

"server_version_string": "v3.1.6",

"fork_db_head_block_num": 538955,

"fork_db_head_block_id": "0008394bd3b0ae2b818eed6a626ef66c3750a2a7cfff48e61f1bc6a8d5203076"

}

{

rows: \[

{

user: 'jack',

name: 'Jackson Smith',

...

....

Check update on [EOS Block Explorer](https://eosauthority.com/account/company?network=localtest&endpoint=http:%2F%2F127.0.0.1:8888&token_symbol=EOS&scope=company&table=employees&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables) ![](data:image/png;base64,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AggggAACCCCAAAIIIIBA+hAgoJw+jhOtRAABBBBAAAEEEEAAAQQQQAABBBBAAAEE0lyAgHKaHwIagAACCCCAAAIIIIAAAggggAACCCCAAAIIpA+BYDc3c9Wsbm5uHm1DAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQCSoARygF1uOksAggggAACCCCAAAIIIIAAAggggAACCCCQcgECyim3Y0sEEEAAAQQQQAABBBBAAAEEEEAAAQQQQCCgBAgoB9ThprMIIIAAAggggAACCCCAAAIIIIAAAggggEDKBQgop9yOLRFAAAEEEEAAAQQQQAABBBBAAAEEEEAAgYASIKAcUIebziKAAAIIIIAAAggggAACCCCAAAIIIIAAAikXIKCccju2RAABBBBAAAEEEEAAAQQQQAABBBBAAAEEAkqAgHJAHW46iwACCCCAAAIIIIAAAggggAACCCCAAAIIpFyAgHLK7dgSAQQQQAABBBBAAAEEEEAAAQQQQAABBBAIKAECygF1uOksAggggAACCCCAAAIIIIAAAggggAACCCCQcgECyim3Y0sEEEAAAQQQQAABBBBAAAEEEEAAAQQQQCCgBAgoB9ThprMIIIAAAggggAACCCCAAAIIIIAAAggggEDKBQgop9yOLRFAAAEEEEAAAQQQQAABBBBAAAEEEEAAgYASIKAcUIebziKAAAIIIIAAAggggAACCCCAAAIIIIAAAikXIKCccju2RAABBBBAAAEEEEAAAQQQQAABBBBAAAEEAkqAgHJAHW46iwACCCCAAAIIIIAAAggggAACCCCAAAIIpFyAgHLK7dgSAQQQQAABBBBAAAEEEEAAAQQQQAABBBAIKAECygF1uOksAggggAACCCCAAAIIIIAAAggggAACCCCQcgECyim3Y0sEEEAAAQQQQAABBBBAAAEEEEAAAQQQQCCgBAgoB9ThprMIIIAAAggggAACCCCAAAIIIIAAAggggEDKBQgop9yOLRFAAAEEEEAAAQQQQAABBBBAAAEEEEAAgYASIKAcUIebziKAAAIIIIAAAggggAACCCCAAAIIIIAAAikXIKCccju2RAABBBBAAAEEEEAAAQQQQAABBBBAAAEEAkqAgHJAHW46iwACCCCAAAIIIIAAAggggAACCCCAAAIIpFyAgHLK7dgSAQQQQAABBBBAAAEEEEAAAQQQQAAB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EFDuoAdOtQkQIECAAAECBAgQIECAAAECBAgQINDeAgLK7S1uewQIECBAgAABAgQIECBAgAABAgQIEOigAgLKHfTAqTYBAgQIECBAgAABAgQIECBAgAABAgTaW6Bbe2+wke299NJLjSxuWQIECBAgQIAAAQIECBAgQIAAAQIEOoFAv379OsFelnMXSx1Q9sUo55dGrQgQIECAAAECBAgQIECAAAECBAgQ6JwCUl50zuNurwkQIECAAAECBAgQIECAAAECBAgQINCwgIByw2RWIECAAAECBAgQIECAAAECBAgQIECAQOcUEFDunMfdXhMgQIAAAQIECBAgQIAAAQIECBAgQKBhAQHlhsmsQIAAAQIECBAgQIAAAQIECBAgQIAAgc4pIKDcOY+7vSZAgAABAgQIECBAgAABAgQIECBAgEDDAgLKDZNZgQABAgQIECBAgAABAgQIECBAgAABAp1TQEC5cx53e02AAAECBAgQIECAAAECBAgQIECAAIGGBQSUGyazAgECBAgQIECAAAECBAgQIECAAAECBDqngIBy5zzu9poAAQIECBAgQIAAAQIECBAgQIAAAQINCwgoN0xmBQIECBAgQIAAAQIECBAgQIAAAQIECHROAQHlznnc7TUBAgQIECBAgAABAgQIECBAgAABAgQaFhBQbpjMCgQIECBAgAABAgQIECBAgAABAgQIEOicAgLKnfO422sCBAgQIECAAAECBAgQIECAAAECBAg0LCCg3DCZFQgQIECAAAECBAgQIECAAAECBAgQINA5BQSUO+dxt9cECBAgQIAAAQIECBAgQIAAAQIECBBoWEBAuWEyKxAgQIAAAQIECBAgQIAAAQIECBAgQKBzCggod87jbq8JECBAgAABAgQIECBAgAABAgQIECDQsICAcsNkViBAgAABAgQIECBAgAABAgQIECBAgEDnFBBQ7pzH3V4TIECAAAECBAgQIECAAAECBAgQIECgYQEB5YbJrECAAAECBAgQIECAAAECBAgQIECAAIHOKSCg3DmPu70mQIAAAQIECBAgQIAAAQIECBAgQIBAwwIdOqD88ccfp/ff/6Dhne5sKzz40MPpT1f+uaHdHj9+fDrvggvTxIkTG1rPwh1f4Lrrb0h3331PQzsS37E//PFPDa1jYQIECBAov8CsuIb46KPJadKkSeXHmYk1jGvcuA574YUXZuJWfDQBAgQIEGg/gU9zn9l+tbMlAgQaFejW6AplWP76G25MN918cxo3bnxRnXnmnjuttdYX0y7f2Tl17dq1DFUsVR1uzlaPPPpo2mbrr6Tu3bu3qW6vvPJquv32f6addtg+9ejRo03rWKh8Ar+74vfphhv/mk4aeULq1WuBFhW8866709nnnJsuuuC81K3blJ+DP115Zerfr3/x/6kWK7Qy44knnkh333Nv+tY3v9HKEvVnR/2uvuba+m/muXv84PtpvXXXafV9bxAgQIDAzBVor2uIBx98KP3tppvTmLFj0muvvV7sVM+ePVP//v3ShhtskNZZZ+2Zu6Ml/PS4Dlt1lZXT4osvXsLaqRIBAgQIEKgvEI3+evTonrp0ad5+8dPcZ9bfgrkECJRBoMMFlKO1Rlxgb7bpJmnlnVYqDO+774H091tuTe+993764V7/VwbXUtXhJ/v+uGhp3NZgcqkqrzKfSWDSRx+lDz/8MJ10yinp6CFHpTnmmKPm8z6umU7p9FNPzQ8e2uenIeoXD4QOPGD/FvWIGX379q0730wCBAgQaB+BmX0N8c4776SLfnFxuv+BB9L/fOtbxYPJxRYbkG9Cu6aXX34pjXrq6XRhfj+u8/bac4+04IILts+O2woBAgQIECDQsMC7776b9vzhPumQgw5MK6zw+Wbrt+d9ZrMNmyBAYKYItE/UaAZWfeuvbJVWWXnltNYX12z61Jh+edzL6cGHHmya58VUgXgyONdcc02d4VWnE3j++RfSb393Rdp+u/+d7r7PNdec011mRi7QLbeaX2aZpWfkR/osAgQIEJhBAjP7GmLEyJPSG2+8no45emgaMGBAs1rHdPy32mqrplNOOS0NO3Z47nEzokWLp2YrmSBAgAABAgRmmUCkbGqttPd9Zmv1MJ8AgRkj0OECygP690/xX21Za8010xNPPFm0xuwMLXFHPfVUOn7EyDT82GE5d+2VRUqL9957Ny2z9DJpl112TgMXW6yJ6C9XX5Pu/dd9uYXqkU3z3nzrrfTHP12ZHn74kfTf//43LT5wYNo0t/re8MsbNC1T78Wvfn1Zuu3229LBBx4oCFgPqITzosvwRht+Of35qr+kFVdYIa244grTrOXwESekJZdYIu2w/XZNy32a70t0dRoxcmR6K3/Xhhx5ZJp//vmaPq/RF4cfcVT60pfWKtK2VK8buT3P+PmZ6fxzzy4CDHEB8/099kz7/mif9NDDD+cWbw+mbbfZOm280YbpuONHpOWWXTb17Dl/uvXW21K/foumZZcdnPOLX5VOOWlkmnPO5oH0+D0ZedLJacTxx6WFF1qoerNeEyBAoEMLlOUa4s677kqjR7+QTj5xZOrdu3eKVk3xu/3II4/m6V5ptVVXzSkv+qfLL/9N2n+/fdNPDzs8Rdqzr2y1ZZN/9ML5/R/+WLRwjlRoSy+9VHHO22D99Ytlzj3vgvSfUf9Jxw4blh+uT/mdj3UOP3JIWmxA//SjffZOH3zwQbryz1ele+69N0XKr7iOXH75z6Xvffe7uUV076ZtVc4j8803X/rHP25Lo8eMSUsNGpQ23WTjtN5666bH//3v9Ne/3pQefuSR1D2nkVp11VXS7t/brSndWOUcFfsyatRT6Y4778qtsF9OSyyxePrSWmulaDQxvXLz328ptv3Ms8/mXjx90ppf+ELRqru1lG+TJ09OV/3l6vSvfB34wujRaaF8PvvCGqvnB8zb5TRxU7oiR87qP191VbrvvvuLfYog/uo5iP+Nr3+tKR1Wpe7h9Ujev/vuvz+9+eabaaWVVkrb5pRqgwcPLlqR33b77enZXLdevXoXx+Gr224zvV3yPgECBAiUQGDUqFHpinw+fe6554pxqiJd4je/8fUcH/hys9pN674wGjBdc+11xfIjRp5YnP8iddWwoUOKeZX7zGjk9KN990ubb7ZpqneeiPNtn0UWSd/f/XtFfGda5/lmlTNBgEC7CnS4gHJrOs8+93zRdb4zBJPDYOIHE4sf12OOG54WXnjhfNH/1XxTMr4I9g4ZOiyNHDG8qVvohAkT0ttvv91EF6+PGjI0vZ9ThEQQuX+/fsXNT3Q5fe+999JWW27RtGzlRdxInH/hRUW6kX1/vI9gcgWmg/yNi4FHH3ssnXLa6fnG/YS0wAIt8ylXdmXC2xOKm/rK9Kf5vkRQYOiwY9Prr79WtDr7LMHkqMcb+aY1bvhry6RJHxb/P6h+EB6BgnPOO78IMEdqnAgKRHlnwjs59/rf83f83bTZZpul1VZZJbd865/iIck/brstp9HZtNnHX3X11cWDGcHkZiwmCBCYDQTKcA0R1xW/uPiStN23v10Ek+Na5bDDj0jvvPNuWik/+Izg5w033pjz6K9bBF63yzefe++1Zzrx5JOLG9DI+x+B0Hjw9/TTzxRB5sVyIDTGjLjgwl8U54z4Xd9xh+3SAQcdnM49//ziYWMcvot+cUl69dVX02GHHlIczahHpNzYYvPNc5B5QHo8jwsQ6dWGjxiRTjh+eFO6qDiPXHvd9cU6W2y+WVp//fWKMT0iHdtHOXB74UW/SGuu+YW08047poceeqio9+tvvJEOPeTgYp34J85RUb933pmQNtl446KRRJyf4yb8lVdeSd/ddZemZWtfxIPhGAA3HhJvlYPqMWBfBNjHjB2b9svpzWrTWoXxqaefkSI/9Ub5wepXcsB6TA6CX3f99cU60R05ljntjCnLbJID4xHUfvqZZ/N+XpeeyX8jJVUl8Bx1j4e4EWQI2zjX35TzXo/MXt/4+tfT7664otinddZeO936j38Ugf5o4R5jeCgECBAgUF6BGLsgegFFw6Mdtt8+n18/yvdHtxfny57z90yrr75aUfnp3Reuv956aWBuqHbOuecV54lVVl4pzT3P3E07XrnPjPPVGvkzr83B5zhHxLmiUkbn83807Imxedpynq+s5y8BAu0vMFsElJ/K+fUiIPQ/3/pm+wvO4i0O6D8gHXzQAU03EZtsvFFuwfOzouVIbYCsUtWLf/mr4iZg+LHHFC1VYn4MdrNKDrBFS5vaEjcbPz/r7HTvvf9KEUxeY/XVaxcxXXKBOGnHzeaBBx+S8ymfloYedUTTd2Z6VW/0+xIXGkOOHlY8xBg2dGjq06fPNDcRDzGilVdtmXeeeZoeitS+N73pCEycd87ZTa3RKsvH/EN/enBa/nNTgswxP27+40l69f9f4qLq0UcfSz/58Y8qq/pLgACB2U5gVl5DjB//StECaostNi9cTz71tOLvaaeclKIFcJTx48fn89ZPi9fxT+RinHfe+XKr5jFp0KAlc4vYW3JL31FpaB4jIHpaRYlBmiMoHA8Lv7TWl3LvmPnz+W/fHBw+obhWjIGG/3nHHbmn1QFpgdyDJ8qOeQDiCORW0oPFZ8TD9ksvuzynVBuX+i26aLFc/BNB1WOOHtI0UN6Wuf4/3OfHRTA5gsw77bhDsWwEfaNFVbQOjsDrPPmcVinRM2zE8GNzT5l+xaxo3Tx4mWXSJb/6dVH/6nNUZZ2XckvmCCZ/b7ddm1qLRfq3uCaLc+49+RqtOh1crHdrbkUdweQD998vrZxv6ivlC2uskSbkgHaUyjLhUenBFNeEa35hjaJnz99uuikH2jerrPrJ/g9Nc+fxD6LEdedP9j8wXf6b3zbbTrTaPnLI0cWDXAHlJj4vCBAgUEqB6I1z4gnHN7tvi9/36Pl5S35AWAkoT+++MHrOLLDAlHNr9HSpzaFcvfNf2WqromdL9KSuPn/Ffdkiiyxc9CyNwXqnf57/9L1gq+vjNQECjQtMfRTU+LqlWOOll14qbhKiK3t0be9sJVqSVLdIiS4l0XJk1KinW6V4LAfKNt1kk6ZgcmXBtXNKgTgJVJd4OnnSKacWweR99t5LMLkap4O9jtQX++YAaXRjuuL3f2hz7Rv5vrzxxpvpoHzzH12GI5hc+32qt9G4Of/Z4Ue2+C8uWD5tiRvnStfm6s+IHgyfW2656lnF70YEkKOrcqVcn1vFhVfk7VQIECAwuwrMymuI555/vjhHxDXMpEmTUjQOiBQTlWBymMcDydpg5OKLD0yxbpTHHn88B5YH5W6xfYrgdKRaiv+i5XCUSHURJXqqxDVitAw+6+xzi55YleBpvB+/9xFMjgfokcYhWhUvO3hwvFW0Gi5efPJPpBRbfPHFq2flFBJrFNPRK6a6RDqKKM/m8251iRvlSjC5Mj9aB8d56/HHp56LKu/F3yf+/UTRUjhSY1T2M/5GSpBIUfF4tqgt0Vo70mlUB5NjmaWWGpRWzqkqolSWqfaI+Z/73HJFb7R4v7pEupFKMDnmxyCJkUYjBtit3c4X8wPbCJ7H8VUIECBAoNwClUZAcW6J82D0EI1xbuK+rlIauS+srNPa37hPjBjO1ddc07RIDNQb6aC23WZKuqS2nuebPsALAgTaVaBDt1COvHNHDT26uOE4ILe+qA6stqviLNzYwHxjVVviRqfS8qT2vfiRfje3CB205JK1b9WdHnHCiU2tR598clT6Ys5VrXRcgRU+//nipjryak/riXFlDxv5vsSgStFdOb5fUcbmLrhtCSjHTejw3FKrtvTIwd/plcgNWa9Ubu5r34t8lrW/E5EvOgIEYfL55ZcvbnyjC2/0eKhdtvbzTBMgQKAjC8zKa4hIvbBY/u2N8sILo4u/9QZojVZRV19zbfF+/BPjaLz44ovFdOTqjQeCe+y5V9P71S8iFUalV9XXv/bV4nc+3o/0DNXl9ddfzymhzijyOUf32uoyuWY6ArS1Zckll8hNfacEwKvfi+B3lDiXVpcVPl9/LIOBAxfP6SaeqV606XWkoYi67bHnD5vmVb+odz6MlBUrrbhi9WItXk9rmei1dtfd9zRbp+7+5/Pom2+92Wy5mIjza5RIWRUpShQCBAgQKK9ApFW6Lqd1qtzLVWq66Ce9dBq5L6ysO72/8bD3xJNPKe4b4+FopCeMBkDrrbtOsWoj5/npbcv7BAjMeIEOe3UX3SCPzHmAe/deMB11xM/qtkac8Vzl+8RuXbs2VKl55523+JEem2/G2hIajlQER/zs0Jxj+dFiULfll1+uqSVOQxu2cGkEIlD6SG6lfnJOffHt6aSJaeT7Eje6PXp0T6efekqRj/GMM8/MubyPL3J8T2vnu+WLht69ek1rkTxgXo9i4KLahcaMGVs7q5iepypXV/UCEbyuV7bdduui1Vq0pIon4ZMnf5RzVG5Yb1HzCBAgMNsIzMpriGgV/OYnrWp7fzLw3WuvvdashXJA1/7OR5qkSuveCEgvtNDCOUfxQXWPSXVOxl/mdBKVcvEll6Q9/2+PymQRTH4rB0QPymkfomVyBD8jCPqD/2sZqK43+N0c+ZMqeYabPnQaL578z5SW07WLRK+7yk107XtLLDEwdb2jS5HOqd7DznrzYpyAMWPH1H5Us+lpLTN27Iu5BfSUtByVlertf8oAAsYVIX8JECDQ8QQiZ3GkVfraV7fNaZU2aOrJHOfORx+b0gOmkfvCtgqstNKKRe/qa3Ig+wd5AL4YFyBSJlXOKY2c59u6TcsRIDDjBDpkyotXc9DnyKOGFgOLDTny8KKb4owjmf0/KXLz3XLrrcUAfNV7G61UIs9fdYmcejFydwzqFt0fz8y5lCOYr3RcgbjpPCCPMB/lspzzcHqlke/LMUcPLS4KDtjvJ2nOHnOmGN13RnR1XWqppfKASQ/mQO/UlmORjqUyivD09mF670fL+wg2x0VMtFRef731O+1DqulZeZ8Agc4t0Mg5YVrXEEvmlr4v5oBllHioGL/Bt9z6jxa4N918czHv48kfF3+fy4MwL7po3+J1tL595pmn8wPHccXNZ9yAxn8R9Ix8/pWA8j333lvkCt7vJ3ksgQP2K7rT3v7PO5q2NXr0Cznf8lpFL5XKTexjn9xANy00A19E4DjqV10efviRFHn+o6dMvRLz48HtnXfd3Wxfo76RpqNeoDd8IpVIDHBUXSJwH3WI0toy8f4TTz6RVlyhfmvq6s/zmgABAgQ6tkAlNVMElCONUZRIAxU5jKtLW64Bunad0mbx7QnNz3PVn1N5HfelkUv5zjvvTLflwXDjPLjllltU3i7OUW05zzet4AUBAu0q0OECynERvP8BBxVdMXbaccdilOpRTz2VKv/FqN3KtAV23mmHInB81NBh6Y477ixG8Y5BY2JQl+pupfEpgwYtmf9NRdf/GKBs7rnnmWFBwuKD/TNLBBZYYIFikL62bLyt35e4+Kjkvoy/hxx8UBo3bny66OJL2rKZaS6zdr7RLwZCOm548Z29//4Hiu9hzJsRJYIOW+W8kDfc+NeizttsvdWM+FifQYAAgdlOoK3nhNjxQYOWzP/Wv4aI9A7RrTbSI0XZNQ+KFzeuMRDe88+/kJ56+umi50gl8Hr3PfcUv/8xOF0l6BoD38XnRPqzeCAYD8YfePDBPD0sDR12TPG5kfvx7HPOLVo8rbbqqkXu4LhZvfCii5qCqksttXS65ZZbUwR1I/3FXXffnc47/4Ji/Zn1TwxYd3u+eY79jAeZ0eU38hjX5iGubD+6Am++2aY5D/RFxQB4/37iiRT/nXfBhWm/fF0c+S6jxHXc4UccVTzMjVZmkaJiyNHHFOe3Z599LkUgPQZvPiubRAnDyjJ//dvfUiwTaZ+G5nX69OlbbLNY0D8ECBAgMNsKRC7jKJdd/pviXijOBZXzRPVOt+UaIMYDiIFyo+FPDKgX55bo9dNa2fDLXy7eivPbqqus3KznalvO8619rvkECMx8gSmPj2b+dmbYFqpbr5ycB4urLRusv376/u671c7uVNMRHKtuyRk736VLdMicUiIPUgyYdulll6WLf/nLYnCXGMgv8gtGS+TWSoxQ/tPcrTRuVC6+5JfZ+XutLWp+BxCIG9cYXOfa3MWouqtsvO5SlUrl035fBg1aMn03Bwjiu7Jy7s4Urb/qlervZr33Y17k0Nzj+7un3//xj+mc884v0rZEDui9f7hX0Wq+tfWq51fvY/X8yuvoXhVdvWJ/K4NSVN7zlwABAp1FoD2vITbaaMN0+s/PSscfd0yKgYFze6h01V+uKYKfkUMxBtM7eshRRaD5d1dcUTzU3nuvPZsGhevRo0c6/LCfpl9fenkOKN9Q3AhH6ollll4mzz+0OGQjTzo5jxbfJ0UjhErZ/n+/nWJgoehFc/KJI9OP9v5hOuPMs4qgbiwT54HdvrtrOvPsc5paOcf86Z1HYpl6pdJSuvLeXnvukaJ7cfQSitZYC+aUH5ttumnacYftm22vsnzl78477VgMghetuK67/oZidtT1kIMObLoBj9zUY18cWzyEjcHzwuHXl16Wb+yvTZfmgXPjRn+lPCDfD3bfvVh/iuGh6Ve/viynNrs6vfXWW8XD4RhzYNddvtPmXoBdu7RMwdYlHwuFAAECBMovEIO17vqdnYuB2+PhbpyDY/DWODc9+thjTTvQ1vvCHXfcPl2az83Djh1efFb0eI68+rX3mfHBcV6K3qHRgzpyKleXtpznq5f3mgCB9hWYI3dlmNKHMG933LhxeRCtKd0I27catjYrBSIlQaWL56ysh213DIFZ/X2J7UfX3k97Y9+acuTpjEEFo4t27Wj3ra1jPgECBDq7wGc5J0ycODH9ZP8D0+qrrZYfQH6n6Vqk3u98W7bTlmWmdbzikjjSKc2sa6L4/F132z3ts/deTYMcf9o6R/qL/Py3bgA63quX07kt22rLMtMy9B4BAgQIdGyB6AEaAeW2lOmdMxr5rBmxvbZ8hmUIfFaB9oqbRqrZsjd003Tgs36bZoP1Z9aN02xAYxfqCMzq70tsf0YFk2/++y0pBp6MVDmnnXFG0T1LMLnOQTeLAAECrQh8lnNCtDw64vDD0tPPPFMElv91333pzdxCtvI7H11kIy1E/Ea3ZTttWaaV3Shmx7nls37GtD6/3nufdnsRMK5t+Vz5/HrB5HivLdtqyzKV7fhLgAABArOfQFuDybHn0ztnNPJZbZGc3vba8hmWIUBgxgl0uJQXM27XfRIBAp1d4M477ypScoRDpH056ID9OzuJ/SdAgEC7CvTLKRuOO+bodONf/5a72v4xD/w7LgdKu6bu+eFh5FiO7rV98yB8Cy+8cLvWy8YIECBAgAABAgQIEGhdQMqL1m28Q4BAJxCIfJETc9euhRZccIa1fO4EbHaRAAECM0Ug0kK88sorRQ7gGOx1rrnmminbmVUfGoPnzTfvvG3uTjyr6mm7BAgQIECAAAECLQWkvJhqooXyVAuvCBDohAI9e/bshHttlwkQIFBOgUg7UfZ8cZ9FrnevXp9ldesSIECAAAECBAgQKIWAHMqlOAwqQYAAAQIECBAgQIAAAQIECBAgQIAAgfILCCiX/xipIQECBAgQIECAAAECBAgQIECAAAECBEohIKBcisOgEgQIECBAgAABAgQIECBAgAABAgQIECi/gIBy+Y+RGhIgQIAAAQIECBAgQIAAAQIECBAgQKAUAgLKpTgMKkGAAAECBAgQIECAAAECBAgQIECAAIHyCwgol/8YqSEBAgQIECBAgAABAgQIECBAgAABAgRKISCgXIrDoBIECBAgQIAAAQIECBAgQIAAAQIECBAov4CAcvmPkRoSIECAAAECBAgQIECAAAECBAgQIECgFAICyqU4DCpBgAABAgQIECBAgAABAgQIECBAgACB8gsIKJf/GKkhAQIECBAgQIAAAQIECBAgQIAAAQIESiEgoFyKw6ASBAgQIECAAAECBAgQIECAAAECBAgQKL+AgHL5j5EaEiBAgAABAgQIECBAgAABAgQIECBAoBQCAsqlOAwqQYAAAQIECBAgQIAAAQIECBAgQIAAgfILCCiX/xipIQECBAgQIECAAAECBAgQIECAAAECBEohIKBcisOgEgQIECBAgAABAgQIECBAgAABAgQIECi/gIBy+Y+RGhIgQIAAAQIECBAgQIAAAQIECBAgQKAUAgLKpTgMKkGAAAECBAgQIECAAAECBAgQIECAAIHyCwgol/8YqSEBAgQIECBAgAABAgQIECBAgAABAgRKISCgXIrDoBIECBAgQIAAAQIECBAgQIAAAQIECBAov4CAcvmPkRoSIECAAAECBAgQIECAAAECBAgQIECgFAICyqU4DCpBgAABAgQIECBAgAABAgQIECBAgACB8gsIKJf/GKkhAQIECBAgQIAAAQIECBAgQIAAAQIESiEgoFyKw6ASBAgQIECAAAECBAgQIECAAAECBAgQKL+AgHL5j5EaEiBAgAABAgQIECBAgAABAgQIECBAoBQCAsqlOAwqQYAAAQIECBAgQIAAAQIECBAgQIAAgfILCCiX/xipIQECBAgQIECAAAECBAgQIECAAAECBEoh0K22FuPGjaudZZoAAQIECBAgQIAAAQIECBAgQIAAAQIECKRmAeW+ffsiIUCAAAECBAgQIECAAAECBAgQIECAAAECdQWkvKjLYiYBAgQIECBAgAABAgQIECBAgAABAgQI1AoIKNeKmCZAgAABAgQIECBAgAABAgQIECBAgACBugICynVZzCRAgAABAgQIECBAgAABAgQIECBAgACBWgEB5VoR0wQIECBAgAABAgQIECBAgAABAgQIECBQV0BAuS6LmQQIECBAgAABAgQIECBAgAABAgQIECBQKyCgXCtimgABAgQIECBAgAABAgQIECBAgAABAgTqCggo12UxkwABAgQIECBAgAABAgQIECBAgAABAgRqBQSUa0VMEyBAgAABAgQIECBAgAABAgQIECBAgEBdAQHluixmEiBAgAABAgQIECBAgAABAgQIECBAgECtgIByrYhpAgQIECBAgAABAgQIECBAgAABAgQIEKgrIKBcl8VMAgQIECBAgAABAgQIECBAgAABAgQIEKgVEFCuFTFNgAABAgQIECBAgAABAgQIECBAgAABAnUFBJTrsphJgAABAgQIECBAgAABAgQIECBAgAABArUCAsq1IqYJECBAgAABAgQIECBAgAABAgQIECBAoK6AgHJdFjMJECBAgAABAgQIECBAgAABAgQIECBAoFZAQLlWxDQBAgQIECBAgAABAgQIECBAgAABAgQI1BUQUK7LYiYBAgQIECBAgAABAgQIECBAgAABAgQI1AoIKNeKmCZAgAABAgQIECBAgAABAgQIECBAgACBugICynVZzCRAgAABAgQIECBAgAABAgQIECBAgACBWgEB5VoR0wQIECBAgAABAgQIECBAgAABAgQIECBQV0BAuS6LmQQIECBAgAABAgQIECBAgAABAgQIECBQKyCgXCtimgABAgQIECBAgAABAgQIECBAgAABAgTqCggo12UxkwABAgQIECBAgAABAgQIECBAgAABAgRqBbqNHz++dp5pAgQIECBAgAABAgQIECBAgAABAgQIECDQQmCOj3NpMdcMAgQIECBAgAABAgQIECBAgAABAgQIECBQIyDlRQ2ISQIECBAgQIAAAQIECBAgQIAAAQIECBCoLyCgXN/FXAIECBAgQIAAAQIECBAgQIAAAQIECBCoERBQrgExSYAAAQIECBAgQIAAAQIECBAgQIAAAQL1BQSU67uYS4AAAQIECBAgQIAAAQIECBAgQIAAAQI1AgLKNSAmCRAgQIAAAQIECBAgQIAAAQIECBAgQKC+gIByfRdzCRAgQIAAAQIECBAgQIAAAQIECBAgQKBGQEC5BsQkAQIECBAgQIAAAQIECBAgQIAAAQIECNQXEFCu72IuAQIECBAgQIAAAQIECBAgQIAAAQIECNQICCjXgJgkQIAAAQIECBAgQIAAAQIECBAgQIAAgfoCAsr1XcwlQIAAAQIECBAgQIAAAQIECBAgQIAAgRoBAeUaEJMECBAgQIAAAQIECBAgQIAAAQIECBAgUF/g/wGLq+d8Z8dt8gAAAABJRU5ErkJggg==)

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
