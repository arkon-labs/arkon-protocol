# Cryptography Specification

## Purpose

This document defines the cryptographic primitives and procedures used by Arkon across wallets, validator operations, block commitments, and proofs.

## 1. Primitives

| Primitive | Usage |
| --- | --- |
| Ed25519 | Transaction signatures and wallet authorization |
| BLS12-381 | Aggregated validator consensus signatures |
| BLAKE3 | Hashing, commitments, and Merkle tree construction |
| Binary Merkle Tree | Inclusion proofs and transaction commitment |

## 2. Key Generation

Each wallet or node identity must generate keys according to the following process:

1. Generate a private key using the specified scheme.
2. Derive the corresponding public key.
3. Derive the address from the public key using a canonical hash-based encoding.

## 3. Address Derivation

An address is derived from:

- the public key
- a namespace or network tag
- a hash digest over the canonical byte representation

## 4. Transaction Signing

A transaction signature is computed over the canonical serialization of the transaction body. The signature must be verified using the public key associated with the spent output owner.

## 5. Validator Signatures

Validators submit consensus signatures using BLS12-381. The protocol may aggregate signatures across validators to produce compact quorum evidence.

## 6. Merkle Proofs

Merkle proofs must be computed over a binary tree of transaction hashes. A proof is valid if the recomputed root matches the block’s merkle_root.

## 7. Commitments

All state commitments and block commitments must be derived using canonical serialization and the protocol-defined hash function.

## 8. Security Requirements

The cryptographic subsystem must:

- reject malformed signatures
- use canonical serialization for all signed payloads
- avoid ambiguity in address encoding
- ensure all proofs are deterministic and verifiable
