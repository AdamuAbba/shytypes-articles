---
id: Week 2
aliases: []
tags: []
---

What are the components of a transaction? Describe in brief each component
and the data they contain.

### Breakdown

A Bitcoin transaction consists of several key components. Each part plays a specific role in ensuring that the transfer of Bitcoin is secure, verifiable, and compliant with the rules of the Bitcoin network. The main components of a transaction are:

At a high level, a transaction has three main parts:

1. Transaction Input (TxIn)
   Description: Inputs specify where the Bitcoin being spent comes from. Each input is tied to a previous output from another transaction.
   Data:
   Transaction ID: A hash of the previous transaction where the Bitcoin originated.
   Output Index: Specifies which output of the previous transaction is being spent.
   Unlocking Script (ScriptSig): Provides proof that the spender has the right to use the funds, typically containing a digital signature and a public key.
2. Transaction Output (TxOut)
   Description: Outputs specify where the Bitcoin is going. Each output represents an amount of Bitcoin and a script that locks the amount to a specific address.
   Data:
   Value: The amount of Bitcoin to be transferred (in satoshis).
   Locking Script (ScriptPubKey): The script that defines the conditions that must be met to spend the output, usually tying it to a specific Bitcoin address.
3. Transaction ID (TxID)
   Description: A unique identifier for the transaction, calculated as the hash of the serialized transaction data.
   Data: Not directly a component but an important result of a transaction that helps to identify it on the blockchain.
4. Version Number
   Description: Indicates the version of the Bitcoin protocol that the transaction adheres to.
   Data: A 4-byte number indicating the protocol version.
5. Locktime
   Description: Specifies the earliest time or block height at which the transaction can be included in a block.
   Data: A 4-byte field that can either be a timestamp or a block height.
6. Witness Data (SegWit Transactions)
   Description: For Segregated Witness (SegWit) transactions, this component holds the witness data, which separates signature data from the transaction structure to reduce size and improve scalability.
   Data: Contains signatures and public keys in a format separate from the transaction inputs.
