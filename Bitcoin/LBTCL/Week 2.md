# Week 2

## Chapter 4

### 1. What are the different methods for sending Bitcoin transactions using bitcoin-cli?
Bitcoin transactions can be sent using the following methods:
- `sendtoaddress`: Sends Bitcoin to a specified address.
- `sendmany`: Sends Bitcoin to multiple addresses in a single transaction.
- `createrawtransaction` + `signrawtransactionwithwallet` + `sendrawtransaction`: Allows creating, signing, and broadcasting custom raw transactions.

### 2. What is the difference between Legacy and SegWit transactions?
- **Legacy Transactions**: Use older address formats (`P2PKH` and `P2SH`), resulting in higher fees and larger transaction sizes.
- **SegWit Transactions**: Use `P2WPKH` and `P2WSH` formats, reducing transaction size and fees while improving scalability and security.

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
- **RBF**: Allows replacing an unconfirmed transaction with a higher fee version.
- **CPFP**: A child transaction with a high fee incentivizes miners to confirm the parent transaction.

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
- **CPFP risk**: The child transaction needs enough fee to attract miners, or it may also get stuck.

### 17. How do miners prioritize transactions in the mempool?
- Miners prioritize transactions based on the **fee rate (satoshis per byte)**.
- Transactions with the highest fees get confirmed first.