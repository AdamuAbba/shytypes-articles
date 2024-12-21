## 📜Objective

The goal of this article to help you

- Install and Setup your rust environment
- Learn how to build a very simple rust CLI app to help us understand Bitcoin HD wallet
- Learn about HD wallets
- Advantages and Disadvantages of HD wallets
- Learn a bit about Bip32 and a few it's underlying standards and improvements
  - Bip39
  - Bip44
- Create a HD wallet using the rust CLI app

## Requirements & specs

### Requirements

- Some understanding of the Bitcoin ecosystem
- A working installation of [Bitcoin core](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md)
- Some basic basic knowledge of the Rust Language
- The rust installed and configured on your machine

### ⚙️ My system specs

- Machine: HP elite book
- Operating System: Ubuntu 22.04.4 LTS
- terminal: Gnome Terminal
- shell: ZSH
- Editor: Neovim

## 📜 Introduction

So you recently came across HD wallets and you're a bit curious as to why they are so awesome. furthermore, you're the kind of guy looking for a mini pet rust project to get your hands dirty with some bitcoin rust development. If that sounds like you then you've come to to the right place.

## Setting up your rust and bootstrapping your CLI app

setting up rust on your machine can be done via [rustup](https://rustup.rs/) and is as easy as running the command bellow and following through the prompts if you are on an ubuntu machine or a Mac

```zsh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Now to bootstrap a new rust project run the command below from a convenient directory

```zsh
cargo new shy-bit-rust
```

Let's open up and run the app

```zsh
cd shy-bit-rust && nvim . && cargo run
```

## What are HD wallets (BIP32)

Hierarchical Deterministic wallets as defined by the Bip32 standard are a kind of cryptocurrency wallet that allows for generation of keys from a single seed or mnemonic phrase

## BIP39

The BIP39 standard works by generating a group of 12,18 or 24 random easy-to-remember words called a mnemonic or seed phrase from a random number which is mostly around a length of 128 to 256-bit.

> Quick Note: the more the bits, the stronger the mnemonic phrase and the more words you have in the phrase generated.

![HD wallet](https://global.discourse-cdn.com/business4/uploads/cardano/original/2X/9/93677908b7eed008ae23acad32eb8908f22114df.png =450x300)

_source [forum.cardano.org](https://forum.cardano.org/t/how-an-hd-wallet-works/28460)_

## BIP44

The BIP44 standard is an improvement on the BIP32 protocol by implementing a Multi-Account Hierarchy for Deterministic Wallets

### Structure of the BIP44 derivation path

Let's look at the structure of the BIP44 derivation path below:

m / purpose’ / coin’ / account’ / change / address_index

- m: This is the master private key and represents the root node of your HD wallet.
- purpose': This is set to 44' for BIP44 enabled wallets.
- coin': This value represents the type of cryptocurrency. e.g
  - Bitcoin = 0'
  - Ethereum = 60'
- account': This number represents an account in a BIP44 wallet
- change: This is either 0 for external/receiving addresses or 1 for internal/change addresses.
- address_index: Represents the individual addresses generated under each account.

![BIP44](https://miro.medium.com/v2/resize:fit:720/format:webp/1*eXE-y4lewW42K7XjPR4_Uw.png)

_source: [FoxWallet](https://medium.com/@FoxWallet/bip32-bip39-and-bip44-explained-1e8a4a327a8b)_

## Creating a new wallet in the rust app

Let's create a new HD wallet using the rust app

## Advantages of HD wallets

Now that we know what we have some idea of what HD wallets are, let's look at some advantages

### Deriving Unlimited Wallet Addresses

HD wallets enable the creation of as many addresses as needed, all tied to a single wallet via a child addresses to wallet chain relationship.

### Security & Privacy

HD wallets provide security and protection via the master seed i.e a 12, 18 or 24 word mnemonic phrase from which all the wallet`s private keys are derived.

### Wallet interoperability

One really cool thing about HD wallets is that they can be restored on different devices and wallet applications by simply entering your seed phrase unlike other types of wallets but the only condition is they must support both BIP-39 and BIP-44 standards.

### Single point of ownership

A wise totally real Bitcoin philosopher once said...

![wise rick](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNmdjamRjZGtsMWtzaGk3YzVqcGNma2xhZHBwbHJnYnRmcG1pY3prNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/1USKMDPjuH4ovL7J5h/giphy.gif)

> "Whoever possesses the private keys owns the wallet."

This is valid because all public keys and addresses can be generated from the private keys.

### Disadvantages of HD wallets

On big and obvious concern of working with HD wallets is the fact that the security of your seed or mneomonic phrase getting compromised would naturally imply the lost of ownership to your wallet

### Conclusion

In this aticle we have touched on just 3 out of 389 existing Bips to give you a general view of some of the improvements that have gone into HD wallets over the years to make them more efficient and secure

### useful links

- [Bitcoin/Bips](https://github.com/bitcoin/bips/tree/master)
