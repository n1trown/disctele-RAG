## **📌 Summary: What Wire is Building with liqSol**

### **🧠 Core Concept**

Wire Network is building a **trustless, high-performance liquid staking protocol** for Solana. It allows users to stake native SOL while receiving a liquid representation (liqSOL token), which they can use across DeFi while still earning staking rewards. Wire extracts maximum validator rewards and syncs them with our 24-hour emissions cycle.

### **⚙️ How It Works (User Flow)**

1. **Deposit SOL** on the Wire Hub.  

2. Receive **liqSOL** 1:1, a tradable token representing staked SOL.  

3. Earn daily staking rewards auto-compounded into the system (or claimable).  

4. When ready to unstake, burn liqSOL to receive an **NFT withdrawal receipt** (redeemable later for SOL after Solana’s ~2-epoch cooldown).  

5. Optionally sell the NFT receipt on a secondary marketplace.  

### **🎯 Why This Matters**

- **Liquidity + Yield:** Users earn yield from staking SOL **without losing access** to capital.  

- **Composable DeFi Asset:** liqSOL can be LP’d, swapped, or held like any SPL token.  

- **Trustless by Design:** No off-chain or multisig control; validator selection and reward distribution is governed entirely by on-chain logic.  

- **Validator Optimization:** Our custom VPP (Validator Performance Points) score selects the **top 50 validators** algorithmically to maximize yield.  

- **MEV Integration:** We claim Jito’s MEV rewards on supported validators — free upside. Longer-term, Wire may build its own MEV layer.  

- **Wire Emissions Sync:** liqSol rewards operate on a **daily cycle**, synchronized with Wire's native emission schedule (TCM) — simplifying staking across chains.  

- **Cross-chain Future:** liqSol is designed to be **interoperable** via Wire’s token standard — usable across ecosystems with awareness of circulating supply across chains.  

### **🔐 Key Differentiators**

| **Feature** | **Wire (liqSol)** | **Jito** | **Marinade** |
| --- | --- | --- | --- |
| Fully Trustless? | ✅ Yes | ❌ Centralized staking selection | ❌ Semi-centralized |
| --- | --- | --- | --- |
| Daily Rewards? | ✅ Yes | ❌ Epoch-based | ❌ Epoch-based |
| --- | --- | --- | --- |
| 1:1 SOL-Pegged Token? | ✅ Yes (liqSOL) | ❌ Floating index token | ✅ Yes |
| --- | --- | --- | --- |
| Validator Selection | Algorithmic + open source VPP score | Committee controlled | Committee controlled |
| --- | --- | --- | --- |
| NFT Unstake Receipts | ✅ Yes, tradable | ❌ No | ❌ No |
| --- | --- | --- | --- |
| Cross-chain Ready | ✅ Built on Wire standard | ❌ No | ❌ No |
| --- | --- | --- | --- |

### **🔨 Current Dev Progress**

- ✅ liqSOL Token & NFT Receipt programs complete.  

- ✅ VPP scoring and validator routing logic defined.  

- 🟡 Withdrawals operator contract undergoing final refactor.  

- 🟡 Agency onboarding planned to accelerate specific programs.  

- 🟢 Goal: Ready for testing and audit ASAP.  

### **📣 Message to Business & Marketing Teams**

Wire is delivering **the most secure, efficient, and interoperable liquid staking system** on Solana. liqSol is foundational infrastructure for DeFi on Wire — a protocol-level primitive that enables seamless staking rewards, liquidity, and composability across chains.
