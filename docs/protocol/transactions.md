# Transaction Specification

## Purpose

This document defines the Arkon transaction format, validation rules, signing semantics, and execution behavior.

## 1. Transaction Structure

A transaction contains:

| Field | Description |
| --- | --- |
| inputs | References to previously unspent outputs |
| outputs | Newly created outputs |
| metadata | Optional transaction metadata, such as expiry or tags |
| fee | Transaction fee paid to the network |
| signatures | Authorization from the owners of the spent inputs |

## 2. Input Semantics

Each input includes:

- previous transaction reference
- output index
- unlocking data
- signature or witness data

## 3. Output Semantics

Each output includes:

- amount
- owner address
- locking conditions

## 4. Validation Rules

A transaction is valid if:

- all referenced inputs exist in the current UTXO set
- none of the referenced UTXOs has already been spent
- the signatures are valid for the referenced input owners
- the fee is non-negative and is paid by the spender
- the outputs satisfy the protocol’s serialization and size limits

## 5. Signature Scheme

Arkon uses Ed25519 for transaction authorization. Each input owner must provide a valid signature over the canonical transaction body.

## 6. Deterministic Execution

The transaction must be executed deterministically. Given the same prior state and identical serialized transaction bytes, all honest nodes must derive the same resulting outputs and state changes.

## 7. Transaction Identifier

The transaction identifier is computed as the BLAKE3 hash of the canonical serialized transaction bytes.

## 8. Implementation Guidance

The transaction module should enforce:

- strict canonical serialization
- signature verification before state mutation
- fee accounting before inclusion in a block
