---
id: Week 5
aliases: []
tags: []
---

# LBTC

Chapters 10 and 11: Embedding Bitcoin Scripts in P2SH Transactions and Empowering
Timelock with Bitcoin Scripts.

## Breakdown

### Wrapping P2WSH inside P2SH:

- **Backward Compatibility:**  
  Some wallets don't support native SegWit addresses yet. Wrapping P2WSH in P2SH allows older wallets to still process these transactions.

- **Gradual SegWit Adoption:**  
  Users get SegWit benefits (like lower fees and transaction malleability fixes) while staying compatible with non-SegWit systems.

- **Flexibility:**  
  P2SH supports more complex scripts (e.g., multisig) while still leveraging SegWit’s efficiency and security.

### Time lock using `nLockTime` and `nSequence`:

When a transaction includes a time lock using both nLockTime and nSequence, you have an Additional condition for delaying a transactions from being added to a block

- **nLockTime:**
  Prevents a transaction from being added to a block until a set block height or time (UNIX time) is reached.

- **nSequence:** 
nSequence works in conjunction with the CHECKSEQUENCEVERIFY opcode, further delaying the transaction based on time or blocks since the confirmation of its inputs

### Error in `testmempoolaccept`:

Returns result of mempool acceptance tests indicating if raw transaction(s) (serialized, hex-encoded) would be accepted by mempool.
- If both `nLockTime` and `nSequence` conditions aren't met, the transaction will return a **“non-final” error**, meaning it’s not yet valid to enter the mempool.

```json
{
  "txid": "<txid>",
  "allowed": false,
  "reject-reason": "non-final"
}
```
**source:** [ chainquery](https://chainquery.com/bitcoin-cli/testmempoolaccept)
