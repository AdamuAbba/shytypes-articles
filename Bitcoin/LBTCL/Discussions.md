# Learn Bitcoin from the Command Line - Discussion Questions

## Week 1

### Chapter 1

**Question 1:** Why is direct interaction with Bitcoin Core and c-lightning via the command line considered more robust and secure compared to using higher-level libraries?

**Answer:**
- Command line interaction offers **more control and transparency** over operations.
- Avoids potential vulnerabilities introduced by higher-level libraries.
- Ensures direct communication with core software without additional dependencies.

---

**Question 2:** How does the decentralization of Bitcoin challenge traditional centralized payment systems?

**Answer:**
- Removes the need for trusted intermediaries like banks or payment processors.
- Enhances censorship resistance, security, and financial sovereignty.
- Provides global access to financial services without geographical restrictions.

---

**Question 3:** What are the potential risks and benefits of working directly with bitcoind and lightningd for cryptocurrency development?

**Answer:**
- **Benefits:**
  - Full control over node operations.
  - Enhanced security and privacy.
  - More precise error handling and debugging.
- **Risks:**
  - Steeper learning curve.
  - Increased responsibility for security.
  - Possibility of making mistakes with serious consequences.

---

**Question 4:** Why is Bitcoin considered pseudonymous rather than fully anonymous?

**Answer:**
- Transactions are recorded on a public ledger (blockchain).  
- Addresses don’t reveal personal identity but can be traced if linked to personal information.
- It’s possible to track transaction flows between addresses.

---

**Question 5:** How does Bitcoin prevent censorship of transactions?

**Answer:**
- Decentralized network of nodes that independently validate transactions.  
- No central authority to block or modify transactions.  
- Use of cryptographic signatures ensures only owners can control their funds.

---

**Question 6:** What is the role of RPC (Remote Procedure Call) in interacting with Bitcoin Core and Lightning?

**Answer:**
- Allows external programs to communicate with Bitcoin Core and lightningd.  
- Provides an interface to perform various operations (e.g., transaction creation, balance checking).  
- Facilitates automation and integration with other software.

## Week 5

### Chapter 12

**Question 1:** How does the Lightning Network differ from the Bitcoin base layer in terms of transaction processing?

**Answer:**
- Uses off-chain payment channels to facilitate transactions.
- Provides instant and low-fee payments by reducing on-chain congestion.
- Settlements are only recorded on-chain when channels are opened or closed.

---

**Question 2:** What are the main advantages of using the Lightning Network compared to traditional Bitcoin transactions?

**Answer:**
- Faster transaction processing.
- Lower fees due to off-chain nature.
- Enhanced privacy as transactions are not publicly recorded on the blockchain.

---

**Question 3:** How do payment channels work within the Lightning Network?

**Answer:**
- Two parties lock funds in a multi-signature address.
- Transactions between them update balances off-chain until channel closure.
- Only the final state is broadcast to the blockchain.

---

**Question 4:** What role do HTLCs (Hashed Time-Locked Contracts) play in enabling multi-hop payments in the Lightning Network?

**Answer:**
- Facilitates payments routed through multiple nodes securely.
- Uses cryptographic hashes and timelocks to ensure successful payment or refund.
- Enhances interoperability within the network.

---

**Question 5:** What are some potential risks associated with using the Lightning Network?

**Answer:**
- Possible channel liquidity issues.
- Reduced security compared to on-chain transactions.
- Potential for routing failures if liquidity is low.

---

**Question 6:** How do Lightning Network nodes differ from Bitcoin Core nodes in terms of operation and purpose?

**Answer:**
- Lightning nodes manage payment channels and route payments.
- Bitcoin Core nodes validate and relay transactions across the blockchain network.
- Different requirements for uptime and connectivity.

---

**Question 7:** What considerations should be made when setting up a Lightning node?

**Answer:**
- Ensuring adequate liquidity for efficient payment routing.
- Balancing privacy, security, and availability.
- Regularly monitoring channel states and managing fees.

---

**Question 8:** How does the use of watchtowers enhance the security of the Lightning Network?

**Answer:**
- Monitors channels for breaches and penalizes malicious actors.
- Provides an extra layer of security for offline users.
- Helps ensure the safety of funds even if a node is temporarily offline.