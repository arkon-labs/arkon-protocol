# RFC-0004: Networking Protocol

## Status

Draft

## 1. Summary

This RFC defines the peer-to-peer messaging and synchronization protocol for Arkon nodes.

## 2. Motivation

A clear network protocol is required for discovery, synchronization, block propagation, transaction gossip, and defense against malicious peers.

## 3. Specification

Nodes communicate using the messages HELLO, PING, PONG, GET_BLOCKS, SEND_BLOCK, NEW_TRANSACTION, VOTE, COMMIT, SYNC_REQUEST, and SYNC_RESPONSE. QUIC is preferred for transport.

## 4. Security Requirements

The implementation must validate peer messages, enforce message size limits, and reject malformed or invalid data.

## 5. Compatibility

Future network upgrades must preserve the semantics of existing message types and support backward-compatible negotiation.
