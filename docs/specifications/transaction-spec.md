# Transaction Specification

## 1. Scope

This specification defines the canonical transaction format for Arkon.

## 2. Transaction Object

A transaction object contains:

- inputs
- outputs
- metadata
- fee
- signatures

## 3. Validation Requirements

A transaction is valid if:

1. all inputs reference existing UTXOs
2. the referenced UTXOs are unspent
3. the unlocking conditions are satisfied
4. the signatures are valid
5. the fee is correctly accounted for
6. the transaction is serialized canonically

## 4. Signing Model

Transaction signatures use Ed25519 over the canonical serialization of the transaction body.

## 5. Fees and Priority

Fee handling is configurable. Transactions with higher fee-to-size ratios may be prioritized in the mempool, but policy must be explicit and enforceable.

## 6. Failure Modes

The transaction subsystem must reject:

- malformed serialization
- invalid signatures
- double spending
- overspending
- invalid output amounts
