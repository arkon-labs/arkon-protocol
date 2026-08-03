# Protocol Overview

## Purpose

This document defines the core Arkon protocol semantics. It specifies the fundamental objects, state transitions, cryptographic assumptions, consensus rules, and networking behavior that all implementations must follow.

## 1. Protocol Goals

The protocol is designed to provide:

- deterministic execution
- precise transaction semantics
- strong finality
- decentralized validator participation
- clear formal invariants

## 2. Protocol Layers

| Layer | Description |
| --- | --- |
| Ledger | Defines the data model and state transition system |
| Consensus | Defines validator participation, voting, and finalization |
| Cryptography | Defines keys, signatures, hashes, and commitments |
| Networking | Defines peer-to-peer communication and synchronization |
| Economics | Defines staking, fees, and incentives |

## 3. State Model

Arkon uses an Extended UTXO state model. The canonical state is the set of currently spendable outputs. A block transition consumes old UTXOs and creates new ones, preserving deterministic ledger semantics.

## 4. Execution Model

For each block:

1. Transactions are parsed and validated.
2. Inputs are checked against the current UTXO set.
3. Output creation is verified.
4. Fees and metadata are checked.
5. The resulting state root is computed.

## 5. Safety and Liveness

The protocol must satisfy:

- no double spending
- no conflicting finalized blocks at the same height
- eventual progress under synchrony assumptions

## 6. Implementation Requirements

Any conforming implementation must:

- serialize data deterministically
- validate all signatures and proofs
- reject invalid state transitions
- preserve finality after commit
