---
id: Week 5
aliases: []
tags:
  - bitcoin
---

# Questions

- What is transaction pinning? How is it a vulnerability for multiparty time-sensitive protocols such as LN?

- What are bloom filters? How do they work?

## Breakdown

### What is transaction pinning?

#### Text Extract

> "Making it impossible or difficult to fee bump a transaction is called transaction pinning."

#### <a name="rbf">Replace-by-Fee (RBF)</a>

- **Definition**: A way to replace an unconfirmed transaction with a new one that has a higher fee.

- **How it works:** If your transaction is taking too long to confirm, you can resend it with a higher fee to encourage miners to pick it up faster.

#### Child Pays for Parent (CPFP)

- **Definition:** A method where a new transaction (child) is created to speed up the confirmation of an older unconfirmed transaction (parent) by attaching a higher fee.

- **How it works:** You send a new transaction that spends the output of the slow transaction and includes a high fee.
  Miners are motivated to confirm both transactions to earn the higher fee.

Both [RBF (Replace-by-Fee)](#rbf) and CPFP (Child Pays for Parent) are methods to increase the transaction fee to get it confirmed faster. However, there are rules to prevent abuse of these methods, which can sometimes make it hard or impossible to increase the fee. This difficulty or impossibility in increasing the transaction fee is called transaction pinning.

### How is it a vulnerability for multiparty time-sensitive protocols such as LN?

**Quick Note:**

> The Lightning Network (LN) is a second-layer solution built on top of the Bitcoin blockchain to enable faster and cheaper transactions.

It is a vulnerability for multiparty time-sensitive protocols like the Lightning Network (LN) because they need to agree on the outcome of certain transactions within a specific time frame.Actions or transactions must be completed within set deadlines. If deadlines are missed, there could be penalties or funds could be lost.

**How LN works**:Users create payment channels that enable fast transactions off-chain, which are eventually settled on the blockchain. This is achieved through different types of transactions.

**Commitment Transactions:** These are special transactions that close the payment channels and settle the final balance on the blockchain.

- Attack Scenario: An attacker can pin a commitment transaction (or related transactions) by making it less likely to be confirmed promptly, often by manipulating transaction fees or creating complex dependencies.

- Consequence: If the legitimate transaction is pinned and not confirmed in time, the attacker can exploit the delay. This could result in financial loss for the parties involved, as they might not be able to claim their funds or might face penalties.

### What are bloom filters?

#### Text Extract

> A [ bloom filter ](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch10_network.adoc#:~:text=A%20bloom%20filter,are%20searching%20for.) is a probabilistic search filter, a way to describe a desired pattern without specifying it exactly. Bloom filters offer an efficient way to express a search pattern while protecting privacy. They are used by lightweight clients to ask their peers for transactions matching a specific pattern without revealing exactly which addresses, keys, or transactions they are searching for.

#### In simpler terms

A Bloom filter is like a fuzzy search tool. It helps you find what you’re looking for without saying exactly what it is.

### How do they work?

- **Setting Up:** You start with a row of N boxes, all set to 0.You have M hash functions ready to use.

- **Adding an Item:** You take the item (like a word) and run it through each of the M hash functions. Each hash function gives you a number that corresponds to a box in the row. You change the boxes at those numbers to 1.

- **Checking an Item:** To see if an item might be in the list, you run it through the same M hash functions. Check the boxes at the numbers given by the hash functions. If all the boxes are 1, the item might be in the list. If any box is 0, the item is definitely not in the list.
