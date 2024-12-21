---
id: week 4
aliases: []
tags: []
---

## Questions:

- Is the Turing incompleteness of  
   Bitcoin's scripting language (SCRIPT)  
   a feature or a deficiency?

- What are digital signatures,  
   where are they placed in a  
   transaction, and what is their  
   purpose? Describe some real-life  
   exploits that occurred due to poor  
   randomness in digital signatures.  
   Besides signing transactions,  
   what other uses could digital  
   signatures have?

### ==Is the Turing incompleteness of Bitcoin's scripting language (SCRIPT) a feature or a deficiency?==

It is a feature: An extract from the text says

- “The Bitcoin transaction script language contains many operators, but is deliberately limited in one important way—there are no loops or complex flow control capabilities other than conditional flow control. This ensures that the language is not *Turing Complete*, meaning that scripts have limited complexity and predictable execution times. Script is not a general-purpose language. These limitations ensure that the language cannot be used to create an infinite loop or other form of "logic bomb" that could be embedded in a transaction in a way that causes a denial-of-service attack against the Bitcoin network. Remember, every transaction is validated by every full node on the Bitcoin network. A limited language prevents the transaction validation mechanism from being used as a vulnerability.”

### ==What are digital signatures?==

It is a Cryptographic tools that verify the authenticity of a “message” or document. In Bitcoin, the “message” that is signed is the hash of the transaction data which are  
The transaction input, the transaction output, and the transaction metadata.

### ==where are they placed in a transaction==,

The digital signature produced by signing the transaction data is included in the input section of a Bitcoin transaction to prove ownership of the funds being spent.

### ==what is their purpose?==

An extract from the text:

- “A digital signature serves three purposes in Bitcoin. First, the signature proves that the controller of a private key, who is by implication the owner of the funds, has *authorized* the spending of those funds. Secondly, the proof of authorization is *undeniable* (nonrepudiation). Thirdly, that the authorized transaction cannot be changed by unauthenticated third parties—that its *integrity* is intact”

### ==Describe some real-life exploits that occurred due to poor randomness in digital signatures.==

**Quick Point:** The Two signature algorithms currently used in Bitcoin are the *schnorr signature algorithm* and the *Elliptic Curve Digital Signature Algorithm* (_ECDSA_).

Here’s an extract from the text

- “As we saw in [Schnorr Signatures](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch08_signatures.adoc#schnorr_signatures) and [ECDSA Signatures](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch08_signatures.adoc#ecdsa_signatures), the signature generation algorithm uses a random number *k* as the basis for a private/public nonce pair. The value of *k* is not important, *as long as it is random*. If signatures from the same private key use the private nonce *k* with different messages (transactions), then the signing *private key* can be calculated by anyone. Reuse of the same value for *k* in a signature algorithm leads to exposure of the private key!”

==**Real-life exploits**==

- Sony PlayStation 3: In 2010, hackers discovered that Sony's implementation of the Elliptic Curve Digital Signature Algorithm (ECDSA) in the PlayStation 3 console used a static, instead of random, value for each signature. This allowed attackers to recover the private key used for signing software allowed to run on the console**,** potentially allowing anyone to run any software - including pirated games - on the console
- In 2013, a significant exploit affected Bitcoin wallets on Android due to poor randomness in digital signatures. The issue was with the random number generation in the Android platform, which led to the reuse of nonces (random numbers used in the signing process). This made it possible for attackers to derive the private keys from the signatures, allowing them to steal funds from the wallets.

### ==Besides signing transactions, what other uses could digital signatures have?==

- **Escrow Services**: Facilitate trustless escrow by requiring signatures from multiple parties to release funds.
- **Decentralized Applications (DApps)**: Authenticate the source of a DApp and ensure it hasn't been tampered with.
- **Voting Systems**: Here Digital signatures ensure that votes cannot be altered after they are cast.

