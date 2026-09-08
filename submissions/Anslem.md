# Blockchain Basics

## 1. What is blockchain?

A blockchain is a distributed, append-only ledger made up of "blocks" of data (usually transactions) that are linked together in chronological order. Each block contains a cryptographic hash of the previous block, a timestamp, and its own transaction data. This chaining means that altering any past block would change its hash and break the link to every block after it — making the ledger tamper-evident.

Instead of being stored on one central server, copies of the ledger are held by many independent nodes across a peer-to-peer network. These nodes use a consensus mechanism (e.g., Proof of Work, Proof of Stake) to agree on which new blocks are valid before they're added, so no single party can unilaterally rewrite history.

## 2. What problems does it solve?

- **Trust between strangers without a middleman** — two parties who don't trust each other can transact directly, with the network (not a bank or broker) verifying validity.
- **Double-spending** — prevents the same digital asset from being spent twice, which was previously only solvable by a trusted central authority.
- **Single points of failure/control** — no single server or company can unilaterally alter records or shut the system down.
- **Data tampering** — cryptographic linking + consensus make retroactive changes to historical records computationally impractical.
- **Lack of transparency/auditability** — all participants can independently verify the full transaction history.
- **Slow, costly intermediated transfers** — can reduce friction in cross-border payments and settlement.
- **Provenance and counterfeiting** — makes it possible to track an asset's full history immutably.

## 3. Which industries can it be used in? (brief examples)

- **Finance** — cryptocurrencies, decentralized finance (DeFi) lending/trading, faster cross-border settlement.
- **Supply chain** — tracking goods from origin to shelf (e.g., food safety and provenance tracking).
- **Healthcare** — secure, auditable sharing of patient records and pharmaceutical supply verification.
- **Real estate** — recording property titles and enabling fractional ownership via tokenization.
- **Voting** — tamper-evident, auditable election or governance systems.
- **Intellectual property / media** — proving ownership and provenance of digital assets (NFTs, licensing).
- **Insurance** — smart contracts that auto-execute payouts when verifiable conditions are met.
- **Identity management** — self-sovereign digital identity that isn't controlled by one company.

## 4. What is encryption?

Encryption is the process of transforming readable data ("plaintext") into an unreadable form ("ciphertext") using an algorithm and a key, so that only someone holding the correct key can reverse the process (decrypt it) and read the original data. Its purpose is **confidentiality** — keeping data secret from anyone who intercepts it.

- **Symmetric encryption**: the same key is used to encrypt and decrypt (fast, but the key must be shared securely).
- **Asymmetric encryption**: a public key encrypts and a separate private key decrypts (used for secure key exchange and digital signatures).

Encryption is reversible by design (with the key); this is a key difference from hashing.

## 5. What is a hash function?

A hash function takes an input of any size and deterministically produces a fixed-size output called a **hash** (or digest). Cryptographic hash functions (e.g., SHA-256, used in Bitcoin) have several important properties:

- **Deterministic** — the same input always produces the same output.
- **Fast to compute** in one direction.
- **Pre-image resistant** — infeasible to reconstruct the original input from the hash.
- **Avalanche effect** — a tiny change in input produces a completely different, unpredictable output.
- **Collision resistant** — extremely unlikely for two different inputs to produce the same hash.

Unlike encryption, hashing is **one-way** — there's no key to "unhash" it. In blockchain, hashing links blocks together, secures transaction data, and underpins mining/consensus (Proof of Work) and Merkle trees.

## 6. What is "on-chain"?

"On-chain" refers to any data, transaction, or action that is recorded directly on the blockchain itself and validated through the network's consensus process. On-chain data is immutable, transparent, and verifiable by anyone running a node.

This is contrasted with **off-chain**: activity or data that happens outside the main ledger (e.g., a side channel, a second layer like the Lightning Network, or a database an oracle later feeds into the chain) — usually done to reduce cost or increase speed, at the cost of some of the blockchain's guarantees until/unless it's settled on-chain.

## 7. What is a Merkle tree?

A Merkle tree (hash tree) is a binary tree used to efficiently and securely summarize a large set of data, such as all the transactions in a block.

- Each **leaf node** is the hash of one piece of data (e.g., a single transaction).
- Each **non-leaf (parent) node** is the hash of the concatenation of its two children's hashes.
- This repeats up to a single top hash called the **Merkle root**.

Benefits:
- The Merkle root uniquely and compactly represents the entire dataset — if any transaction changes, the root changes.
- It enables a **Merkle proof**: you can prove a specific transaction is included in a block by providing only a small number of hashes (the "sibling" hashes along the path to the root), without needing the entire dataset. This is what allows lightweight ("SPV") clients to verify transactions without downloading the full blockchain.

**Example with four transactions:**

```
                Root = H(Hab + Hcd)
               /                   \
        Hab = H(Ha+Hb)        Hcd = H(Hc+Hd)
        /          \            /          \
      Ha           Hb          Hc          Hd
      |            |           |           |
     Tx_a         Tx_b        Tx_c        Tx_d
```

## 8. Bonus: Adding a fifth transaction (He) without tampering with the existing tree

Starting tree (from four transactions):

```
Level 0 (leaves):  Ha    Hb    Hc    Hd
Level 1:           Hab = H(Ha,Hb)     Hcd = H(Hc,Hd)
Level 2 (root):     Root = H(Hab, Hcd)
```

To add a fifth transaction's hash, **He**, none of the existing leaf hashes (Ha–Hd) or their original relationships are altered — you don't edit any existing data. Instead, you extend the structure so it accommodates an odd number of leaves, which produces a new root:

1. **Add He as a new leaf**, giving five leaves total: Ha, Hb, Hc, Hd, He.
2. Since five is odd, standard implementations (e.g., Bitcoin's approach) handle the unpaired node by **duplicating it** to form a pair at each level where an odd count occurs:
   - Pair He with itself: `Hee = H(He, He)`
3. **Rebuild the level above** the leaves:
   - `Hab = H(Ha, Hb)` — unchanged, since Ha and Hb didn't change.
   - `Hcd = H(Hc, Hd)` — unchanged, since Hc and Hd didn't change.
   - `Hee = H(He, He)` — new.
4. Now there are three nodes at this level (Hab, Hcd, Hee) — odd again, so duplicate the last one once more:
   - `Habcd = H(Hab, Hcd)`
   - `Heeee = H(Hee, Hee)`
5. **Compute the new root:**
   - `New Root = H(Habcd, Heeee)`

Resulting tree:

```
                         New Root = H(Habcd, Heeee)
                        /                          \
        Habcd = H(Hab, Hcd)                 Heeee = H(Hee, Hee)
         /            \                              |
   Hab=H(Ha,Hb)   Hcd=H(Hc,Hd)                Hee = H(He, He)
    /      \        /      \                          |
  Ha       Hb      Hc      Hd                         He
```

**Key point:** The original transactions and their hashes (Ha, Hb, Hc, Hd) — and the sub-hashes built from them (Hab, Hcd) — are never recomputed from different data or edited; they're only reused as inputs to new parent hashes. The Merkle **root** naturally changes because the tree now represents five transactions instead of four, but that's an expected structural update, not tampering (tampering would mean changing what Ha–Hd actually hash to, i.e., altering the original transactions).

*Note: in production systems, if the total number of transactions is fixed in advance and large, trees are often rebuilt fresh per block rather than incrementally patched — the duplication method above is the standard way to handle an odd leaf count within a single Merkle tree construction, including when patching in a new transaction like this.*
