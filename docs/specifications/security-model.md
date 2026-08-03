# Security Model

## 1. Threat Model

Arkon is designed to remain secure under the assumption that some validators and peers may behave maliciously. The protocol assumes an adversary may delay, reorder, or forge messages, but must not exceed the allowed Byzantine threshold.

## 2. Security Goals

The protocol aims to provide:

- authenticity of transactions and blocks
- integrity of ledger state
- safety of finalized blocks
- liveness under partial synchrony
- resistance to validator equivocation and denial-of-service attacks

## 3. Cryptographic Assumptions

Arkon relies on:

- Ed25519 for signatures
- BLS12-381 for validator signatures
- BLAKE3 for hashing and commitments
- canonical serialization for cryptographic payloads

## 4. Consensus Security

The system is safe so long as the number of Byzantine validators is less than one-third of the total voting power, and liveness is preserved under network synchrony assumptions.

## 5. Network Security

The network must protect against:

- invalid block propagation
- spam transactions
- peer impersonation
- replay attacks
- resource exhaustion

## 6. Economic Security

Stake-based validator participation and configurable slashing rules provide economic deterrence against malicious behavior.
