# State Machine Specification

## Purpose

This document defines the Arkon state machine, including state representation, transition rules, and commit semantics.

## 1. State Components

The state machine consists of:

- UTXO set
- validator set
- staking state
- governance state
- chain metadata

## 2. Transition Function

For each block, the state transition is:

$$
\text{State}_{i+1} = \mathcal{T}(\text{State}_i, \text{Block}_i)
$$

The transition applies the block’s transactions to the existing state and produces a new state root.

## 3. Validity Rules

State transitions are valid only if:

- all transactions are valid under the current state
- no double spending occurs
- all signatures and proofs verify
- the resulting state root matches the block header

## 4. Determinism

The state machine must be deterministic. Two correct nodes operating from the same initial state and the same block sequence must reach the same state.

## 5. Commit Semantics

A block is committed only after the consensus algorithm reaches the required quorum. Once committed, its state transition is considered finalized and is applied to the canonical state.
