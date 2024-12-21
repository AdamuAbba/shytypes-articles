---
id: Week 1
aliases: []
tags: []
---

# LBTC

Chapters 8 and 9: Expanding Bitcoin Transactions in Other Ways and Introducing
Bitcoin Scripts.

## Questions:

- How are locktime via Unix time and locktime
via block height differentiated in the
transaction data?

- What are scriptPubKey and scriptSig? How
are they used in script verification?

- Why is P2PKH needed when we already had
P2PK?

- What is LockTime? Why is LockTime useful?

- Differentiate between SegWit and non-SegWit script verification.

- What is OP_RETURN? How is it useful? What happens during script verification when an OP_RETURN is encountered? What if the value of OP_RETURN is non-zero?

- What are standard and non-standard scriptPubKeys? Can you create and submit a transaction with a non-standard scriptPubKey to your mempool? (Hint: Create a transaction with an addition script and call testmempoolaccept).

## Breakdown

### How are locktime via Unix time and locktime via block height differentiated in the transaction data?

Locktime is a feature in Bitcoin that allows you to set a delay before a transaction can be added to the blockchain. It means the transaction cannot be confirmed until:

- A certain block is mined (block height).

- Or a specific date and time is reached (Unix time). This can be useful for delaying payments or creating time-based conditions for transactions.

The locktime field in the transaction data is a 4-byte unsigned integer, and the value of this field differentiates whether it's interpreted as a Unix timestamp or a block height

Block Height: If the locktime value is less than 500,000,000 (5×10^8), it is interpreted as a block height. This means the transaction cannot be included in a block until the blockchain reaches that height.

Unix Time: If the locktime value is equal to or greater than 500,000,000, it is interpreted as a Unix timestamp (seconds since January 1, 1970). The transaction can only be included in a block if the block’s timestamp is after this Unix time.

### What are scriptPubKey and scriptSig? How are they used in script verification?

In Bitcoin transactions, scriptPubKey and scriptSig are key components used to verify and unlock funds:

- scriptPubKey (locking script): Found in the output of a transaction. It specifies the conditions that must be met to spend the funds. Typically contains the recipient’s public key hash or other spending conditions.

- scriptSig (unlocking script): Found in the input of a transaction. It provides the data needed to satisfy the conditions set by the scriptPubKey (usually includes the signature and public key of the sender).

#### How they are used in script verification

  - scriptSig is run first to provide input data.

  - scriptPubKey is run next to verify that the provided data (from scriptSig) satisfies the conditions.
  
  - If scriptSig correctly satisfies scriptPubKey, the transaction is valid, and the funds can be spent.

### Why is P2PKH needed when we already had P2PK

P2PKH (Pay-to-PubKeyHash) was introduced to improve on P2PK (Pay-to-PubKey) for several reasons:

- Improved Privacy: P2PK reveals the public key right away, but P2PKH only reveals the hash of the public key until it's spent, protecting the key from early exposure.

- Reduced Attack Surface: Since public keys in P2PKH are only exposed when spending, it reduces the risk of quantum computing attacks, as the public key isn't available for analysis until it's necessary.

- Shorter Addresses: P2PKH addresses are shorter and easier to use than P2PK, improving usability.

Overall, P2PKH provides more security and privacy over P2PK.

### Differentiate between SegWit and non-SegWit script verification.

The key differences between SegWit (Segregated Witness) and non-SegWit script verification are:

- Witness Data Location:

  - Non-SegWit: Signature and script data are included within the transaction itself.

  - SegWit: Signature and witness data are separated from the transaction, placed in a different section of the block, reducing the transaction size.

- Transaction Size:

  - Non-SegWit: Larger transaction size due to including signature data in the main transaction.

  - SegWit: Smaller transaction size as witness data is removed, lowering fees and allowing more transactions in a block.

- Malleability:

  - Non-SegWit: Transactions are vulnerable to malleability, where signature data can be modified, changing the transaction ID.

  - SegWit: Fixes transaction malleability by removing signature data from the part of the transaction that determines the transaction ID.

- Script Versioning:

  - Non-SegWit: Script upgrades are more difficult as changes affect the entire transaction structure.

  - SegWit: Allows easier upgrades to Bitcoin's scripting language through witness versioning without affecting non-witness parts of the transaction.
  - SegWit improves efficiency, reduces malleability, and supports future upgrades

### What is OP_RETURN? How is it useful? What happens during script verification when an OP_RETURN is encountered? What if the value of OP_RETURN is non-zero?

OP_RETURN is a Bitcoin script opcode used to embed arbitrary data in a Bitcoin transaction. It marks the output as unspendable and carries no associated value that can be later redeemed, making it ideal for data storage or signaling purposes on the blockchain.

#### Key Points:

- Data Embedding: It allows embedding up to 80 bytes of data (depending on protocol limits).

- Unspendable Output: The transaction's output cannot be spent, reducing its effect on the UTXO set.

- Applications: Used in timestamping, asset issuance, and storing metadata on-chain (e.g., in Counterparty or OmniLayer).

#### Script Verification with OP_RETURN:

- When an OP_RETURN is encountered during script verification, the script fails, meaning the output is considered unspendable and does not require further validation. This reduces processing time.

#### Non-Zero OP_RETURN:

- If OP_RETURN is followed by a non-zero value, it doesn't change the outcome. The script still fails and marks the output as unspendable.

### What are standard and non-standard scriptPubKeys? Can you create and submit a transaction with a non-standard scriptPubKey to your mempool? (Hint: Create a transaction with an addition script and call testmempoolaccept).

Standard scriptPubKeys are specific Bitcoin scripts that the Bitcoin network nodes typically recognize and accept into the mempool because they follow known formats. These include:

P2PKH (Pay-to-PubKey-Hash): Transactions pay to a Bitcoin address (hash of a public key).
P2SH (Pay-to-Script-Hash): Transactions pay to a hash of a script.
P2PK (Pay-to-PubKey): Transactions pay directly to a public key.
P2WPKH and P2WSH (SegWit variants): Native SegWit address types.
Non-standard scriptPubKeys are scripts that don't follow these common patterns. Examples include unusual opcodes or custom scripts not recognized by most nodes, like a custom addition script or any arbitrary conditions outside standard types

Most Bitcoin nodes have a policy to reject non-standard transactions for security and efficiency. However, in testnet or custom node environments, you can configure nodes to accept non-standard transactions.
