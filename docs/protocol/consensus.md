# Consensus Specification

## Purpose

This document defines the Byzantine Fault Tolerant consensus algorithm used by Arkon. The protocol is designed to provide deterministic agreement, fast finality, and explicit quorum semantics.

## 1. Consensus Model

Arkon uses a Tendermint-style consensus protocol with Proof-of-Stake validator participation. The protocol proceeds through five logical phases:

1. Proposal
2. Prevote
3. Precommit
4. Commit
5. Finalization

## 2. Validator Model

Validators are selected using weighted round-robin proposer scheduling based on stake. The system assumes:

$$
n = 3f + 1
$$

where $n$ is the total validator voting power and $f$ is the maximum tolerated Byzantine validator set. A block is committed when more than $2/3$ of voting power participates in the required decision phase.

## 3. Voting Rules

Validators may cast:

- a vote for a proposed block
- a nil vote when the proposal is invalid or unavailable

The protocol requires a supermajority of voting power to progress from prevote to precommit and from precommit to commit.

## 4. Finality

A committed block is final immediately. No chain reorganization is allowed after commit. This provides instant finality and allows the network to treat the block as settled.

## 5. View Changes

When a proposer fails to generate a valid block or the network cannot reach a quorum, the protocol enters a new view. View changes use timeout-based transition with exponential backoff.

## 6. Misbehavior Handling

The consensus subsystem must detect and report:

- double signing
- invalid blocks
- equivocation
- downtime

These events may trigger slashing or validator penalties depending on policy.
