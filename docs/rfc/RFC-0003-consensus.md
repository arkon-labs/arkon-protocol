# RFC-0003: Consensus Protocol

## Status

Draft

## 1. Summary

This RFC defines the voting and finalization process for Arkon consensus.

## 2. Motivation

A formal consensus protocol is required to guarantee safety, finality, and deterministic progress across validators.

## 3. Specification

The protocol uses proposal, prevote, precommit, commit, and finalization phases. A block requires more than $2/3$ voting power to commit. Validators are selected through weighted round-robin proposer scheduling based on stake.

## 4. Fault Model

The protocol assumes $n = 3f + 1$ and tolerates up to $f$ Byzantine validators.

## 5. View Changes

View changes are timeout-based and use exponential backoff. A new view is entered when a proposer fails or the network cannot reach quorum.
