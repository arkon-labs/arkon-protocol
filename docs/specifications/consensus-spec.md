# Consensus Specification

## 1. Scope

This specification defines the Arkon consensus protocol for agreement on block ordering and finality.

## 2. Model

Arkon uses a permissionless Proof-of-Stake validator set with a Tendermint-style BFT voting procedure. The protocol assumes a partially synchronous network and uses weighted validator voting power.

## 3. Parameters

The following parameters are configurable:

- minimum stake for validator candidacy
- block time target
- proposal timeout
- prevote timeout
- precommit timeout
- max evidence age
- slashing penalties

## 4. Protocol Phases

### 4.1 Proposal

A proposer is selected by weighted round-robin scheduling. The proposer forms a candidate block and broadcasts it to validators.

### 4.2 Prevote

Validators verify the proposal. If valid, they cast a prevote for the block. Otherwise, they cast a nil prevote.

### 4.3 Precommit

Validators precommit to a block if the network observed sufficient prevotes for that proposal.

### 4.4 Commit

If the required quorum of voting power prevotes and precommits, the block is committed and finalized.

### 4.5 Finalization

The block becomes part of the canonical chain; no later reorganization is permitted.

## 5. Quorum and Fault Tolerance

The protocol requires more than $2/3$ of voting power to commit a block. Under the model $n = 3f + 1$, the protocol tolerates up to $f$ Byzantine validators.

## 6. Safety Requirements

The protocol must ensure:

- no conflicting finalized blocks at the same height
- no double-vote evidence under the same height and round
- validator equivocation is detectable

## 7. Liveness Requirements

The protocol must recover from proposer failure or temporary network delay using timeouts and exponentially increasing view changes.
