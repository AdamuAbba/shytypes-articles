---
id: Week 3
aliases: []
tags: []
---

1. What is a multisig? What are the common
   script types for multisig addresses?
2. What is a PSBT and why is it
   useful?
3. Why is it important to preserve the order of
   keys in multisig addresses for address
   generation? What happens if the order isn't
   preserved?

## Answers

A multisig (multi-signature) is a type of Bitcoin address that requires more than one private key signature to authorize a transaction. It is often used for added security or shared ownership of funds, ensuring that no single party can unilaterally control or move the funds.

Common script types for multisig addresses:
P2SH (Pay-to-Script-Hash):

The most common multisig script type. Funds are sent to a hash of the redeem script, which is later revealed when spending.
Example: 2-of-3 multisig.
P2WSH (Pay-to-Witness-Script-Hash):

A more efficient SegWit version of P2SH that reduces transaction fees by moving the redeem script outside of the main transaction data.
P2TR (Pay-to-Taproot):

Allows for more complex spending conditions, including multisig, with the added benefit of privacy and efficiency since it hides whether a multisig is used unless all participants reveal it.

### 2

A PSBT (Partially Signed Bitcoin Transaction) is a Bitcoin transaction format that allows multiple parties to collaborate in signing a transaction without needing to trust one another. It's particularly useful in multisig setups, hardware wallets, or scenarios where different devices or parties hold keys.

Why PSBT is useful:
Multisig transactions: It enables different participants to sign a transaction at different stages and locations.

Hardware wallets: It allows the creation of a transaction on one device (e.g., a computer) and signing on a separate, secure device (e.g., a hardware wallet) without exposing private keys.

Collaboration: Multiple parties can contribute inputs, outputs, or signatures before finalizing the transaction, enabling shared control over funds.

Offline signing: PSBTs can be passed between offline (air-gapped) devices for signing without ever revealing sensitive information.

Key features:
Partially signed: The transaction can be incrementally signed by multiple parties, ensuring that all required signatures are collected before broadcasting.

Standardized format: It defines a standard for handling unsigned, partially signed, and fully signed transactions.

PSBT simplifies complex transaction workflows while ensuring security and coordination between multiple parties or devices.

### 3

In a multisig address, the order of keys matters because it affects the final Bitcoin address.

If the order changes, a completely different address is created.
This means if you put the keys in a different order than when the address was made, you won't be able to access your Bitcoin.
So, keeping the same order ensures that the address stays the same, and everyone can sign to spend the funds correctly.
