---
id: Week 6
aliases: []
tags: []
---

# Bitshala Bitcoin study session (Mastering Bitcoin)

## Chapters

- Chapter 11: The Blockchain
- Chapters 12: Mining and Consensus

## Questions

- What is a Light Client in the context of Bitcoin?
  - How do Light Clients verify transactions associated with their addresses?
- What factors could cause a change in Bitcoin’s consensus rules?
  - How is a change in consensus rules achieved in a decentralized network like Bitcoin?

## What is a Light Client in the context of Bitcoin?

In the context of Bitcoin, A Light Client or Simplified Payment Verification (SPV) client is a type of Bitcoin node that downloads only block headers instead of the full blockchain, making it more resource-efficient and suitable for devices with limited storage and processing power.

## How do Light Clients verify transactions associated with their addresses?

### Text Reference

> Merkle trees are used extensively by lightweight clients. Lightweight clients don’t have all transactions and do not download full blocks, just block headers. In order to verify that a transaction is included in a block, without having to download all the transactions in the block, they use a merkle path.

### Steps

- Request Merkle Proof: Light clients request a Merkle proof from full nodes.
- Proof Contents: The Merkle proof includes the transaction's hash and necessary intermediate hashes.
- Compare Merkle Root: They check if the transaction's Merkle root matches the one in the block header.
- Verification Outcome: If they match, the transaction is verified as valid for their address.

## Factors that Could Cause a Change in Bitcoin's Consensus Rules

- Technological Improvements: Advances in technology may propose better security scalability, or functionality enhancements that require changes to the protocol.

- Security Concerns: Discoveries of vulnerabilities or potential attack vectors could prompt changes to strengthen the network's security.

- Scalability Needs: As Bitcoin grows, scalability solutions may be proposed to handle increasing transaction volumes more efficiently.

- Community Consensus: Changes may be driven by consensus among developers, miners, users, and other stakeholders who agree on the need for improvements or adjustments.

- Economic Considerations: Changes may be proposed to better align incentives, address economic issues, or optimize the functioning of Bitcoin as a digital currency.

## How is a change in consensus rules achieved in a decentralized network like Bitcoin?

- **Proposal**: A proposal for a change, often in the form of a Bitcoin Improvement Proposal (BIP),
  is put forward by developers, stakeholders, or the community.

- Discussion and Evaluation: The proposal undergoes thorough discussion and evaluation within the Bitcoin community, including developers, miners, businesses, and users. This stage involves technical analysis, debates, and consideration of potential impacts.

- Testing and Implementation: If consensus begins to form around the proposal, developers and other stakeholders may test the proposed changes in test environments (testnets) to identify and address any issues.

- Activation: Once testing is successful and consensus is broad, the change may be activated on the Bitcoin network. Activation can occur through mechanisms like miner signaling (e.g., with soft forks or miner-activated hard forks) or node adoption (e.g., with user-activated soft forks).

- Adoption: Nodes and miners on the network gradually upgrade their software to enforce the new rules. This ensures that the network remains compatible and that the new rules are universally applied.

- Monitoring and Adjustment: Post-activation, the network monitors the effects of the change. Adjustments may be made if unexpected issues arise, ensuring the network's stability and security.
