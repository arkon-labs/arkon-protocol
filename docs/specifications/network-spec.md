# Network Specification

## 1. Scope

This specification defines the Arkon peer-to-peer networking behavior required for connectivity, synchronization, and propagation.

## 2. Transport

QUIC is the preferred transport. Nodes must support message framing, encryption, and version negotiation.

## 3. Messages

The following message types are defined:

- HELLO
- PING
- PONG
- GET_BLOCKS
- SEND_BLOCK
- NEW_TRANSACTION
- VOTE
- COMMIT
- SYNC_REQUEST
- SYNC_RESPONSE

## 4. Peer Behavior

Nodes must:

- maintain a set of active peers
- exchange HELLO on connection establishment
- respond to PING with PONG
- relay valid transactions and blocks to peers

## 5. Synchronization Model

Nodes synchronize by requesting missing blocks or state from peers. The protocol must support partial sync and recovery from interrupted transfers.

## 6. Security Constraints

The network layer must reject malformed messages, enforce peer identity checks, and protect against spam and denial-of-service behavior.
