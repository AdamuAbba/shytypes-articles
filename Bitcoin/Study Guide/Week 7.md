---
id: Week 7
aliases: []
tags: []
---

# Bitshala Bitcoin study session (Mastering Bitcoin)

**Group:** 2

## Chapters

- Chapter 13: What is a multi-sig address?

  - In what situation is it advisable to share confidential information about your bitcoin keys with a trusted person?

- Chapters 14: What is an HTLC?
  - Which OP-code is used to achieve it in the context of payment channels?

## Breakdown

## What is a multi-sig address?

> "Whenever a company or individual stores large amounts of bitcoins, they should consider using a multisignature Bitcoin address. Multisignature addresses secure funds by requiring more than one signature to make a payment. The signing keys should be stored in a number of different locations and under the control of different people."

## In what situation is it advisable to share confidential information about your bitcoin keys with a trusted person?

> "In a corporate environment, for example, the keys should be generated independently and held by several company executives to ensure that no single person can compromise the funds. Multisignature addresses can also offer redundancy, where a single person holds several keys that are stored in different locations."

## What is an HTLC(Hash Time Lock Contracts)?

**Text Extract:** Payment channels can be further extended with a special type of smart contract that allows the participants to commit funds to a redeemable secret, with an expiration time.

### Hashlock

Imagine a locked box that can only be opened with a secret code. The sender locks up some digital assets in this box and creates a "hash" from the secret code. The recipient needs to provide the correct secret code to unlock the box and get the assets.

#### How it works?

- Creating a Secret:
  - The recipient of the payment generates a secret.
- Hashing the Secret:
  - The recipient then calculates the hash of the secret preimage using a hash function to give a digest
- Including the Hash in a Script:
  - The hash H is included in an output’s script.
  - This script ensures that only someone who knows the secret R can redeem the output.

### Time Lock

if the recipient doesn’t reveal the secret code in time? The contract has a built-in safety feature called a time lock. This means that if the secret code isn’t revealed within a certain time, the person who sent the money (the payer) can get it back. This time lock is enforced by a specific command in the contract called "CHECKLOCKTIMEVERIFY," which makes sure the funds are returned to the payer if the deadline passes without the secret being revealed.

Anyone who knows the secret R, which when hashed equals to H, can redeem this output by exercising the first clause of the IF flow.

If the secret is not revealed and the HTLC claimed after a certain number of blocks, the payer can claim a refund using the second clause in the IF flow.

## OP-Code Used in Bitcoin for HTLCs

In the context of Bitcoin payment channels, the key OP-code used to achieve the functionality of HTLCs is OP_CHECKLOCKTIMEVERIFY (CLTV). This OP-code enforces the timelock by ensuring that a specific block time or height must be reached before the transaction can be spent.

To implement the hashlock component, the OP_SHA256 and OP_EQUAL OP-codes are often used. Here's how these might be used in a Bitcoin script:

The script will typically check that the recipient can produce a hash preimage using OP_SHA256 and OP_EQUAL.
It then uses OP_CHECKLOCKTIMEVERIFY to enforce the timelock.
