# Serialization Specification

## Purpose

This document defines the canonical serialization rules for Arkon data structures. Deterministic serialization is essential for consensus correctness, cryptographic commitments, and state reproduction.

## 1. Serialization Principles

All protocol objects must be serialized according to the following principles:

- fixed-length encoding for integers and hashes
- length-prefixed encoding for variable-size fields
- canonical ordering of fields and lists
- no platform-specific endianness dependence

## 2. Encoded Objects

The serialization format applies to:

- transactions
- blocks
- UTXOs
- consensus messages
- cryptographic proofs

## 3. Canonicalization Rules

A canonical encoding must:

- include all fields required for semantic interpretation
- exclude nondeterministic metadata
- preserve field ordering
- use the same encoding for all conforming implementations

## 4. Hashing and Signing

The canonical byte representation is used for:

- transaction hash computation
- block hash computation
- signature payloads
- Merkle tree construction

## 5. Implementation Guidance

Implementations must avoid implicit serialization differences caused by language-specific defaults or map ordering. All data structures should be normalized prior to hashing or signing.
