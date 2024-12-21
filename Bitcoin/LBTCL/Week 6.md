---
id: Week 1
aliases: []
tags: []
---

# LBTC

Chapters 12 and 13: Expanding Bitcoin Scripts and Designing Real Bitcoin Scripts.

## Breakdown

### What are some real world examples of multisig escrows?

- **BitGo**: Provides multi-signature wallets for cryptocurrency exchanges, enabling secure escrow services where multiple parties must sign transactions.

- **OpenBazaar**: A decentralized marketplace that uses multisig wallets for buyer-seller escrow. A third party acts as a mediator in case of disputes.

- **LocalBitcoins**: Users can opt for multisig escrow for safer peer-to-peer Bitcoin trading. (Closed)

- **BTCPay Server**: Enables multisig setups for merchants and customers, adding an extra layer of security in transactions.

- **Bisq**: A decentralized Bitcoin exchange that uses multisig escrow to hold funds until both parties confirm the trade.

### What are some real world conditional script examples?

- Timelocks (CheckLockTimeVerify):
  - Example: A person creates a transaction that can only be spent after a certain time or block height. Commonly used in Lightning Network or escrow contracts where funds are locked for a period before they can be accessed

- Hash Time-Locked Contracts (HTLCs):
  - Used in Lightning Network and Atomic Swaps. It allows a transaction to be executed if a cryptographic hash is revealed within a time frame. If the condition isn't met, the transaction is canceled.

- Multisig with condition:
  - Example: A multisig wallet where funds can be spent if 2-of-3 parties sign the transaction. However, if one party doesn't sign within a certain timeframe, it falls back to 1-of-2 multisig after a timelock.

- Inheritance scripts:
  - Conditional setup where a beneficiary receives funds if the original owner doesn't spend the coins within a set period (acting as a fail-safe or "dead man's switch").
