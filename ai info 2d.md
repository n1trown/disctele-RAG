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

[Source code](../LM%20Data/_blank)

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

Check update on [EOS Block Explorer](https://eosauthority.com/account/company?network=localtest&endpoint=http:%2F%2F127.0.0.1:8888&token_symbol=EOS&scope=company&table=employees&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables) 