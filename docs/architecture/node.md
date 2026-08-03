# Node Architecture

## Scope

The Arkon node is the execution environment for the protocol. It must be capable of participating in networking, validating transactions, producing blocks, storing state, and serving RPC clients.

## 1. Module Responsibilities

| Module | Responsibility |
| --- | --- |
| blockchain | Maintains chain metadata, block history, and canonical tip selection |
| transaction | Parses, validates, signs, and executes transactions |
| utxo | Tracks spendable outputs and enforces UTXO invariants |
| crypto | Provides hashing, key generation, Merkle proofs, signatures, and commitments |
| consensus | Implements proposal, prevote, precommit, commit, and view change logic |
| network | Manages peer connections, message handling, and synchronization |
| storage | Persists state, blocks, indexes, and snapshots to disk |
| mempool | Holds pending transactions until inclusion in a block |
| rpc | Exposes JSON-RPC or gRPC interfaces for wallet and client integration |
| wallet | Derives addresses, manages keys, and assembles signed transactions |
| staking | Records bonded stake and validator participation |
| slashing | Penalizes double signing, downtime, and invalid blocks |
| governance | Handles parameter changes and validator governance actions |
| metrics | Emits counters, gauges, and traces for observability |

## 2. Node Lifecycle

1. Startup
   - Load configuration
   - Initialize cryptographic primitives
   - Open storage and databases
   - Connect to bootstrap peers
2. Synchronization
   - Retrieve recent blocks and state from peers
   - Rebuild UTXO state and indexes
3. Validation
   - Process mempool transactions and incoming blocks
4. Participation
   - Propose, vote, and finalize blocks when selected as validator
5. Service
   - Respond to RPC and network requests

## 3. Internal Interfaces

The node should expose internally consistent interfaces so that each module consumes only the data it needs:

- `consensus -> blockchain` for new block acceptance
- `transaction -> utxo` for spend verification
- `network -> mempool` for transaction gossip
- `storage -> blockchain` for block retrieval
- `wallet -> crypto` for key operations

## 4. Determinism Requirements

All modules must be deterministic with respect to the same input state and serialized data. The node must not rely on nondeterministic ordering unless explicitly defined by the protocol.

## 5. Operational Requirements

The node must support:

- clean restart and recovery
- fast boot from snapshots
- graceful handling of peer disconnects
- metrics reporting for block production and validation
