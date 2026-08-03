# Networking Architecture

## Purpose

Arkon uses a decentralized peer-to-peer network to distribute blocks, propagate transactions, and synchronize chain state. The network layer must resist malicious peers while remaining efficient under partial connectivity.

## 1. Transport

QUIC is the preferred transport protocol because it provides:

- low-latency communication
- built-in connection migration
- robust performance under packet loss

TCP fallback may be used during early deployment if QUIC support is unavailable.

## 2. Node Identity

Each node has:

- a cryptographic identity key
- a network address
- optional validator identity for consensus participation

The node identity is distinct from the wallet address used for transaction authorization.

## 3. Peer Discovery

Nodes discover peers through:

- static bootstrap nodes
- DNS seed lists
- peer exchange over existing connections
- manual configuration

## 4. Message Model

The following message types are required:

| Message | Purpose |
| --- | --- |
| HELLO | Announces node identity and protocol version |
| PING | Liveness check |
| PONG | Response to PING |
| GET_BLOCKS | Requests block range or tip state |
| SEND_BLOCK | Delivers a serialized block |
| NEW_TRANSACTION | Announces a new pending transaction |
| VOTE | Carries consensus vote data |
| COMMIT | Carries a commit evidence message |
| SYNC_REQUEST | Requests a state synchronization operation |
| SYNC_RESPONSE | Returns synchronized state data |

## 5. Block Propagation

Blocks are propagated using a broadcast strategy with validation at each hop. A node accepts a block only if:

- it passes structural validation
- it extends the current canonical chain
- it has a valid quorum-supported commit context

## 6. Transaction Gossip

New transactions are gossiped to peers after basic validation. Nodes must avoid rebroadcasting duplicates and should apply rate limiting to prevent spam.

## 7. Security Against Malicious Peers

The network layer must enforce:

- protocol version checks
- peer reputation scoring
- rate limiting
- transaction and block signature validation
- message size limits

## 8. Synchronization

The node should recover from gaps in chain knowledge using block range requests and state synchronization. Synchronization must be resumable and should not require a full restart after temporary disconnection.
