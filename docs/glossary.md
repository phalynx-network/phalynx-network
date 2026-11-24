<!--
Source: https://phalynx.network/docs/glossary
Extracted: 2026-11-24 (America/New_York) from the public PhalynX Network site.
The site JS bundle was last-modified 2026-08-30 (HTTP Last-Modified on https://phalynx.network/assets/index-DQnlPCMO.js).
This file is a faithful Markdown conversion of the published page. Mermaid diagrams
were restored from the site source bundle. No protocol content was invented.
-->

# Glossary

Comprehensive glossary of PhalynX Network protocol terminology and concepts.

## A

**Attestation**
:   Cryptographic proof provided by a Knowledge Node confirming evidence integrity via Merkle root verification.

## B

**Bond**
:   Economic stake posted by participants (victims, defendants) to ensure skin-in-the-game and discourage frivolous claims or defenses.

**Buy-and-Burn**
:   Settlement mechanism where verdict tokens are used to purchase BTC, which is distributed to payees, then tokens are permanently destroyed (burned).

## C

**Claim Value**
:   The amount of compensation requested by the victim, denominated in USD equivalent.

**Commit-Reveal**
:   Two-phase voting mechanism where jurors first submit hashed votes (commit), then reveal plaintext votes after all commits are received, preventing vote coordination.

**Consensus**
:   Agreement reached by jury panel, typically requiring simple majority (>50%) for verdict finalization.

## D

**Damping Factor (β)**
:   Parameter controlling how much a single case outcome affects Reputation Index, preventing extreme swings from isolated verdicts.

**Defendant Bond (DB)**
:   Economic stake posted by defendant, proportional to claim value (typically 120%), forfeited if found guilty.

## E

**Evidence Chunk**
:   Discrete unit of evidence (video frame, sensor reading, document) transmitted to the protocol with cryptographic hash and sequence number.

**Evidence Pipeline**
:   Multi-stage system for collecting, hashing, encrypting, and storing evidence with integrity guarantees.

## G

**Gateway**
:   Entry point for evidence submission, validating signatures and routing data to Knowledge Nodes.

**Governance**
:   System for managing protocol parameters and upgrades, evolving from centralized (Phase 0) to fully decentralized (Phase 2).

## J

**Jury Panel**
:   Randomly selected group of jurors (default: 7) who review evidence and vote on case verdicts.

**Juror**
:   Protocol participant who stakes economic value to join jury pools, earning rewards for consensus participation.

## K

**Knowledge Node**
:   Decentralized storage provider that encrypts evidence, computes Merkle trees, and issues attestations.

## M

**Merkle Tree**
:   Hierarchical hash structure allowing efficient proof of evidence inclusion and integrity verification.

**Merkle Root**
:   Top hash of Merkle tree, serving as compact cryptographic commitment to all evidence in a case.

## N

**Nonce**
:   Monotonically increasing counter included in messages to prevent replay attacks.

## O

**Oracle**
:   External data provider (Chainlink, Band, etc.) supplying BTC price feeds for settlement conversion.

## P

**Payout Ordering**
:   Deterministic sequence for distributing bonds after verdict: victim compensation → juror rewards → token burn (for Guilty verdicts).

## Q

**Quorum**
:   Minimum number or percentage of jurors required to reach consensus, defaulting to simple majority (>50%).

## R

**Reputation Index (RI)**
:   Score tracking participant behavior over time, influencing bond costs and jury selection probability. Updated after each case based on verdict outcome.

**RI Floor**
:   Minimum RI value (default: 100) used in bond calculations to prevent division by zero and cap maximum bond requirements.

**RI High**
:   Baseline RI value (default: 1000) representing high reputation, resulting in minimum bond costs.

## S

**Settlement**
:   Final distribution of bonds according to verdict, executed in BTC via buy-and-burn mechanism.

**SOS Event**
:   Initial message initiating a new case, containing victim ID, claim value, category, and optional location/device metadata.

**State Machine**
:   Deterministic flow of case states (Filed → Active → Voting → Verdict → Settled) with defined transition rules.

## T

**Threshold Encryption**
:   Cryptographic technique requiring multiple Knowledge Nodes to cooperate for decryption, preventing unilateral evidence access.

**Timestamp**
:   ISO 8601 UTC timestamp included in all messages for ordering and replay attack prevention.

## V

**Verdict**
:   Final decision by jury panel, either GUILTY or NOT\_GUILTY, determining bond distribution and reputation updates.

**Verdict Token**
:   BTC-denominated token representing settlement obligation, minted at verdict and burned after BTC distribution.

**Victim Bond (VB)**
:   Economic stake posted by case filer, scaled inversely by Reputation Index to discourage frivolous claims.
