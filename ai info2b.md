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
