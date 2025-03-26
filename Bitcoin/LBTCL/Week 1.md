# Week 1

## Chapter 1

### Why is direct interaction with Bitcoin Core and c-lightning via the command line considered more robust and secure compared to using higher-level libraries?

- Direct interaction with Bitcoin Core and c-lightning ensures:
  - 🔒 Better security: No third-party dependencies or abstractions.
  - ⚙️ Full control: Access to all RPC calls and configurations.
  - 🔍 Enhanced reliability: Avoids potential bugs or limitations in higher-level libraries.

### How does the decentralization of Bitcoin challenge traditional centralized payment systems?

- Bitcoin’s decentralization offers:
  - 🌍 Permissionless transactions: No single authority can censor transactions.
  - 📊 Transparency: Publicly verifiable ledger.
  - 🏦 Resilience: No central point of failure.

### What are the potential risks and benefits of working directly with bitcoind and lightningd for cryptocurrency development?

- Risks:
  - 🔥 Higher complexity: Requires deep technical knowledge.
  - ⚠️ Security risks: Misconfigurations can lead to loss of funds.
- Benefits:
  - 🔒 Enhanced control and security.
  - 🛠 Flexibility in custom applications.
  - 📊 Improved efficiency and reliability.

### Why is Bitcoin considered pseudonymous rather than fully anonymous?

- Bitcoin is pseudonymous because:
  - 📌 Transactions are publicly visible on the blockchain.
  - 🔑 Addresses do not directly reveal identity, but they can be traced back to individuals if linked to personal information.

### How does Bitcoin prevent censorship of transactions?

- Bitcoin prevents censorship through:
  - ⛓ Decentralized network of nodes validating transactions.
  - 🔐 Proof-of-work consensus mechanism making attacks costly.
  - 📂 Permissionless design allowing anyone to participate.

### What is the role of RPC (Remote Procedure Call) in interacting with Bitcoin Core and Lightning?

- RPC provides:
  - 📞 Interface for communication between software and Bitcoin Core/Lightning.
  - 📋 Allows querying blockchain data, sending transactions, and managing nodes.
  - 🖥 Enables programmatic access for building applications.

---

## Chapter 2

### How do the five major types of Bitcoin nodes differ?

- Types of nodes:
  - 🌕 Full Nodes: Store entire blockchain, verify transactions.
    - Example: A Bitcoin Core node running with the `txindex=1` option to keep a complete transaction index for querying historical data.
    - Differences:
      - Stores the entire blockchain.
      - High disk space requirements.
      - Provides high security and trustworthiness.
      - Does not rely on other nodes.
      - Requires more computational resources.
  - 🌱 Light Nodes: Depend on full nodes, store headers only.
    - Example: Mobile wallets like Electrum and BlueWallet.
    - Differences:
      - Relies on full nodes for validation.
      - Uses less disk space and bandwidth.
      - Suitable for mobile and lightweight applications.
      - Provides lower security compared to full nodes.
      - Faster to set up and use.
  - 🪶 Pruned Nodes: Keep recent blockchain history, discard old data.
    - Example: Raspberry Pi devices running Bitcoin Core in pruned mode.
    - Differences:
      - Stores only recent blocks.
      - Saves disk space by discarding old data.
      - Retains transaction validation capability.
      - Cannot provide historical data.
      - Useful for low-storage environments.
  - 🔒 Archival Nodes: Store full historical blockchain data.
    - Example: Blockstream’s Esplora.
    - Differences:
      - Stores the entire blockchain history.
      - Provides complete transaction history.
      - Requires massive storage and resources.
      - Used for research and analysis.
      - Acts as a reference point for other nodes.
  - ⚡ Lightning Nodes: Handle off-chain transactions for faster payments.
    - Differences:
      - Uses payment channels for quick transactions.
      - Reduces load on the main blockchain.
      - Requires liquidity management.
      - Provides fast and low-fee transactions.
      - May require constant uptime for reliability.

### What are the differences between Mainnet, Testnet, and Regtest, and in what scenarios would each be used?

- **Mainnet**:
  - 💰 Real Bitcoin transactions.
  - Differences:
    - Uses real BTC with actual value.
    - Fully decentralized and secure.
    - High transaction fees.
    - Strict consensus rules.
    - Suitable for production use.

- **Testnet**:
  - 🧪 Public testing network with test Bitcoin.
  - Differences:
    - Uses test BTC with no monetary value.
    - Easier access to funds (via faucets).
    - Relaxed rules compared to Mainnet.
    - Used for development and testing.
    - Transactions may be slower than Regtest.

- **Regtest**:
  - ⚙️ Private network for local testing and rapid development.
  - Differences:
    - Instant block generation.
    - No network connectivity required.
    - Full control over mining difficulty.
    - Suitable for unit testing and debugging.
    - Not connected to Mainnet or Testnet.

---

## Chapter 3

### What are the basic steps to create a Bitcoin address to receive funds?

1. **Start Bitcoin Core Daemon** (if not already running):
```bash
bitcoind -daemon
```

2. **Create a new wallet** (if you don't have one):
```bash
bitcoin-cli createwallet "mywallet"
```

3. **Load the wallet** (if it’s not loaded already):
```bash
bitcoin-cli loadwallet "mywallet"
```

4. **Generate a new receiving address**:
```bash
bitcoin-cli -rpcwallet=mywallet getnewaddress
```

5. **Get the descriptor for the generated address** (optional):
```bash
bitcoin-cli -rpcwallet=mywallet getdescriptorinfo "wpkh([<fingerprint>/84'/0'/0'/0/0]xpub...)"
```

6. **Check the balance** (to confirm received funds):
```bash
bitcoin-cli -rpcwallet=mywallet getbalance
```

7. **Verify address details** (if needed):
```bash
bitcoin-cli -rpcwallet=mywallet validateaddress "<address>"
```

### What is a descriptor, and how does it relate to address generation?

#### What is a Descriptor? 🔑
A **descriptor** is a string that defines how a Bitcoin address or set of addresses is generated, derived, and validated. It specifies the conditions under which coins can be spent, including:
- 🔒 Public keys
- 📜 Scripts (e.g., P2PKH, P2WPKH, P2SH)
- 🧩 Key derivation paths

#### How Descriptors Relate to Address Generation 🔗
- Descriptors provide a **structured way** to define address generation rules, especially in wallets.
- They enable easy management of **hierarchical deterministic (HD) wallets**.
- They ensure consistency and compatibility across wallet implementations.
- They are useful for **backup, recovery, and cross-software compatibility**.

#### Example of a Descriptor 💡
A common descriptor for a native SegWit address (P2WPKH) looks like this:
```bash
wpkh([<fingerprint>/84'/0'/0'/0/0]xpub...)
```
This descriptor represents:
- `wpkh`: A native SegWit address type.
- `<fingerprint>/84'/0'/0'/0/0`: A derivation path conforming to BIP84 for generating a receiving address.
- `xpub...`: An extended public key.

#### Commands to Work with Descriptors 🖥️
- Generate a descriptor:
```bash
bitcoin-cli getdescriptorinfo "wpkh([<fingerprint>/84'/0'/0'/0/0]xpub...)"
```
- Derive addresses from a descriptor:
```bash
bitcoin-cli deriveaddresses "<descriptor>"
```
- Validate an address:
```bash
bitcoin-cli validateaddress "<address>"
```

Descriptors make address management more robust and compatible across different software implementations. 🔥

### What are the key files and directories in a Bitcoin node’s file layout?

- 📂 `bitcoin.conf`: Configuration file.
- 📂 `blocks/`: Stores blockchain data.
- 📂 `chainstate/`: Contains UTXO database.
- 📂 `wallets/`: Stores wallet information.

### How can you use informational commands in bitcoin-cli to understand your node's status?

- `getblockchaininfo`: Provides blockchain status.
- `getnetworkinfo`: Shows network details.
- `getwalletinfo`: Displays wallet information.

### Why is it important to verify your Bitcoin setup before engaging in transactions?

- 🔒 Ensures your node is properly configured.
- 🛡 Prevents accidental loss of funds.
- 📊 Confirms network synchronization.

### What are the benefits of using command-line variables when working with Bitcoin Core?

- 📋 Simplifies command usage.
- 🔍 Provides better control over inputs and outputs.
- 🚀 Speeds up repetitive tasks.