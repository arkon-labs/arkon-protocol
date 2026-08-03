# Block Specification

## Purpose

This document specifies the structure and validation rules for Arkon blocks. Blocks are the atomic units of ledger progression and consensus agreement.

## 1. Block Structure

A block consists of:

- a header
- a body containing a list of transactions

### 1.1 Block Header

| Field | Type | Description |
| --- | --- | --- |
| version | uint8 | Protocol version |
| height | uint64 | Canonical block height |
| timestamp | uint64 | Unix timestamp in milliseconds |
| prev_hash | bytes32 | Hash of the parent block |
| merkle_root | bytes32 | Merkle root of transactions |
| state_root | bytes32 | Root of post-state after applying block |
| validator_sig | bytes | BLS12-381 signature from the proposer or validator quorum |

### 1.2 Block Body

The block body contains:

- transaction list
- optional metadata for consensus context

## 2. Serialization Format

The block format should be serialized using a deterministic binary encoding. The recommended structure is:

- fixed-size fields for integers and hashes
- length-prefixed fields for variable-size data
- canonical ordering for maps and lists

## 3. Hashing

The block hash is computed over the canonical serialization of the header and the body. The default hash function is BLAKE3.

## 4. Validation Rules

A block is valid only if:

- the parent exists
- the height increments by one from the parent
- the timestamp is not earlier than the parent by a protocol-defined tolerance
- the merkle_root matches the transactions in the body
- the state_root matches the resulting state transition
- the validator signature or quorum evidence is valid

## 5. Storage Requirements

Blocks should be stored in a compact, append-only log. The node must retain:

- block bytes
- block header metadata
- transaction references
- state root data

## 6. Implementation Notes

The implementation should separate block parsing, block validation, and block persistence so that validation logic is independent of storage concerns.
