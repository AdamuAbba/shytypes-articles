---
id: Week 1
aliases: []
tags: []
---

# LBTC

Chapters 1, 2, and 3: Introduction, Setup your Bitcoin, and Understand your setup.

## Questions:

- Describe in brief the main components of the Bitcoin system. What are
  transactions? How are they created? How are
  they protected?

- What is a software
  signature? Why is it
  recommended to verify the
  signature of the downloaded
  Bitcoin Core binary? What
  possible attack can be made
  with a malicious binary?

- What is bitcoin-cli? What
  happens when you run
  bitcoin-cli command without
  starting bitcoind?
  What's the difference between
  different node types (mainnet,
  testnet, signet, and regtest)?

- What are cryptographic primitives used in Bitcoin? Give a brief description of them.

## Breakdown

### Describe in brief the main components of the Bitcoin system. What are transactions? How are they created? How are they protected?

- Nodes: Computers running Bitcoin software, participating in the network by verifying transactions and blocks.

- Blockchain: A public ledger where all confirmed Bitcoin transactions are recorded.

- Transactions: Movements of Bitcoin from one address to another, which are verified and added to the blockchain.

- Mining: The process of validating transactions and creating new blocks through solving complex cryptographic puzzles.

- Wallets: Software or hardware that stores Bitcoin private keys and enables users to send/receive Bitcoin.

What are Transactions?
A transaction is the transfer of Bitcoin between two parties. It consists of inputs (Bitcoin being spent) and outputs (the recipient's address). Each transaction references previous ones to prove ownership of the Bitcoin being transferred.

#### How are Transactions Created?

A user generates a transaction using their Bitcoin wallet.
The wallet selects unspent transaction outputs (UTXOs) as inputs and specifies outputs (recipient addresses and amounts).
The transaction is signed using the sender’s private key to prove ownership of the Bitcoin being sent.
The transaction is broadcast to the Bitcoin network for validation.

#### How are Transactions Protected?

- Digital Signatures: Cryptographic signatures that ensure only the owner of the private key can spend Bitcoin.
  Proof of Work: Miners must solve a cryptographic puzzle (hashing) to validate transactions and add them to the blockchain.
  Consensus Rules: Nodes validate transactions by following strict rules that prevent double-spending and fraud.

### What is a software signature? Why is it recommended to verify the signature of the downloaded Bitcoin Core binary? What possible attack can be made with a malicious binary?

A software signature is a cryptographic hash of a software file, signed by the developer using their private key. It allows users to verify the authenticity and integrity of the software by checking the signature against the developer's public key.

If you don't verify the binary, you risk installing malware that could steal your Bitcoin, spy on your activities, or compromise your system's security. Verifying the signature helps protect against these attacks.

### What is bitcoin-cli? What happens when you run bitcoin-cli command without starting bitcoind? What's the difference between different node types (mainnet, testnet, signet, and regtest)?

bitcoin-cli is a command-line interface tool that interacts with a running instance of Bitcoin Core (bitcoind). It allows users to send commands to the bitcoind JSON-RPC server to retrieve blockchain data, manage wallets, or control various node operations.
If you run bitcoin-cli without starting bitcoind, the command will fail because there is no running Bitcoin daemon for it to connect to

- Mainnet: The real Bitcoin network where actual transactions take place with real value.

- Testnet: A testing network for Bitcoin with no real value; used by developers to test apps.
  Signet: A more predictable test network where blocks are signed by selected parties, ideal for controlled testing.

- Regtest: A private network for development, where you can create blocks manually for fast testing.

### What are cryptographic primitives used in Bitcoin? Give a brief description of them.

1. Hash Functions (SHA-256)
   Description: Bitcoin uses SHA-256 (Secure Hash Algorithm 256-bit) extensively. A hash function takes an input and produces a fixed-size output (256 bits in this case). It is deterministic, fast, and resistant to collisions, meaning no two different inputs should produce the same hash.
   Role in Bitcoin: Used in creating block hashes, transaction IDs, and mining (Proof of Work). Bitcoin also applies SHA-256 twice (SHA-256d) in the mining process to enhance security.

2. RIPEMD-160
   Description: RIPEMD-160 is another cryptographic hash function that outputs a 160-bit hash.
   Role in Bitcoin: Bitcoin uses RIPEMD-160 in combination with SHA-256 to create Bitcoin addresses (specifically, Hash160, which is RIPEMD-160(SHA-256(public key))).

3. Elliptic Curve Cryptography (ECC)
   Description: ECC is a type of asymmetric cryptography based on the algebraic structure of elliptic curves over finite fields. Bitcoin uses the secp256k1 elliptic curve.
   Role in Bitcoin: ECC allows for the generation of public/private key pairs. The private key is kept secret by the user, and the public key is shared. The public key is used to create Bitcoin addresses, and private keys are used to sign transactions.

4. ECDSA (Elliptic Curve Digital Signature Algorithm)
   Description: ECDSA is a signature algorithm used with elliptic curve cryptography to sign messages. It ensures that the message came from a particular private key holder without revealing the key.
   Role in Bitcoin: Used to sign Bitcoin transactions. Only the owner of the private key associated with a Bitcoin address can create a valid signature for a transaction.

### Why is it required to install an old version of BDB to run Bitcoin? What happens when you don't install BDB and try to run the software?

Bitcoin requires an older version of Berkeley DB (BDB 4.8) to maintain wallet compatibility. Using a newer version can cause wallet corruption or failure to open wallet files. Without installing the correct BDB version, Bitcoin Core may not access or manage the wallet properly

What is a blockchain?
What makes it different
from an array or other
common data types in
programming? When is
blockchain data structure
useful?
