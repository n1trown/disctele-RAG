_UPDATE July 29, 2025 → FYI This is an older document that I (Will) wrote up in late 2024. I’ve scanned through this now and updated it with some modern lingo. I’d recommend starting with the whitepaper and other docs in_ [_this gFolder_](https://drive.google.com/drive/folders/1JjAVePbcWC5Otcxj_jRvhQalKH6-D_VM?dmr=1&ec=wgc-drive-globalnav-goto)_._

_The purpose of this document is to provide - from_ [_Will_](https://www.linkedin.com/in/wclittle/)_’s perspective - a FAQ for his friends who are potential Wire Network investors, node buyers, and/or associated tech diligence partners_

_This FAQ assumes you have a decent level of blockchain/Web3 knowledge already. If you don’t know any of these terms, you should have your favorite LLM and/or search engine ready to assist you :)_

_Some answers are in Will’s own language - and some are assisted by LLMs based on feeding ‘em docs, transcripts from interviews with the founders, etc…_

Below we explore the key features and benefits of the Wire Network, a Layer-1 blockchain designed specifically for high-volume dApps (e.g. for the AI agent economy, next-gen Defi and Web3 gaming, etc..). Wire boasts groundbreaking capabilities such as 10k+ transactions per second, universal interoperability without bridges, optional gas fees, and advanced security mechanisms.

We discuss Wire's novel governance structure, tiered node systems, and technological innovations like the Universal Transaction Layer (UTL) and Wire Name Service (WNS), which eliminate the need for traditional bridges and facilitate cross-chain asset management.

Finally, we address technical specifics, explaining how the architecture ensures scalability, affordability, and future-proofing for decentralized applications and AI-driven use cases.

​

- In a nutshell, what is Wire Network?
  - It’s a new L1 built for next-gen dApps that require fast, free, and secure transactions between assets from any blockchain ecosystem. It has 10k+ TPS, is able to secure, trade, and manage assets from all chains, and has no gas fees for node owners (Tiers 1, 2, & 3).
- Why is Will excited about it
  - The future of blockspace - globally speaking - will inevitably be filled by global-scale dApps that compete with Venmo, Robinhood, Coinbase, etc...
    - This includes a massive amount of blockspace purchased by AI agents, likely as a part of these high-volume dApps
  - It has now become obvious that Web3 is better optimized for AI UX than for human UX…
    - i.e. Blockchains are better for AI agents than for humans.
  - Ethereum is too slow/expensive, EVM L2/L3s (and other chains) are not interoperable enough to be deeply useful for AI agents. Even the small gas fees on L2s/L3s and other chains will be prohibitive for the massive amount of transactions that good/robust/helpful AI agents will need.
  - It’s a game changer that users (humans and/or agents) can participate on Wire without worrying about the need for any tokens to pay for gas. This is always a pain when onboarding into a new chain.
- Where can I find the latest version of Wire’s whitepaper
  - <https://github.com/Wire-Network/documentation/tree/master/Whitepaper>
- Where can I find the latest developer documentation?
  - <https://docs.wire.network/>
  - <https://github.com/Wire-Network/documentation>
- Is the Wire Network code open-sourced?
  - Yes, follow the directory tree to all the various repos from the README here → <https://github.com/Wire-Network/documentation>
- What is a node?
  - This takes a minute to understand if you are new to the concept, so let’s walk through it:
  - It’s important to first understand the _roles_ in Wire Network. There are:
    - Node **_owners_** (the people governing T1s/T2s/T3s/T4s)
    - Node **_operators_** (the people running the machines securing the L1, aka the block producers)
    - **_Council members_** (the people voted in by the T1 node owners)
    - **_Batch operators_** (the people running the machines that handle the bulk withdrawal system into native chains)
  - A “Node”, then, is a T1, T2, T3, or T4 - as described in section 3.3 of [the whitepaper](https://github.com/Wire-Network/documentation/blob/master/Whitepaper). Each node tier has different roles, privileges, and compensation.
- Where can I find more information about nodes and how to buy them?
  - <https://www.wire.foundation/>
- How were Wormhole, Axie Infinity’s Ronin Bridge, and Harmony’s Horizon Bridge hacked and how does Wire’s architecture prevent similar attacks from happening?
  - By bypassing key signature verifications, stealing private keys, and attacking a multi-signature wallet setup requiring only 2 out of 5 keys to authorize transactions, respectively.
  - Assuming you’ve read [the whitepaper](https://github.com/Wire-Network/documentation/tree/master/Whitepaper), to quickly recap → Wire’s architecture entails smart contracts on both the native chain and Wire’s L1 to lock and record/transfer ownership of the asset (these are the “Wire Name Service” contracts, i.e. the bucket contract on the native side, and the settle.wns contracts on the Wire L1 side). These contracts are setup by node owners and the governance council, not a small number of people/addresses.
    - NOTE from Kyle: “The external contracts are Immutable once deployed and similar to say uniswap v2 contracts. Even though there is v3 and v4, contracts users can reject these and use the Immutable v2 contracts.”
  - Therefore, there is simply no attack vector possible for hackers to bypass key signature verifications, steal private keys, access smart contracts, attack a multi-sig, print more ERC20s, etc..
  - More convo from ChatGPT on this:
  
  
  - Kyle’s additional commentary:
    - “major ones are separation of powers in the traditional validator model, no native tokens on Wire so consensus is layered with the external chain for finality around ownership, Internet sized scalability is built into the protocol (Network Expansion), Polymorphic blocks meaning wires node operators can evaluate many different signature schemes and formats.”
- Hmmm, regarding the (now old lingo) that Wire is the **_only_** blockchain built for the AI agent Economy? Is that just marketing lingo?
  - This isn’t just a marketing ploy - the gasless, cross-chain, and 10k+TPS setup is unique in the market landscape and perfect for AI agents. Plus, the C++/WASM smart contract architecture makes it relatively easy (and extremely robust) for devs to build complex agents on top of it.
  - Kyle:
    - “Additionally proof of inference is much easier to enforce with Wire’s form factor since there are two steps to finality and the possibility of structuring a rule set around this where there is plenty of time to verifiably slash a bad actor such as a rouge LLM compute provider”
- How does identity (UPAP) _functionally_ work on Wire’s L1 and onramp/offramp chains?
  - To get into the core Wire L1, you don’t need a 24-word mnemonic phrase. You just need an email / username / password. If you want to offramp to another chain, however, you will need to write down your words. Obviously if you are on-ramping into Wire then you already have a wallet with a mnemonic phrase written down.
- What features of the wallet will be unique vs. other wallets?
  - The AI-integration (agent marketplace and a custom wallet agent to guide UX)
  - The social features
  - The integration with a cross-chain DEX (NoGas.com)
  - Zero gas fees and the other key Wire Network talking points (above)
- _Interoperability_ - how on earth does this really work? Is it real?
  - Yes, it’s real. Bucket contracts get deployed on chains and interact with the settle.wns contracts on the Wire side.
  - These bucket contracts will need to be manually installed on the native chains, of course. But once they are set up, they are set up forever.
- How will bucket contracts work with chains that don’t have robust smart contract architectures, like Bitcoin?
  - _Bucket contracts on Wire Network can work with chains that lack robust smart contract architectures, like Bitcoin, by employing the following mechanisms:_

1. **_Message-Based Transactions:_**
    - _Chains like Bitcoin operate on a messaging system rather than executing complex state changes. Wire Network can adapt by creating_ **_bucket contracts_** _on Bitcoin's UTXO (Unspent Transaction Output) model, where transactions are validated based on inputs and outputs without native smart contracts._
2. **_Layered Consensus and Off-Chain Verification:_**
    - _Wire Network utilizes_ **_layered consensus_**_. For Bitcoin, bucket contracts can rely on transaction proofs directly from Bitcoin's blockchain. These proofs are recorded on Wire’s Universal Transaction Layer (UTL), ensuring that ownership and state transitions are provable without altering Bitcoin's architecture._
3. **_Intermediary Systems (Bridge-like but Secure):_**
    - _A lightweight bridge or intermediary service can be implemented to facilitate interaction between Bitcoin and Wire’s UTL. Unlike traditional bridges, Wire’s system doesn’t require full custody of assets, as it relies on_ **_proof of state ownership_** _provided by Bitcoin’s transaction logs._
4. **_Bucket Contract Emulation:_**
    - _While Bitcoin lacks the infrastructure for deploying bucket contracts natively, Wire can emulate bucket behavior through external validators or_ **_sidechain implementations_**_. For instance:_
        - **_RSK (Rootstock)_** _or_ **_Stacks_** _can serve as intermediaries, enabling smart contract functionality while maintaining security via Bitcoin's consensus mechanism._
        - _The bucket contract logic would then operate on the interoperable layer, linked back to Bitcoin._
5. **_Manual State Management:_**
    - _For chains like Bitcoin, user transactions can be tracked via_ **_deterministic systems_** _in Wire’s UTL. Ownership and transfer rules are enforced within Wire’s network, while Bitcoin’s role remains as the immutable ledger for asset custody._
6. **_Future Enhancements:_**
    - _Wire’s extensible architecture supports additional cryptographic formats and transaction proof systems. For example, with integration of cryptographic signatures or Merkle proof verifications, transactions on non-smart-contract chains like Bitcoin can still align with Wire’s UTL standards._

_This approach ensures seamless and secure interoperability between Wire Network and Bitcoin, without compromising Bitcoin's foundational architecture or Wire's trustless design._

- Let’s do a step-by-step how this bucket contract emulation will work with Bitcoin

1\. Locking Bitcoin on Its Blockchain

- **What Happens**: A special Bitcoin address or script (like a multisig or P2SH contract) is created. When you send Bitcoin to this address, it effectively locks the funds so they can’t be moved without satisfying specific conditions.
- **Purpose**: This ensures the Bitcoin remains on its original blockchain and can be unlocked later only by the rightful owner.

2\. Creating a "Digital Receipt" on Wire

- **What Happens**: When you lock Bitcoin, Wire's system creates a **cryptographic representation** (let’s call it a "receipt") of your locked Bitcoin. This receipt is recorded in Wire’s Universal Transaction Layer (UTL).
- **Details**: This receipt isn’t a copy of your Bitcoin; instead, it’s like a proof of deposit. It contains:
  - The amount of Bitcoin you locked.
  - The unique transaction ID on the Bitcoin blockchain.
  - Your ownership details.

3\. Transacting the Receipt on Wire

- **What Happens**: Instead of moving actual Bitcoin around (slow and expensive), Wire lets you transact the receipt within its fast and low-cost ecosystem. Every transaction involving the receipt is recorded on Wire's UTL.
- **Layered Consensus**: Wire’s consensus checks every step to ensure:
  - The receipt matches a valid Bitcoin lock transaction.
  - Ownership and rules are respected on both Bitcoin and Wire.

4\. Verifying with Bitcoin

- **What Happens**: Wire uses cryptographic proofs to check that the Bitcoin you locked is still secure. This is done periodically or when someone requests a transaction involving that Bitcoin.
- **Example**: If someone buys your receipt, Wire’s validators confirm:
  - The Bitcoin is still locked in the original address on Bitcoin.
  - No double-spending or tampering has occurred.

5\. Redeeming the Bitcoin

- **What Happens**: If you or someone else holding the receipt wants to withdraw the Bitcoin:
  - The receipt is sent to Wire’s settlement layer.
  - Wire generates the necessary transaction to unlock the Bitcoin on the original Bitcoin blockchain.
  - The Bitcoin is released back to the wallet specified by the receipt holder.

Key Technical Components

- **Bitcoin Script**: Used for locking funds securely on Bitcoin.
- **Wire Name Service (WNS)**: Wire’s system of bucket contracts to track ownership of the locked Bitcoin and manage transactions.
- **Cryptographic Proofs**: Wire generates and validates proofs to ensure locked assets remain secure and legitimate.
- **Layered Consensus**:
  - Bitcoin handles security and ownership at the native chain level.
  - Wire manages fast transaction handling and receipt updates in its ecosystem.

Why It Works

- **Bitcoin’s Security**: The Bitcoin network guarantees your funds are secure because they stay on the Bitcoin blockchain.
- **Wire’s Speed**: Wire’s UTL provides a way to trade ownership efficiently without interacting with Bitcoin’s slow confirmation times for every transaction.
- **Trustless Design**: No one, including Wire, can move your Bitcoin without your consent. It’s all based on cryptographic proofs and blockchain rules.
- _Speed & Throughput_ - how the heck can Wire’s L1 get to 10k+ TPS?
  - Following the EOS architecture, there are only 21 block producers at initial launch
  - Wire's infrastructure focuses heavily on horizontal scalability through the parallel processing of transactions, which allows multiple validators to handle transactions simultaneously. This reduces congestion and improves throughput across the network.
  - Via compression, Wire reduces transaction sizes and limits on-chain data to only essential information, minimizing the burden on the network and speeding up transaction validation.
  - Leveraging a UXTO model and having no gas fees to worry about for whitelisted contracts, the blockchain can zing quickly.
- How big are the block sizes on Wire?
  - Like EOS, block sizes are dynamic (i.e. not fixed) and optimized based on resources (RAM/CPU/NET) available and the types of transactions that need to be processed.
- Are we worried at all about saying “No Gas” when a zero-fee experience only applies to white-listed smart-contracts by node owners?
  - The architecture of Wire quite literally doesn’t use gas and tokens to pay for that gas, so saying “no gas” isn’t wrong - it’s technically accurate. Wire has a fundamentally different architecture.
  - While yes, there is a transaction fee (paid in $WIRE) for users that interact with Wire outside of the whitelisting process from a node, this is hyper-technically not a “gas fee”.
  - Plus, the idea here is that most dApps will be node owners so their users literally won’t have to worry about any kind of transaction fee whatsoever (unless the dApp itself charges one, which is certainly possible).
- How is Wire more “secure” than other blockchains?
  - Security is obviously a complex topic, but a key design decision for wire is to separate the node owners from the council from the node operators.
    - Wire Network is more secure than other blockchains due to several foundational advantages:
      - No Custody at Network Level: Wire never takes custody of assets at a network level, unlike bridges or centralized systems. Assets remain under the native chain's consensus, ensuring external validations are always required for ultimate ownership
      - Layered Consensus and Decentralization: Wire employs a layered consensus model combining Appointed Proof of Stake (APoS) and Asynchronous Byzantine Fault Tolerance (aBFT). This enhances decentralization by separating validator roles and governance responsibilities, reducing centralization risks​
      - Abstract Ownership: Instead of bridging or transferring assets, Wire uses a system of abstracted ownership where assets stay on their native chain. Transactions in Wire are merely proofs or representations of ownership, minimizing risks associated with traditional bridge exploits​.
      - Quantum-Resistant (as much as possible) Design: Wire is structured to evolve with advancements in cryptography, ensuring future-proof security - as best as possible - against emerging threats like quantum
      - Transparent and Open Infrastructure: The network relies on trustless, open-source hardware and software, reducing the vulnerabilities tied to proprietary systems​
    - These features collectively establish Wire as a secure and resilient blockchain platform, addressing vulnerabilities that have plagued other networks.
- How do we know these bucket contracts and settle.wns contracts aren’t going to get hacked like other bridge contracts get hacked?
  - Wire Network has implemented several innovative strategies to secure its bucket contracts and settlement contracts (settle.wns) against the types of vulnerabilities commonly exploited in bridge hacks. Here's how Wire avoids those pitfalls:
    - No Third-Party Consensus Mechanisms: Traditional bridges often introduce a third-party consensus mechanism that creates vulnerabilities. Wire does not rely on these mechanisms, removing an attack vector present in other interoperability.
    - Abstract Ownership and Asset Retention: Wire employs an abstract ownership model where assets remain on their original chains. This eliminates the risks associated with transferring custody of assets to a bridge or a centralized authority. When assets are locked in Wire's bucket contracts, they remain fully tied to their native chain, preserving the chain's original consensus mechanisms and avoiding weaknesse.
    - Extensive Auditing and Open Source Code: Wire's contracts are open source, allowing for community inspection and independent verification of their security. Additionally, Wire has completed audits with reputable firms like Halborn and plans to pursue continuous auditing to ensure robust security​
    - Separation of Powers: Wire employs a decentralized governance structure, separating node ownership from operation and relying on the consensus of the original chains for finality. This design limits any single point of failure that could be exploited by an attacker​
    - Built-In Redundancy and Validator Security: Wire's architecture avoids reliance on small groups of validators or multi-signature wallets, which were exploited in past bridge hacks like the Ronin and Harmony bridge incidents. Instead, ownership proofs and transaction finality depend on the original chain's consensus
    - Continuous Innovation Against New Threats: Wire Network's development includes strategies to remain quantum-computing resistant and integrate security updates as threats evolve​
  - By adhering to these principles, Wire Network minimizes the risks associated with bridge technologies and positions itself as a more secure alternative for cross-chain interoperability.
- Is Wire “Quantum-Computing” safe? how?

Yes, Wire is designed to be quantum-computing safe. Here's how:

1. **Layered Consensus for Provable Ownership:** Wire's architecture ensures that assets remain under the custody of their native blockchain. Even if Wire’s network were compromised by a quantum computing attack, ownership of assets could be externally verified and challenged at the smart contract level on the originating chain. This layered consensus approach significantly enhances security.
2. **Polymorphic Blocks:** Wire supports polymorphic blocks, allowing the network to adapt to different cryptographic algorithms, including quantum-resistant ones. This flexibility ensures that Wire can integrate future-proof algorithms, such as Falcon 512 or other post-quantum cryptographic methods, to secure transactions.
3. **Separation of Custody:** Wire’s architecture avoids custody of assets at the network level. For example, transactions within the Universal Transaction Layer (UTL) do not physically move assets off their native chain. Instead, ownership rights are transferred while assets remain protected by their original blockchain's consensus mechanism. This reduces the attack surface for quantum threats.

Kyle elaborated on this in an interview with Will:

_“If all Wire key pairs were factored out by a quantum computer because they use SHA-256 in the settlement contracts, the contract that maintains parity with the external chain requires native formatted signatures to the remote chain. For example, if the external chain uses Falcon 512 or some other algorithm, that will be required to transfer or sign meaningful transactions for that asset. Essentially, we ensure that the cryptographic safety of the external chain is inherited.”_​

Wire’s design choices ensure that it is both quantum-resistant today and ready to evolve as cryptographic standards advance

- - In a nutshell, from Kyle:
        - “Layered Consensus for provable ownership of assets is a highly secure way to protect assets.”
- What’s up with the ROA and SYS token - why is this system needed as part of the Wire architecture?
  - It’s an upgrade from the EOSIO system that better manages resources
  - The ROA (Resource Owners' Association) and SYS token in the Wire Network architecture are fundamental components designed to enhance resource management, decentralization, and scalability within the network. Here's why they are integral:
    - Resource Management Simplification (SYS Token):
      - The SYS token is a non-transferable system token that manages the network’s resources like CPU, NET, and RAM. Instead of requiring users to individually stake tokens or manage resources directly (like in the EOSIO model), the SYS token allocates resources through the ROA on behalf of the Node Owners. This abstraction simplifies user interactions with the network, making it more accessible and efficient​.
    - Gas-Free Transactions:
      - By leveraging the SYS token, Node Owners can whitelist smart contracts, covering transaction fees for end-users. This creates a "gas-free" experience, which is critical for onboarding users unfamiliar with blockchain concepts, especially for use cases involving high-frequency and low-cost transactions, such as AI agents​.
    - Decentralized Control and Incentivization (ROA):
      - The ROA acts as a proxy for Node Owners, holding and managing SYS tokens. It ensures that resources are distributed fairly and efficiently across the network, while providing a revenue stream to Node Owners. This model decentralizes control, prevents concentration of power, and promotes sustainability by tying resource allocation to network demand​.
    - Adaptability to Network Growth:
      - The ROA and SYS token mechanism allow the network to scale efficiently during Network Expansion Events. When usage exceeds thresholds, new nodes and resources are introduced into the network, ensuring it can handle increased demand without compromising performance​.
    - Security and Performance Enhancements:
      - Unlike traditional models, the SYS token and ROA avoid transferring custody of assets or creating new vulnerabilities through bridging mechanisms. This design minimizes attack vectors and enhances the security of transactions and resource utilization​.
    - Economic Model Efficiency:
      - By removing direct staking requirements for users and managing resources at the Node Owner level, the system avoids the complexities and inefficiencies of traditional resource models. This structure is particularly beneficial for enterprises and developers looking to deploy large-scale applications​
    - These innovations position Wire Network as a robust and future-proof platform tailored to the needs of decentralized AI applications and other high-performance blockchain use cases.
- Is WNS properly named? Seems like - from the name - it would be like DNS or ENS, but it’s fundamentally quite different, isn’t it?
  - Kyle:
    - “WNS is an expansion on what the authoritative records can represent and how they function with rules. It's similar to DNS in this way but its orientation aims at solving interoperability issues for tokenized assets in multiple formats and standards.”
  - ChatGPT
    - “The name "Wire Name Service" (WNS) can be misleading if one assumes it functions similarly to DNS or ENS, as its purpose and mechanism are fundamentally different. While DNS and ENS primarily resolve names to digital resources (like IP addresses or blockchain addresses), WNS introduces a system that focuses on enabling interoperability and abstract ownership across multiple blockchain ecosystems. It acts as a hub-and-spoke model, where assets maintain their original chain identity while facilitating seamless transactions through a universal settlement layer. This approach avoids the vulnerabilities of traditional bridging mechanisms and introduces a deterministic system for cross-chain interactions, making WNS less about naming and more about providing an infrastructure for decentralized, cross-chain asset management​”
- How does staking work in the Wire ecosystem?
  - In the Wire ecosystem, staking plays a crucial role in securing the network and facilitating its functionality. Here's an overview of how staking works in the Wire ecosystem, drawing from its architecture and governance structure:
    - Staking Mechanics
      - Node Tiers and Staking:
        - Tier-1 (T1) Nodes: These are the backbone of the network, requiring a significant stake of 7.5 million $WIRE tokens over a year. They oversee key operations like electing the Council and managing network governance. T1 Nodes are essential for network governance and resource allocation, receiving 4% of network resources​.
        - Tier-2 (T2) Nodes: These support the network, especially during governance activities, by endorsing Wire Improvement Proposals (WIPs). They require 1 million $WIRE tokens staked for two years.
        - Tier-3 (T3) Nodes: These nodes are designed for smaller-scale operators and require 100,000 $WIRE tokens staked for three years. T3 nodes provide access to fewer resources and are typically used for specific smart contract operations​.
      - Length of Compliance:
        - Staking in the Wire ecosystem is tied to the "length of compliance." Node operators maintain their ranking and rewards by consistently staying compliant with network standards, ensuring the reliability and security of the network. Falling out of compliance can lead to penalties, such as being replaced in the node roster​.
    - Governance and Decentralization
      - Separation of Roles: Unlike other blockchain models, Wire separates the roles of Node Owners (who stake tokens) and Node Operators (who manage the technical infrastructure). This division ensures decentralization and reduces risks of centralization seen in other proof-of-stake models.
      - Appointed Proof of Stake (APoS): This novel consensus mechanism allows Node Owners to elect a governing Council while delegating operations to Node Operators. This structure prevents concentration of power and promotes transparency and fairness​.
    - Resource Allocation and Rewards
      - Staking in Wire is not just about securing the network. Stakers receive rewards in $WIRE tokens, proportional to their stake and the role of their nodes. Rewards are tied to resource usage, and node owners can allocate resources for gas-free transactions, enhancing user experience.
    - Economic Incentives and Expansion
      - As the network grows and reaches capacity, new staking opportunities arise during "Network Expansion Events." These events allow the network to scale horizontally and introduce new nodes with increased resources​
  - By leveraging this innovative staking model, Wire balances scalability, security, and decentralization, positioning itself as a robust platform for the AI agent economy and beyond.
- How are node operators selected? (recruited?)
  - Node operators for Wire Network are primarily selected based on their ability to meet compliance requirements, which include running Wire's proprietary node software and registering their node on the network's initial contract, typically on the Ethereum mainnet. Once registered and operational, they accrue "length of compliance," which determines their standing within the node operator pool. This ensures a reliable and secure operation of the network. In the early phases, Wire actively recruits experienced validators, particularly from well-regarded blockchain communities such as EOSIO and Antelope, to ensure the initial pool of node operators is robust and experienced. Over time, compliance and potential contributions to the network, such as staking, may influence rankings within the operator pool
- How are weights issued to contributors?
  - Weights are issued to contributors on the Wire Network through a transparent and decentralized process. Contributors submit their work, such as code or other forms of contributions, along with an estimation of the time spent. These submissions are evaluated by others with existing weights, typically starting with Wire's core engineering team. This evaluation process ensures the accuracy and fairness of claimed contributions. Once approved, these records are written on-chain, creating a public and immutable ledger of contributions and weights. The system is inclusive of non-code contributions, which can also be submitted through similar workflows, ensuring recognition across diverse contribution types
    - TLDR
      - Based on pull requests - attach amount of time you spent on it - evaluated by other people with weights (will be Wire’s core engineering team to start…they will catch bad actors)
      - Possible that folks can do this outside of Code - but it would be done on Github to record it.
- How are council members given weights / comp?
  - Council members are given weights in Wire Network's governance system based on their participation in monthly council meetings and their voting activity on issues. The weights they accrue serve as a measure of their contributions and engagement in the network's decision-making processes. However, these weights do not translate to immediate monetary rewards; instead, council members are incentivized by the prospect of sustainable growth and rewards tied to the network's successful expansion, which typically coincides with the end of their term. Additionally, maintaining a minimum depth in the node operator pool is also part of their responsibilities​
    - TLDR
      - By attending meetings / monthly council meetings / and voting on issues
      - They are motivated to do things that lead to Network Expansion
      - They also have to maintain a minimum depth in the node operator depth (they need to do the community organizing – they have some control over the node reward pool)
- When a Network Expansion Event is triggered, do node owners automatically get a new node? Or is it an open first-come-first-served marketplace? Or something else?
  - When a Network Expansion Event is triggered on the Wire Network, node owners do not automatically receive new nodes. Instead, new nodes are sold in an open marketplace where interested buyers must stake Wire tokens to acquire them. This sale process is conducted on a first-come, first-served basis, with the costs for nodes remaining consistent across generations (e.g., a T1 node always requires staking 7.5 million Wire tokens). Existing node owners can use their Wire token holdings, if not sold, to acquire nodes in the next generation. The expansion aligns with resource scaling, ensuring increased network capacity and maintaining equitable resource allocation across participants
- In the whitepaper, regarding _“...This process allows users to sign transactions and access the Wire Network ecosystem using the wallet they already know and use, without any behavior change. “_ – does this mean they can literally use their metamask (for example) to operate with Wire and make Wire L1 transactions / signatures, see assets (at least EVM compatible ones), etc..?
  - Yes, Wire Network's design allows users to operate seamlessly with wallets they already use, such as MetaMask. Users can perform Wire L1 transactions, sign transactions, and view compatible assets, particularly EVM-based ones, without altering their existing behavior. This capability stems from Wire's Universal Transaction Layer (UTL), which abstracts asset ownership while maintaining them on their native chains, avoiding traditional bridging methods and associated risks​
    - Notes:
      - Even for assets that are not Ethereum assets
      - Polymorphic blocks
      - sig_em (Ethereum message) - tells the node software operator how to handle the sig
- Technically how does a sign transaction happen?
  - A signed transaction on the Wire Network begins when a user creates a transaction using their private key. This process generates a cryptographic signature that ensures the transaction's authenticity and integrity. The Wire Network then validates the signature against the user's public key, ensuring the transaction was authorized by the owner. The system operates through a Universal Transaction Layer (UTL), enabling cross-chain interactions without asset custody changes. Transactions involve "bucket contracts" on the source chain and settlement contracts on Wire, maintaining the native chain's consensus and security protocols. This architecture allows for fast, secure, and gasless interactions across multiple blockchain networks​
  - Notes:
    - The dApp or the wallet has to support WNS for it to work
      - Add the Wire.js module in your dApp, people can use their wallet that interact with contracts
- How does Wire improve the onboarding process compared to other blockchains?
  - Wire simplifies onboarding through a single sign-on experience similar to Web2. Users can create an account with an email, username, and password. For advanced functionality or when off-ramping to another chain, they can escalate to managing mnemonic phrases, making it easy for both new and experienced users to start and adapt as needed​
- How does the to-be-named NewWalletCo help in onboarding new users?
  - This new wallet will support all blockchains, enabling users to keep their keys while providing functionality like universal identity across chains. The wallet integrates seamlessly into the onboarding process, offering crypto SSO (Single Sign-On) for simplified account recovery, allowing gradual user progression from beginner to expert​.
- What are the barriers to onboarding users into Web3 that Wire addresses?
  - Wire eliminates the need for users to understand gas fees or complex bridging processes by providing gas-free interactions on whitelisted contracts. It also abstracts the technical complexities of managing assets across chains, offering an intuitive experience​
- How does Wire handle onboarding for developers and businesses?
  - Developers can onboard easily through Wire's robust ecosystem, including open-source tools, a universal transaction layer, and chain-agnostic protocols like UPAP and WNS, which ensure compatibility with various blockchains without needing additional permissions​
- How does Wire enable seamless onboarding into its network for various blockchain assets?
  - Assets remain on their native chains, with ownership abstracted via Wire Name Service (WNS) and validated through settlement contracts. This ensures users don’t face the risks and complexities of transferring assets, making onboarding assets straightforward​
- How does Wire Network empower users to self-host liquidity pools and earn yield?
  - Wire Network’s innovative software enables users to independently create and manage liquidity pools directly from their devices, whether hosted on a phone, server, or other hardware. Unlike traditional platforms like BancorSwap, Wire’s solution focuses on decentralization and user autonomy. By using Wire’s wallet, users can seamlessly sign transactions, configure their liquidity pools, and start earning yield—all without relying on centralized platforms. This approach allows individuals to retain full custody of their assets while participating in DeFi, aligning with Wire’s mission to empower user sovereignty and promote decentralized finance.
  - NOTES
    - Phase 1 of LPs will be self-hosted (phone or server or whatnot)
      - Different kind of product that BancorSwap
      - Software will allow you to sign for that
      - Wallet will allow you to get yield if you want to setup a pool yourself
- How does Wire Network's Mainnet Alpha differ from the Testnet?
  - Wire Network's Testnet and Mainnet Alpha serve distinct purposes within the development and deployment of the blockchain. The Testnet is a sandbox environment designed for developers to test and debug applications without the risk of financial loss, ensuring that features and upgrades function correctly before release. It allows experimentation with transactions, smart contracts, and system integrations in a controlled, consequence-free setting. On the other hand, the Mainnet Alpha represents the first live version of Wire Network’s blockchain, where real transactions occur, and the economic models, governance structures, and security protocols are implemented and validated under real-world conditions. The transition to Mainnet Alpha signifies a pivotal step toward broader adoption, offering early participants the opportunity to engage with the network in its operational state while receiving ongoing updates and enhancements.
  - NOTE
    - Mainnet Alpha
      - May need manual hand-holding to whitelist smart contracts for nogas
- What are Polymorphic Blocks?
  - Polymorphic Blocks in Wire Network represent a groundbreaking design that allows the network to support multiple cryptographic signature schemes and transaction formats within the same block. This flexibility is achieved by enabling Wire's settlement contracts to process and validate transactions originating from diverse blockchains, each using its own cryptographic standards. For instance, Wire can handle transactions signed with Ethereum's secp256k1 curve alongside those using newer algorithms, like those optimized for post-quantum cryptography, all in a single block. This is pivotal for interoperability, as it ensures that Wire can seamlessly integrate with emerging blockchains without requiring the entire network to standardize to a single format. This capability makes Wire uniquely adaptable and future-proof in an ever-evolving blockchain ecosystem​