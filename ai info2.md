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
