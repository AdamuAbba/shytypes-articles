# Rust solution

**Game Plan**
- Use a hard-coded **tprv** (private key).
- Interacts with locally synced `signet node` via bitcoin-cli commands.
- Calculate the confirmed balance of your wallet.
- Return the balance as a float with 8 decimal places

> [!TIP]
> - import your descriptor into your locally synced signet node and query the balance, then you know the exact right answer. 
> - you can even look through the tx history to see what you did wrong.
> - final output should look like
```rust
println!("{} {:.8}", WALLET_NAME, balance);
```

## A Few Tips That Might Be Helpful

## RECOVER BALANCE

- Make sure that you put the signet challenge in your `bitcoin.conf` file and turn `signet=1` (delete the old signet directory if you ran without the signet challenge).
- To test your balance:
  - Import your descriptor into your locally synced signet node and query the balance.
  - Use the [deriveaddresses](https://chainquery.com/bitcoin-cli/deriveaddresses) RPC call to check if your found pub keys are correct.
- Scan only the first 300 blocks.
- Replace the `EXTENDED_PRIVATE_KEY` variable with the private key you received in the email. Also, ensure that you replace the `WALLET_NAME`.
- The variable `n` in [BIP-0032](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#child-key-derivation-ckd-functions) is the order of the curve, a fixed number for the secp256k1 curve. You can find its value [here](https://en.bitcoin.it/wiki/Secp256k1).
- View any block in the blockchain at: https://boss2025.xyz/block/<blockhash-here>
- View any transaction at:https://boss2025.xyz/tx/<txid/>
- For base58 decoding, refer to: [https://learnmeabitcoin.com/technical/keys/base58/](https://learnmeabitcoin.com/technical/keys/base58/).
- Use [https://iancoleman.io/bip39/](https://iancoleman.io/bip39/) to experiment with key derivation.
- Remember: Derivation for hardened and non-hardened keys is different.
- Write unit tests using the data here: [BIP-0032 Test Vectors](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#test-vectors).

## SPEND
- Refer to this guide for creating and signing a SegWit transaction from scratch: [Creating and Signing a SegWit Transaction](https://medium.com/coinmonks/creating-and-signing-a-segwit-transaction-from-scratch-ec98577b526a).
- Remember to **double SHA256** the elements in the preimage and the preimage itself.
- Changing the amounts from `u32` to `u64` can be helpful in Rust.

**Wallet Name :** wallet_005 
**Descriptor :** 
```
wpkh(tprv8ZgxMBicQKsPeUzfZxrciz9JjbA9NmueNMtUSmgYaP5sDfjFXFGkh8wMxmugcUubK1FteSKxh2VoTYivmzCgoM5XdenGZ6t5qu2yYrjViD7/84h/1h/0h/0/*)#ezjyaqrx
```

> [!TIP]
> **Key Features of Base58:**
> - **Excludes ambiguous characters:** Characters like `0` (zero) and `O` (capital letter O) or `l` (lowercase L) and `I` (uppercase i) are excluded to reduce the chance of errors.
> - **Character set:** Includes uppercase and lowercase letters and digits but skips potentially confusing ones

**child key derivation**
The child key derivation logic changes based on `hardened` vs `normal` 
[https://learnmeabitcoin.com/technical/keys/hd-wallets/extended-keys/](https://learnmeabitcoin.com/technical/keys/hd-wallets/extended-keys/ "https://learnmeabitcoin.com/technical/keys/hd-wallets/extended-keys/")

A hardened child extended private key is created from a parent extended private key using the following steps:
 
1. Use an index between 2147483648 and 4294967295. Indexes in this range are designated for hardened child extended keys.
2. Put data and key through HMAC:
3. data = 0x00 | 32-byte private key | 4-byte index (concatenated)

Deriving the key at path m/84'/1'/0'/0 (BIP84, testnet, first account, external chain) refers to a Bitcoin private key derived using BIP84 (Bitcoin Improvement Proposal 84), which is specifically for native SegWit addresses. The path `m/84'/1'/0'/0`means:

- `84'` - BIP84 purpose (for native SegWit)
- `1'` - testnet coin type
- `0'` - first account
- `0` - external chain (for receiving addresses)

The apostrophes (`'`) indicate hardened derivation, which provides extra security for the derived keys. This derivation path is used to generate a sequence of private keys that will control your Bitcoin testnet wallet addresses.


> [!Note] 
> Don't forget the 0x00 byte prefix. This distinguishes it as a private key and makes the data the same length as when a public key is used instead.
- key = 32-byte chain code



  
## how to derive my wallet balance from UTXOS

Let me explain how to derive your wallet balance from UTXOs (Unspent Transaction Outputs). The process involves:

1. Collecting all your UTXOs (which represent unspent coins)
2. For each UTXO, looking up the transaction it belongs to
3. Getting the value from the specific output in that transaction
4. Summing up all these values

### Pseudo code
1. Initialize `total_balance = 0`
2. Get all UTXOs (unspent transaction outputs) for the wallet:
   - `utxos = fetch_utxos_from_wallet()`

3. Loop through each UTXO in `utxos`:
   - For each `utxo`:
     - a. Fetch the transaction it belongs to:
       - `transaction = get_transaction(utxo.txid)`
     - b. Retrieve the value from the specific output in the transaction:
       - `output_value = transaction.outputs[utxo.output_index].value`
     - c. Add `output_value` to `total_balance`:
       - `total_balance += output_value`

4. Return `total_balance`
