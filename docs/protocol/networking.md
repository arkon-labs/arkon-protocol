# Networking Protocol Specification

## Purpose

This document defines the peer-to-peer network protocol used by Arkon nodes. The network is responsible for discovery, synchronization, transaction gossip, and block propagation.

## 1. Transport

QUIC is preferred. Nodes may fall back to TCP if required by deployment constraints.

## 2. Message Catalog

| Message | Direction | Purpose |
| --- | --- | --- |
| HELLO | bidirectional | Announces identity and protocol version |
| PING | bidirectional | Liveness check |
| PONG | bidirectional | Response to PING |
| GET_BLOCKS | request/response | Requests a range of blocks |
| SEND_BLOCK | response | Delivers a block payload |
| NEW_TRANSACTION | broadcast | Announces a new transaction |
| VOTE | broadcast | Propagates consensus votes |
| COMMIT | broadcast | Propagates commit evidence |
| SYNC_REQUEST | request/response | Requests chain sync |
| SYNC_RESPONSE | response | Returns state or block data |

## 3. Peer Discovery

Nodes discover peers from a configured list of bootstrap nodes, DNS seeds, and peer exchange over active connections.

## 4. Synchronization

Nodes maintain a view of the best known chain height and synchronize missing blocks through GET_BLOCKS and SEND_BLOCK. Sync must be resumable and deterministic.

## 5. Security Requirements

The network implementation must enforce:

- protocol version compatibility
- transaction and block signature checks
- peer blacklisting for repeated invalid behavior
- rate limiting to deter spam and amplification attacks
