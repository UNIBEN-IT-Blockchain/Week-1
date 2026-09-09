# Blockchain Assignment — skodeesam
 

 
## 1. What is blockchain?
 
Blockchain is a decentralized digital ledger used to record and store transactions or information in a secure and transparent way. The information is stored in groups called blocks, and each block is linked to the previous block using cryptographic hashes. Because copies of the blockchain are maintained across multiple computers, it is difficult for one person to secretly alter the records.
 
## 2. What problems does it solve?
 
Blockchain helps solve problems such as lack of trust between parties, data tampering, and the need for a central authority to verify transactions. It provides a way for people or organizations to share records and verify transactions without relying entirely on a single central authority. It can also improve transparency, traceability, and security.
 
## 3. Which industries can it be used in? (brief examples)
 
Blockchain can be used in many industries, including:

Finance: For cryptocurrencies, payments, and secure financial transactions.
Healthcare: For securely sharing and managing medical records.
Supply Chain: For tracking products from their origin to the customer.
Real Estate: For recording property ownership and transactions.
Voting: For creating transparent and verifiable voting systems.
Education: For storing and verifying academic certificates and credentials.
 
## 4. What is encryption?
 
Encryption is the process of converting readable information (plaintext) into an unreadable form (ciphertext) using an encryption method and usually a key. Only someone with the appropriate key or method can decrypt the information and read the original data. Encryption is commonly used to protect sensitive information such as passwords, messages, and financial data.
 
## 5. What is a hash function?
 
A hash function is a mathematical function that takes input data of any size and produces a fixed-length string of characters called a hash. A small change in the input normally produces a completely different hash. Hash functions are designed to be one-way, meaning it should be extremely difficult to recover the original input from the hash. Blockchain uses hash functions to link blocks and protect the integrity of data.
 
## 6. What is on-chain?
 
On-chain refers to data or transactions that are recorded directly on a blockchain. Once an on-chain transaction is confirmed and included in the blockchain, it becomes part of the public ledger and can be verified by the network. For example, a cryptocurrency transfer that is recorded on the blockchain is an on-chain transaction.
 
## 7. What is a Merkle tree?
 
A Merkle tree is a data structure used to efficiently and securely verify data stored in a blockchain block. It starts with the hashes of individual transactions, called leaf nodes. These hashes are combined and hashed repeatedly until one final hash remains, called the Merkle root
 
## 8. Bonus: Given a Merkle tree already built from four transactions (Ha, Hb, Hc, Hd), how would you add a fifth transaction (He) to the tree without tampering with the existing transactions?
 
First, I would keep the existing transaction hashes, Ha, Hb, Hc, and Hd, unchanged and calculate the hash of the new transaction, He.

The existing tree can be represented as:

H_ab = Hash(Ha + Hb)
H_cd = Hash(Hc + Hd)
Root = Hash(H_ab + H_cd)

To add He, I would add it as a new leaf and rebuild only the necessary parts of the Merkle tree. Since there are now five leaves, the tree has an odd number of nodes. A common Merkle tree approach is to duplicate the last hash at that level when there is no pair. Therefore, He can be paired with itself:

H_ee = Hash(He + He)

The new root can then be calculated from the existing branches and the new branch according to the Merkle tree's structure.

The important point is that the original transactions Ha, Hb, Hc, and Hd are not changed or modified. Only the hashes needed to incorporate He and the resulting Merkle root are recalculated. The exact handling of an odd number of transactions can vary depending on the blockchain's Merkle tree implementation.
 
