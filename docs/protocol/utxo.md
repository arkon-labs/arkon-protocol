# UTXO Model

## Purpose

This document specifies the Extended UTXO data model used by Arkon and the rules by which outputs are created and consumed.

## 1. UTXO Definition

A UTXO contains:

| Field | Description |
| --- | --- |
| tx_ref | Identifier of the transaction that created the output |
| output_index | Position of the output within that transaction |
| amount | Numeric value of the output |
| owner | Address or public key identity |
| lock | Locking conditions requiring authorization or script-like predicates |

## 2. UTXO Lifecycle

A UTXO is created when a transaction emits an output and destroyed when an input spends it. The ledger state is therefore the set of all currently live UTXOs.

## 3. Invariants

The protocol must enforce:

- no output may be spent more than once
- each spend must reference an existing output
- each spend must satisfy the output’s locking conditions
- output amounts must remain non-negative

## 4. Extended Semantics

The Extended UTXO model allows outputs to carry complex locking conditions beyond simple ownership. This makes the model suitable for future extensions while preserving deterministic and auditable semantics.

## 5. State Representation

The UTXO set is the canonical state representation of the ledger. The state root is computed over the canonical serialization of the current UTXO set, which permits efficient proofs and state verification.
