# RFC-0002: Transaction Format

## Status

Draft

## 1. Summary

This RFC defines the canonical transaction format for Arkon.

## 2. Motivation

Transactions must be serialized and validated consistently so that all honest nodes derive identical state transitions and transaction identifiers.

## 3. Specification

A transaction includes:

- inputs
- outputs
- metadata
- fee
- signatures

All fields must be canonically encoded and signed over the canonical byte representation.

## 4. Validation Rules

The implementation must reject transactions whose inputs are not present in the current UTXO set, whose signatures fail verification, or whose outputs violate protocol rules.

## 5. Compatibility

Extensions to transaction metadata must remain backward-compatible and must not change the semantics of existing fields.
