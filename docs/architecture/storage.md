# Storage Architecture

## Purpose

Arkon requires robust persistence for blocks, state, indexes, and validator metadata. Storage must be efficient, crash-safe, and suitable for high-throughput validation.

## 1. Preferred Database

RocksDB is the preferred embedded key-value store for the reference implementation. It provides:

- efficient on-disk storage
- incremental compaction
- strong local performance
- suitability for append-heavy workloads

## 2. Storage Layout

The storage subsystem should maintain separate logical databases:

| Database | Contents |
| --- | --- |
| blocks | Serialized block data keyed by height or hash |
| state | UTXO set and state metadata |
| transactions | Transaction index and metadata |
| accounts | Address and balance-related indexes if needed |
| validators | Validator set and staking records |
| metadata | Chain metadata, version, last finalized height |

## 3. Schema Design

### Blocks

- Key: `(height, block_hash)`
- Value: serialized block bytes

### UTXO Set

- Key: `txid || output_index`
- Value: serialized UTXO object

### Transaction Index

- Key: `txid`
- Value: transaction metadata, included block height, status

## 4. Write Path

When a block is committed:

1. Block bytes are stored
2. New UTXOs are inserted
3. Spent UTXOs are deleted
4. Transaction indexes are updated
5. Validator and metadata state are updated

## 5. Recovery

On startup, the node must:

- open all RocksDB columns
- verify the latest committed state root
- replay any pending or unfinalized metadata if present
- recover from the last checkpoint or snapshot when available

## 6. Snapshots

Snapshots provide fast recovery by capturing a compact state image. They should include:

- latest finalized height
- state root
- UTXO set summary
- validator set state

## 7. Indexing Requirements

Arkon requires efficient lookup for:

- block by height or hash
- transaction by identifier
- UTXO by reference
- validator participation history

## 8. Implementation Guidance

The storage layer should be isolated behind an interface to permit future migration from RocksDB to another backend without changing consensus logic.
