# Blockchain Model

## Purpose

This document defines the high-level blockchain model used by Arkon. It specifies the ledger representation, state transitions, and invariants that govern how the chain evolves over time.

## 1. Ledger Model

Arkon adopts an Extended UTXO model. The ledger state is not a general account database; instead, it is a set of unspent outputs that can be consumed by future transactions.

A transaction is valid if:

- each input references a currently existing UTXO
- the referenced UTXO is not already spent
- the transaction satisfies the locking conditions of the referenced UTXOs
- signatures are valid
- the resulting state transition is deterministic

## 2. State Transition Function

The global state transition is given by:

$$
S_{n+1} = (S_n \setminus \text{SpentOutputs}) \cup \text{CreatedOutputs}
$$

This transition must be deterministic and must not depend on nondeterministic execution order.

## 3. State Invariants

The following invariants must always hold:

- no UTXO may be spent twice
- every created output has a valid owner and amount
- fees must be non-negative and properly accounted for
- the state root must correspond to the committed UTXO set

## 4. Chain Semantics

The chain is an ordered list of finalized blocks. Each block references its parent and advances the state by applying a deterministic set of transactions.

## 5. Finality Semantics

Once a block is committed, it is final. The protocol does not permit chain reorganization after commit. This property is central to the safety model and supports fast settlement semantics.
