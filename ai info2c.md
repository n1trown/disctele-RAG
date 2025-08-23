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