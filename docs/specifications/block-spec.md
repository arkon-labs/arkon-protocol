# Block Specification

## 1. Scope

This specification defines the format and validation criteria for Arkon blocks.

## 2. Block Format

A block consists of a header and a body.

### Header

| Field | Type | Description |
| --- | --- | --- |
| version | uint8 | Protocol version |
| height | uint64 | Block height |
| timestamp | uint64 | Block timestamp |
| prev_hash | bytes32 | Parent block hash |
| merkle_root | bytes32 | Merkle root of transactions |
| state_root | bytes32 | Root of resulting state |
| validator_sig | bytes | Validator signature or quorum evidence |

### Body

The body contains the transaction list.

## 3. Validation

A block is accepted only if:

- the parent block is known
- the height is exactly one greater than the parent
- the transaction list is valid
- the merkle root is correct
- the state root is correct
- the validator signature is valid

## 4. Hashing

The canonical block hash is computed with BLAKE3 over the canonical serialization of the full block.

## 5. Persistence

Blocks must be stored in a deterministic append-only format that supports random access by height and hash.
