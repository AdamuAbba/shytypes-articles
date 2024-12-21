---
id: Week 2
aliases: []
tags: []
---

## Questions:

- How can you verify the signatures of  
   downloaded binaries of Bitcoin Core?  
   What are the potential damages of  
   running a malicious version of the  
   software?

- What are the different private key  
   formats used by wallets?  
   What is the difference between a hot  
   wallet and cold storage?

### ==How can you verify the signatures of downloaded binaries of Bitcoin Core?==

Bitcoin releases are signed by a number of individuals, each with a unique public key

A comprehensive guide can be found here: ==[https://bitcoincore.org/en/download/](https://bitcoincore.org/en/download/)==

==**Hot Point:**==

- download the binary for your platform, the SHA256 digital fingerprint file, and the  
   SHA256 hash digital signature file from `  
[https://bitcoincore.org/bin/bitcoin-core-27.1/bitcoin-27.1-x86_64-linux-gnu.tar.gz](https://bitcoincore.org/bin/bitcoin-core-27.1/bitcoin-27.1-x86_64-linux-gnu.tar.gz)`
- find the digital fingerprint inside the fingerprint file for the downloaded binary
- compare the fingerprint generated using the actual binary with the one in the fingerprint file using the `sha256sum` cli app (linux)

=========================================================================

the fingerprint file is signed by Bitcoin maintainers with their private keys and a digital signature file is generated

=========================================================================

- the public keys of the signers are stored in the `guix.sigs` bitcoin repo which you can then load into your machine via an open-sourced cryptographic tool called `gpg` and then used to verify the downloaded binary.
- The last part would be to verify if the fingerprint file is valid by using the digital signature file

- clone the bitcoin repository containing the public keys of maintainers

  ```Bash
  git clone https://github.com/bitcoin-core

  ```

- Load Maintainers key into GPG
  ```Bash
  gpg --import guix.sigs/builder-keys/*
  ```
- Confirm binary fingerprint
  ```Bash
  sha256sum --ignore-missing --check SHA256SUMS
  ```
- **Verify Signature**: Check the signature with GPG:
  ```Bash
  gpg --verify SHA256SUMS.asc
  ```

### ==Potential Damages of Running a Malicious Version==

- **Loss of Funds**: Theft of private keys and Bitcoin.
- **Compromised Privacy**: Exposure of transaction history and personal information.
- **Network Security Risks**: Disruption of the Bitcoin network and possible double-spending attacks.
- **Data Corruption**: Corrupted blockchain data and transaction history loss.
- **System Security Risks**: Broader system attacks including malware, keyloggers, or ransomware.

### ==What are the different private key formats used by wallets?==

According to the study text, The private key can be represented in a number of different formats, all of which correspond to the same 256-bit number

The text also mentions three formats of Bitcoin private key representation:

**Hexadecimal (Hex)**

- **What It Is**: Hexadecimal is a base-16 representation of the private key.
- **Why Use It**: It's a simple and direct way to represent the 256-bit number that makes up the private key. It's used internally by software for precise and efficient processing.
- **Example**: `1E99423A4ED27608A15A2616C5F46E1ABDC92A7DC1A4466779485B78C12C000F`

**Wallet Import Format (WIF)**

- **What It Is**: WIF is a base58 encoded format that includes the private key, a version byte, and a checksum to detect errors.
- **Why Use It**: WIF makes it easier for users to handle private keys. The base58 encoding reduces the chance of mistyping the key, and the checksum helps detect errors. It's often used for importing and exporting keys between wallets.
- **Example**: `5HueCGU8rMjxEXxiPuD5BDu8NQHQz8rMkKnz8TNBHAdAVJDLH1Z`

**WIF Compressed**

- **What It Is**: Similar to WIF but includes an extra byte to indicate the associated public key should be compressed.
- **Why Use It**: Compressed keys are shorter and lead to smaller transaction sizes, which can save on fees and improve processing times. The WIF compressed format ensures compatibility with wallets that use compressed keys.
- **Example**: `KxBz9XPUGBEThAP6GVq9whEU7fsau7F2bA1YX6S8zY4UN5uHhJw9`

### ==What is the difference between a hot wallet and cold storage?==

- **Hot Wallet:**
  - ==**Hot points:**==
    - A cryptocurrency wallet that is connected to the internet. It is used for frequent transactions and allows quick access to funds.
    - Ease of access for transactions.
    - User-friendly and often integrated with exchanges and mobile apps.
    - Less secure compared to cold storage.
  - **Examples**:
    - Coinbase Walle**t**
    - MetaMask
    - Trust Wallet
- **Cold Storage/Wallet :**
  - ==**Hot points:**==
    - This is an offline Bitcoin wallet i.e. It is not connected to the Internet.
    - Private keys are frequently stored in a secure section of a microcontroller and cannot be sent out in plain text.
    - Greatly reduces the risk of hacking and unauthorized access.
    - Ideal for storing large amounts of cryptocurrency for long periods.
  - **Examples:**
    - Ledger Nano S
    - Ledger Nano X
    - TREZOR
    - paper wallet
