# Blockchain Assignment — Flourish
 
 
## 1. What is blockchain?
 
A blockchain is a distributed  digital ledger that records transactions (or data) in a series of linked blocks. Each block contains a batch of transactions, a timestamp, and a cryptographic hash of the previous block, which chains them together in order. Copies of the ledger are maintained across many independent computers in a network. This makes the ledger transparent, tamper-evident, and resistant to a single point of failure or control.
 
## 2. What problems does it solve?
 
- **Trust without intermediaries**: Two parties who don't know or trust each other can transact directly, without relying on a bank, government, or other central authority to validate the exchange.
- **Double-spending**: In digital systems, it's trivial to copy data. Blockchain solves the "double-spend problem" for digital assets by ensuring a unit of value can only be spent once, verified by network consensus.
- **Data tampering / fraud**: Because each block is cryptographically linked to the one before it, altering historical data would require changing every subsequent block across the majority of the network — making tampering computationally impractical.
- **Lack of transparency**: Public blockchains give all participants visibility into transaction history, reducing opportunities for hidden manipulation.
- **Single point of failure**: Since the ledger is replicated across many nodes, there's no single server or entity whose failure or compromise takes down the whole system.
## 3. Which industries can it be used in? (brief examples)
 
- **Finance**: Cryptocurrencies, cross-border payments, decentralized finance (DeFi) — e.g., Bitcoin for peer-to-peer digital cash, or DeFi lending platforms that remove the need for a bank.
- **Supply chain**: Tracking goods from origin to consumer to verify authenticity and reduce fraud — e.g., tracing the origin of coffee beans or diamonds.
- **Healthcare**: Secure, tamper-proof storage and sharing of patient records across providers.
- **Real estate**: Recording property titles and automating transfers via smart contracts, reducing paperwork and fraud.
- **Voting**: Creating verifiable, tamper-resistant digital voting records.
- **Identity management**: Giving individuals self-sovereign digital identities that they control, rather than relying on centralized databases.

## 4. What is encryption?
 
Encryption is the process of converting readable data into an unreadable, scrambled format using an algorithm and a key, so that only someone with the correct key can convert it back  into its original form. 

## 5. What is a hash function?
 
A hash function is a mathematical algorithm that takes an input  and produces a fixed-size string of characters called a hash  that appears random.

 
## 6. What is on-chain?
 
On-chain refers to any data or action that is recorded directly on the blockchain itself. 
 
## 7. What is a Merkle tree?
 
A Merkle tree is a data structure used to verify the integrity of large sets of data. It represents the entire set of underlying data. If even a single transaction changes, its hash changes. Blockchains store the Merkle root in each block header to efficiently verify that all transactions in that block are intact.
 
## 8. Bonus: Given a Merkle tree already built from four transactions (Ha, Hb, Hc, Hd), how would you add a fifth transaction (He) to the tree without tampering with the existing transactions?
 
Starting tree (4 transactions):
```
                Root
              /      \
          H(AB)        H(CD)
          /    \        /    \
        Ha     Hb     Hc     Hd
```
 
To add a fifth transaction (He) **without altering** Ha, Hb, Hc, or Hd themselves:
 
1. **Hash the new transaction** to get He, just like the others.
2. Since Merkle trees are typically built by pairing nodes, an odd number of leaves (5) is usually handled by **duplicating the last leaf** to make the count even, or by carrying the unpaired node up unchanged to the next level.:
   - Duplicate He to pair with itself: `H(EE) = Hash(He + He)`
3. **Rebuild the tree levels above** using the original (unchanged) pairs plus the new one:
```
                     New Root
                   /          \
              H(ABCD)         H(EE)
              /      \            
          H(AB)      H(CD)
          /   \        /   \
        Ha    Hb     Hc    Hd
```
