---
id: Week 1
aliases: []
tags: []
---

## Questions:

- What is the Bitcoin Issuance  
   Rate? How do we know the  
   supply cap of Bitcoin is 21  
   million?

- Why did Satoshi say transactions  
   are a "chain of digital signatures"?  
   What is a UTXO? What's the  
   difference between the UTXO and  
   the account-based model? Why did  
   Bitcoin chose to stick with the  
   UTXO model?

## Breakdown

### What is the Bitcoin Issuance Rate?

### Bitcoin Issuance Rate

The bitcoin issuance rate talks about how much bitcoin can be created and is available for circulation. We know that Bitcoins are created as rewards for miners who validate and add new blocks to the blockchain. Initially, miners received 50 bitcoins for each block they mined.

1. **Halving Events**: The reward is halved every four years:
   - 2009: 50 bitcoins per block
   - 2012: 25 bitcoins per block
   - 2016: 12.5 bitcoins per block
   - 2020: 6.25 bitcoins per block
   - 2024: 3.125 bitcoins per block (expected)
2. **Decreasing Rate**: This halving process continues until the reward reaches zero, which slows the rate of new Bitcoin creation over time.

### Summary

- **Controlled Supply**: New bitcoins are created at a decreasing rate due to regular halving events.
- **Predictable Schedule**: The issuance rate is predictable, ensuring the total supply will never exceed 21 million bitcoins.

### ==How We Know the Supply Cap of Bitcoin is 21 Million==

### 1. **Protocol Rules**

- **Hard-Coded Limit**: Bitcoin's software is programmed to ensure the total supply never exceeds 21 million bitcoins.

### 2. **Mining Rewards and Halving**

- **Initial Reward**: Miners originally received 50 bitcoins per block.
- **Halving Events**: Every four years, the reward is cut in half (e.g., 50 to 25 to 12.5, etc.) until it reaches zero.

### 3. **Geometric Series**

- **Mathematical Design**: The sum of all block rewards forms a geometric series that adds up to 21 million bitcoins.

### 4. **Consensus Mechanism**

- **Network Agreement**: All participants (miners, nodes, users) follow the rules, making it impossible to change the cap.

### 5. **Open-Source Code**

- **Transparency**: Bitcoin's code is public, so anyone can verify the 21 million cap and halving schedule.

### ==Why did Satoshi say transactions are a "chain of digital signatures"?==

Satoshi described transactions as a "chain of digital signatures" to emphasize how the Bitcoin protocol enforces security and validations without needing a third-party governing body like in the case of centralized finance.

Quick breakdown:

- Each Bitcoin transaction includes a digital signature generated via the sender's private key
- Transactions are linked together in a chain with pointers to previous transactions.
- the blockchain is public and everyone is involved in transaction validation
- A true trust-less system with no need for a third party to police transactions between members

### ==What is a UTXO?==

A UTXO (Unspent Transaction Output) in Bitcoin is like having money in your pocket that hasn't been spent yet. Bitcoins are received as UTXOs showing a specific amount of bitcoin. When you want to make a payment, you pick one or more of these UTXOs to use as the payment amount (input) in a new transaction there making it become "spent" and can't be used again.

### ==What's the difference between the UTXO and the account-based model?==

- With the UTXO model, the mechanism to find your Bitcoin wallet balance involves tracking a specific set of UTXOs ensuring user privacy.
- Account-based model just like in the banking space, transactions update the account balance directly thereby sacrificing privacy.

### ==Why did Bitcoin choose to stick with the UTXO model?==

Bitcoin chose to stick with the UTXO model because it enhances security, privacy, and inclusiveness. By having transactions as separate encrypted entities, they are harder to trace compared to account-based systems and they provide a form of inclusiveness to the participants on the network via transaction validation. The UTXO model aligns with Bitcoin's principles of decentralisation

