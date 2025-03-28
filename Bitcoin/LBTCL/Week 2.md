# Week 2

## Chapter 4

### 1. What are the different methods for sending Bitcoin transactions using bitcoin-cli?
Bitcoin transactions can be sent using the following methods:
- `sendtoaddress`: Sends Bitcoin to a specified address.
- `sendmany`: Sends Bitcoin to multiple addresses in a single transaction.
- `createrawtransaction` + `signrawtransactionwithwallet` + `sendrawtransaction`: Allows creating, signing, and broadcasting custom raw transactions.

### 2. # Difference Between Legacy and SegWit Transactions

## 🔹 Legacy Transactions (P2PKH & P2SH)
- The **original Bitcoin transaction format**.
- Uses **Pay-to-Public-Key-Hash (P2PKH)** or **Pay-to-Script-Hash (P2SH)** addresses.
- Example address format: **`1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`**.
- Stores **signatures inside the main transaction data**, increasing transaction size.
- **Higher fees** due to larger transaction sizes.
- Less efficient for block space usage.

## 🔹 SegWit Transactions (P2WPKH & P2WSH)
- Introduced with the **Segregated Witness (SegWit) upgrade in 2017**.
- Uses **Pay-to-Witness-Public-Key-Hash (P2WPKH)** or **Pay-to-Witness-Script-Hash (P2WSH)** addresses.
- Example address format: **`bc1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`**.
- **Separates witness (signature) data** from the main transaction.
- **Smaller transaction size**, leading to **lower fees**.
- **Fixes transaction malleability**, enabling features like **Lightning Network**.

## 🔹 Key Differences
| Feature | Legacy (P2PKH/P2SH) | SegWit (P2WPKH/P2WSH) |
|---------|------------------|------------------|
| Address Format | Starts with `1` (P2PKH) or `3` (P2SH) | Starts with `bc1` |
| Transaction Size | Larger | Smaller |
| Fees | Higher | Lower |
| Malleability Fix | ❌ No | ✅ Yes |
| Block Space Efficiency | ❌ Less Efficient | ✅ More Efficient |
| Lightning Network Support | ❌ No | ✅ Yes |

## 📌 Example: Checking if a Transaction is SegWit
```sh
bitcoin-cli getrawtransaction "<txid>" 1
```
- If **`"vsize"` is significantly smaller than `"size"`**, it’s a SegWit transaction.

---

## 🚀 Why Use SegWit?
- **Lower transaction fees** 💰.
- **More transactions per block** ⛓️.
- **Enables Lightning Network** ⚡ for faster payments.
- **Improves network scalability** 📈.



### 3. How do transaction fees work, and how are they determined?
- Fees are based on transaction size (in bytes) rather than amount sent.
- Higher fees prioritize transactions for faster confirmation.
- Wallets estimate fees based on network congestion and past transaction data.

### 4. What are the risks and dangers associated with raw transactions?
- **Manual errors**: Incorrect inputs/outputs can result in lost funds.
- **Malicious transactions**: Can be crafted to exploit vulnerabilities.
- **No automatic fee calculation**: Requires careful selection to avoid low-fee stuck transactions.

### 5. How can you use bitcoin-cli to send Bitcoin in the simplest way?
- Use `sendtoaddress "address" amount` for a quick transaction.
- Example:
  ```sh
  bitcoin-cli sendtoaddress "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa" 0.01
  ```

### 6. What are the benefits of using named arguments when creating raw transactions?
- Improves readability and clarity.
- Reduces errors by specifying parameters explicitly.
- Enhances automation by making scripts more maintainable.

### 7. How can automation be used to send raw Bitcoin transactions?
- Use shell scripts or Python to generate, sign, and broadcast transactions.
- Example: Automating `bitcoin-cli createrawtransaction` with predefined inputs/outputs.

### 8. How does jq help when working with Bitcoin transactions?
- `jq` is a command-line JSON processor that formats and filters Bitcoin transaction data.
- Useful for parsing `bitcoin-cli` JSON output to extract specific fields.

### 9. What role does curl play in sending Bitcoin transactions via command-line tools?
- `curl` can interact with Bitcoin Core’s RPC interface.
- Example:
  ```sh
  curl --user user:password --data-binary '{"method": "sendtoaddress", "params": ["address", 0.01]}' -H "content-type: text/plain;" http://127.0.0.1:8332/
  ```

## Chapter 5

### 10. What is the mempool, and how does it affect Bitcoin transactions?
- The mempool is a pool of unconfirmed transactions waiting to be mined.
- Transactions with higher fees get prioritized.
- Network congestion can lead to longer confirmation times.

### 11. How do Replace-By-Fee (RBF) and Child-Pays-For-Parent (CPFP) mechanisms differ in resolving unconfirmed transactions?

### 🔹 How Replace-By-Fee (RBF) Works in Bitcoin

**Replace-By-Fee (RBF)** allows you to **increase the fee** of an unconfirmed Bitcoin transaction by **sending a new version** of the same transaction with a higher fee.

---

### ✅ How RBF Works – Step by Step

1. **Enable RBF when creating a transaction**  
   - When you first send a transaction, you must **opt-in to RBF** by setting the **nSequence** field to a value below `0xFFFFFFFF`.  

   📌 **Example using `bitcoin-cli`**
   ```sh
   bitcoin-cli sendtoaddress "recipient_address" 0.01 '{"replaceable": true}'
   ```

2. **Transaction gets stuck in the mempool**  
   - If the original transaction **has a low fee**, it may **not get picked up by miners** quickly.  

3. **Create a new transaction with a higher fee**  
   - The sender **resends the same transaction** but with:  
     - **Same inputs**  
     - **Same (or updated) outputs**  
     - **Higher fee**  

   📌 **Using `bumpfee` in `bitcoin-cli`**
   ```sh
   bitcoin-cli bumpfee "txid"
   ```
   - This command automatically increases the fee and rebroadcasts the new transaction.

4. **Miners accept the higher-fee transaction**  
   - The original **low-fee transaction is dropped** from the mempool.  
   - The **new transaction with a higher fee is confirmed faster**.  

---

### 🔍 Key Requirements for RBF
✅ The original transaction **must be RBF-enabled** (`nSequence` < `0xFFFFFFFF`).  
✅ The sender **must control the inputs** to create a replacement.  
✅ The **new transaction must pay a higher fee** (otherwise, miners ignore it).  

# How Does Child-Pays-For-Parent (CPFP) Work?

## 🔹 What is CPFP?
Child-Pays-For-Parent (CPFP) is a Bitcoin transaction fee bumping technique where a **new transaction (child)** with a **higher fee** incentivizes miners to confirm a **previous unconfirmed transaction (parent)**.

## ✅ How CPFP Works
1. **A transaction (parent) is stuck** due to a low fee.
2. **A new transaction (child) is created**, spending an output from the parent transaction.
3. The child transaction **includes a very high fee**.
4. **Miners prioritize** transactions with the highest total fee.
5. Since the child **depends on the parent**, miners confirm **both together** to collect the fees.

---

## 📌 Example Scenario  
1. **Check if your transaction is unconfirmed:**  
   ```sh
   bitcoin-cli getrawtransaction "<parent_txid>" 1
   ```  
   - If `"confirmations": 0`, it's stuck.

2. **Find an unspent output (UTXO) from the parent transaction:**  
   ```sh
   bitcoin-cli listunspent
   ```  
   - Look for an output from the **stuck parent transaction**.

3. **Create a new (child) transaction using the unspent output:**  
   ```sh
   bitcoin-cli createrawtransaction '[{"txid": "<parent_txid>", "vout": <vout_index>} ]' '[{"address": "<your_address>", "amount": <btc_amount>}]'
   ```  
   - The **amount** should be lower than the input to allow for a **high fee**.

4. **Sign the child transaction:**  
   ```sh
   bitcoin-cli signrawtransactionwithwallet "<raw_child_tx>"
   ```  

5. **Broadcast the child transaction:**  
   ```sh
   bitcoin-cli sendrawtransaction "<signed_child_tx>"
   ```  

6. **Now miners will confirm both transactions together! 🚀**

---

## 🔍 CPFP vs. RBF
| Feature | CPFP | RBF |
|---------|------|-----|
| Who initiates? | Receiver or another party | Sender |
| How it works? | Creates a high-fee child transaction | Replaces the original transaction with a higher fee |
| Requires RBF flag? | ❌ No | ✅ Yes |
| When to use? | If you can’t modify the parent tx | If you control the original tx |

---

## 🚀 When to Use CPFP
- The sender **didn’t enable RBF**, so you can’t replace the transaction.
- You have **access to an unconfirmed output** from the parent transaction.
- You want to **speed up confirmation** without waiting for the sender.



---

### 12. How do you determine if a Bitcoin transaction is stuck?
- Check mempool status using `bitcoin-cli getmempoolentry txid`.
- If it's in the mempool for a long time with low fees, it's likely stuck.

### 13. How does RBF help in modifying an unconfirmed transaction?
- Allows rebroadcasting the same transaction with a higher fee.
- Requires the original transaction to have `RBF` enabled.

### 14. How does CPFP allow a child transaction to push a parent transaction through?
- A high-fee child transaction spends unconfirmed outputs from a low-fee parent.
- Miners prioritize the pair since they want the combined fees.

### 15. When should you use RBF versus CPFP?
- Use **RBF** when you control the original transaction and can increase the fee.
- Use **CPFP** when you don’t control the parent transaction but can create a child.

### 16. What are the risks of using RBF and CPFP?
- **RBF risk**: Merchants may reject transactions due to potential fee bumps.
- you could miscalculate and overpay for a transaction.
- **CPFP risk**: The child transaction needs enough fees to attract miners, or it may also get stuck.

### 17. How do miners prioritize transactions in the mempool?

## 🔹 1. Transaction Fees (sats/vByte)  
- The **higher the fee rate** (satoshis per virtual byte), the **higher the priority**.  
- Miners aim to maximize their rewards by picking transactions with the **best fee-to-size ratio**.  

## 🔹 2. Replace-By-Fee (RBF)  
- If a transaction is **RBF-enabled**, it can be **replaced with a higher-fee version**.  
- Miners prefer the **latest, highest-fee** version of an RBF transaction.  

## 🔹 3. Child-Pays-For-Parent (CPFP)  
- If a **low-fee parent transaction** has a **high-fee child transaction**, miners may confirm both to collect the total fees.  
- This encourages miners to process **otherwise low-fee transactions**.  

## 🔹 4. Transaction Age  
- Some miners **prioritize older transactions** if they’ve been stuck in the mempool for a long time.  
- However, this varies by mining pool policies.  

## 🔹 5. Transaction Size (Weight Units - WU)  
- **Smaller transactions** (in bytes) are easier to confirm.  
- **Larger transactions** (e.g., multi-sig or complex scripts) need **higher fees** to compete.  

## 🔹 6. Mempool Policy & Mining Pool Rules  
- Each mining pool **sets its own rules** for prioritization.  
- Some pools may **filter out** very low-fee transactions.  

---

## 📌 Example: Checking Mempool Priority via bitcoin-cli  
```sh
bitcoin-cli getmempoolinfo
```
- This command shows mempool usage and fee rates.  

```sh
bitcoin-cli getrawmempool true
```
- This gives details on pending transactions, including fees.  

---

## 🚀 How to Get Your Transaction Prioritized?  
- **Increase your fee rate (sats/vByte)** when sending.  
- Use **RBF** so you can **bump fees later** if needed.  
- If receiving, try **CPFP** to attach a high-fee child transaction.  

