# RFC-0001: Block Format

## Status

Draft

## 1. Summary

This RFC defines the canonical on-chain block format for Arkon.

## 2. Motivation

A deterministic block format is required to ensure consensus correctness, verifiable state transitions, and consistent serialization across implementations.

## 3. Specification

A block is encoded as:

- header
- body

The header contains version, height, timestamp, previous hash, Merkle root, state root, and validator signature. The body contains a list of transactions.

## 4. Validation Rules

Implementations must reject blocks that fail the structural, cryptographic, or state transition checks defined in this specification.

## 5. Compatibility

Future versions may extend the header with additional fields, but existing fields must preserve their semantics and fixed placement.
