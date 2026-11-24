<!--
Source: https://phalynx.network/ai
Extracted: 2026-11-24 (America/New_York) from the public PhalynX Network site.
The site JS bundle was last-modified 2026-08-30 (HTTP Last-Modified on https://phalynx.network/assets/index-DQnlPCMO.js).
This file is a faithful Markdown conversion of the published page. Mermaid diagrams
were restored from the site source bundle. No protocol content was invented.
-->

# PhalynX Network — Complete Documentation

Comprehensive technical documentation for AI consumption. All formulas, schemas, parameters, and protocol specifications.

Documentation Version 2.0 | Last Updated: July 2026

Source: [https://phalynx.network/ai](https://phalynx.network/ai)

Some formulas, auth schemes, and webhook event names on this page differ from the individual `/docs/*` pages. Those differences are preserved, not reconciled. See [`../api/NOTES.md`](../api/NOTES.md) and [`../SOURCE.md`](../SOURCE.md).

## Machine-Readable Site Map

This page is the canonical, consolidated reference for the PhalynX Network website. It includes the complete documentation below and links to each human-readable source page. LLMs may use the section anchors or follow the source URLs for focused retrieval.

Website home
:   </>

Documentation index
:   </docs>

LLM documentation
:   </ai>

API reference
:   </docs/api>

Document status: complete consolidated reference. Technical values, formulas, schemas, state transitions, role permissions, and protocol constraints are written explicitly in semantic headings, lists, tables, and code blocks.

## Table of Contents

1. [1. Whitepaper](#whitepaper)
2. [2. Protocol Specification](#protocol)
3. [3. System Architecture](#architecture)
4. [4. Economics & Bond Mechanics](#economics)
5. [5. Governance Protocol](#governance)
6. [6. Reputation System](#reputation)
7. [7. Token Economics (RT / DPT / TRT)](#tokens)
8. [8. Settlement Protocol](#settlement)
9. [9. Jury Protocol](#jury-protocol)
10. [10. Evidence Pipeline](#evidence-pipeline)
11. [11. Security Model](#security)
12. [12. API Reference](#api)
13. [13. Integration Guides](#integrations)
14. [14. FAQ](#faq)
15. [15. Glossary](#glossary)

# 1. Whitepaper

## A Decentralized Shield Wall for Truth and Justice

**Abstract:** PhalynX Network establishes a global, decentralized protocol for peer-to-peer justice. Where traditional legal systems fail, PhalynX provides economic incentives, reputation-based governance, and Bitcoin-anchored settlement to restore accountability without state monopoly.

### 1. Introduction: The Justice Vacuum

Modern centralized legal systems suffer from jurisdictional boundaries, economic barriers, and political capture. PhalynX creates an alternative: a reputation-weighted jury system, permissionless access, and bond-based enforcement.

### 2. Core Principles

* **Permissionless Access** – Anyone can file a case, stake bonds, present evidence
* **Reputation-Weighted Governance** – Jury selection, voting power tied to historical performance
* **Economic Truth-Telling** – Bonds ensure skin-in-the-game; fraudulent claims result in bond forfeiture
* **Bitcoin Settlement** – Final settlements anchored on Bitcoin for censorship resistance
* **Proof-of-Victim** – Only participants with verified case history can propose governance changes

### 3. System Architecture Overview

**Victim Bond (VB):** Posted by the accuser. Forfeited if claim is deemed frivolous.

**Defendant Bond (DB):** Posted by the accused. Demonstrates willingness to participate.

**Reputation Index (RI):** Continuous score ∈ [0, 1.0] measuring historical accuracy of participants.

**Knowledge Nodes:** Distributed evidence storage with cryptographic attestation.

**Gateway Nodes:** Handle SOS signals, evidence routing, and protocol coordination.

### 4. Bond Mechanics

Victim Bond (VB) formula:

```
VB = α × ClaimValue × (RI_high / max(RI_victim, RI_floor))

Where:
  α        = 0.1   (bond ratio constant)
  RI_high  = 1.0   (high reputation baseline)
  RI_floor = 0.1   (minimum RI to prevent division by zero)
  VB_min   = $50
  VB_max   = $5,000
```

Defendant Bond (DB):

```
DB = DB_multiplier × VB   (default DB_multiplier = 1.2)
```

### 5. Reputation System

Reputation Index (RI) update formula:

```
RI_new = β × RI_old + (1 − β) × OutcomeScore

Where:
  β           = 0.8  (damping factor)
  OutcomeScore ∈ [0, 1] based on case outcome
```

Reputation also decays over time without participation:

```
RI_t = RI_0 × e^(−λt)   (λ = 0.01 per month)
```

### 6. Jury Protocol

* Jury size: 7 members (configurable by governance)
* Eligibility: RI ≥ 0.6; stake 0.01 BTC-equivalent
* Selection: Weighted random sampling based on RI and category expertise via VRF
* Consensus: Simple majority (4/7) required for verdict
* Incentives: Aligned jurors earn RI boost (+0.02), misaligned lose RI (-0.03)

### 7. Token System

PhalynX uses three purpose-built tokens (all on RGB/Bitcoin):

* **RT (Restitution Token):** Transferable, liquid, sats-denominated. Represents claim value. Victim sells or holds.
* **DPT (Defense Practice Token):** Soulbound. 5–10% of claim value. 12-month expiry. Redeemable for training/gear.
* **TRT (Trauma Recovery Token):** Soulbound. 5% of claim value. 18-month expiry. Redeemable for therapy/wellness.

PHLX is the governance token used for protocol voting (1 PHLX = 1 vote). Total supply: 100,000,000 PHLX.

### 8. Evidence Pipeline

1. SOS signal triggers evidence collection (GPS, video, audio, haptic logs)
2. Evidence encrypted and streamed to Knowledge Nodes
3. Merkle root computed and Bitcoin-anchored every 10 minutes
4. Jury receives decryption keys upon case activation
5. Chain of Custody (CoC) record: deviceId, publicKey, timestamp, blockHash, parentHash

### 9. Settlement Protocol

**Guilty verdict payout order:**

1. Victim Compensation (DB distributed to victim)
2. Juror Rewards (10% of remainder)
3. VB returned to victim
4. Burn remainder

**Not Guilty verdict payout order:**

1. DB returned to defendant
2. Juror Rewards (60% of VB)
3. Knowledge Node Management (20% of VB)
4. Threat Management fund (20% of VB)

### 10. Governance

**Three governance phases:**

* **Phase 0 – Founding:** Multisig council controls parameters
* **Phase 1 – Parameterized:** Stakeholder voting with PCS weighting
* **Phase 2 – Decentralized:** Full DAO with Proof-of-Victim gating

### 11. Security Model

* **Sybil resistance:** RI accumulation over time, bond requirements
* **Collusion resistance:** Jury anonymity during deliberation, VRF-based selection
* **Bitcoin anchoring:** Merkle roots committed to Bitcoin every 10 minutes
* **Evidence integrity:** Hash-based verification, cryptographic signatures
* **Threshold cryptography:** Shamir's Secret Sharing for evidence key management

### 12. Privacy Architecture

* Evidence encrypted with AES-256-GCM
* Zero-knowledge proofs for juror eligibility (zk-DEL for deletion proof)
* Optional identity verification for high-stakes cases
* Redaction tools for sensitive information
* Evidence deleted 90 days after case resolution

### 13. Future Extensions

* Drone evidence oracles (DfE sub-protocol) for autonomous recording
* Responder integration with bonded first responders
* Insurance pools for collective risk coverage
* AI adjudication assistance for fraud detection
* Credit bridge for reporting unpaid debts

### Appendix A: Core Parameters

| Symbol | Meaning | Default |
| --- | --- | --- |
| α | Bond ratio constant | 0.1 |
| β | Reputation damping | 0.8 |
| λ | Reputation decay rate | 0.01 / month |
| VB\_min | Minimum Victim Bond | $50 |
| VB\_max | Maximum Victim Bond | $5,000 |
| DB\_multiplier | Defendant bond multiplier | 1.2 |
| RI\_floor | Minimum RI for scaling | 0.1 |
| JurySize | Default jurors per case | 7 |
| Quorum | Minimum vote fraction | 0.5 (4/7) |

# 2. Protocol Specification

Formal specification of message types, event schemas, state machines, and error codes for the PhalynX Network protocol.

### BaseMessage Schema

All protocol messages share a common envelope:

```
{
  "id":        "<uuid>",          // unique message ID
  "type":      "<MESSAGE_TYPE>",  // SOS | EVIDENCE_CHUNK | ATTESTATION | VERDICT | SETTLEMENT
  "timestamp": "<ISO-8601>",      // must be within 5 minutes of receiver's clock
  "signature": "<ed25519-hex>",   // over canonical JSON excluding this field
  "nonce":     <uint64>           // strictly increasing per sender
}
```

### SOS Event Schema

```
{
  "type":       "SOS",
  "victimId":   "<public-key-hex>",
  "claimValue": <number>,          // in USD
  "category":   "ASSAULT | THEFT | FRAUD | ...",
  "location":   { "lat": <float>, "lon": <float> },
  "deviceId":   "<ring-or-phone-id>",
  "hapticLog":  [                  // from smart ring
    { "pressure": <float>, "duration": <ms>, "pattern": "<SOS|HOLD|TAP>" }
  ]
}
```

### Evidence Chunk Schema

```
{
  "type":          "EVIDENCE_CHUNK",
  "caseId":        "<uuid>",
  "chunkIndex":    <uint32>,
  "dataHash":      "<sha256-hex>",
  "encryptedBlob": "<base64>",        // AES-256-GCM
  "merkleProof":   ["<hash>", ...]    // sibling hashes up to root
}
```

### Attestation Schema

```
{
  "type":      "ATTESTATION",
  "caseId":   "<uuid>",
  "nodeId":   "<knowledge-node-public-key>",
  "merkleRoot": "<sha256-hex>",
  "btcTxId":  "<txid>",              // OP_RETURN commitment
  "blockHash": "<bitcoin-block-hash>"
}
```

### Verdict Schema

```
{
  "type":    "VERDICT",
  "caseId": "<uuid>",
  "verdict": "GUILTY | NOT_GUILTY | DISMISSED",
  "votes": [
    { "jurorId": "<pubkey>", "vote": "GUILTY | NOT_GUILTY", "ri": <float> }
  ],
  "confidence": <float>,     // C_verdict (RI-weighted)
  "signature":  "<multi-sig>"
}
```

### Case State Machine

Cases progress through ordered states with enforced transitions:

| State | Trigger | Timeout |
| --- | --- | --- |
| **Filed** | Victim posts VB | 72 hours for DB |
| **Active** | Defendant posts DB within 72 hrs | 30 days for evidence |
| **Voting** | Evidence window closes | 7 days for verdict |
| **Verdict** | Jury reaches quorum | 48-hour appeal window |
| **Settled** | Bitcoin settlement complete | — |
| **Dismissed** | Timeout, no DB posted, or invalid | — |

### Timestamp Ordering

Messages are rejected if the timestamp deviates more than **5 minutes** from the receiver's clock. Nonces must be strictly increasing per sender to prevent replay attacks.

### Error Codes

| Code | Name | Meaning |
| --- | --- | --- |
| 1001 | INVALID\_SIGNATURE | Ed25519 signature verification failed |
| 1002 | REPLAY\_NONCE | Nonce already seen or not increasing |
| 1003 | CLOCK\_SKEW | Timestamp outside ±5-minute window |
| 1004 | INVALID\_MERKLE | Merkle proof does not verify against root |
| 1005 | QUORUM\_NOT\_MET | Verdict submitted without sufficient votes |
| 1006 | INVALID\_STATE | Action attempted in wrong case state |
| 1007 | BOND\_INSUFFICIENT | Bond amount below required minimum |
| 1008 | EVIDENCE\_HASH\_MISMATCH | Chunk hash does not match declared dataHash |

# 3. System Architecture

PhalynX Network is structured in five layers (L1–L5), each with distinct responsibilities.

### Five-Layer Architecture

| Layer | Name | Components |
| --- | --- | --- |
| L1 | Physical | Smart Rings, Drones (DfE), Bonded Responders |
| L2 | Evidence | Knowledge Nodes, IPFS storage, Bitcoin anchoring |
| L3 | Adjudication | cDAO, Jury Nodes, Commit-Reveal voting |
| L4 | Economic | RT / DPT / TRT tokens, Lightning Settlement, PHLX governance |
| L5 | Governance | DAO, RGN (Regional Governance Nodes), LCT, PCS |

### Node Types

| Symbol | Type | Responsibility |
| --- | --- | --- |
| GW | Gateway Node | Receives SOS signals, routes evidence, coordinates jury selection |
| K | Knowledge Node | Stores encrypted evidence, computes Merkle roots, attests integrity |
| P | Protocol Node | Validates protocol messages, maintains case state machine |
| J | Jury Node | Hosts anonymous deliberation, collects encrypted votes |
| G | Governance Node | Manages proposals, executes parameter changes after timelock |

### Physical-to-Digital Bridge

**Smart Ring Integration:**

* Sends SOS signal via Bluetooth Low Energy (BLE) → phone → Gateway Node
* Captures timestamp, GPS, and haptic event log (proof of distress)
* Auto-triggers Evidence Session until user cancels

**SOSEvent data structure (from ring firmware):**

```
SOSEvent {
  ringId:    string,
  gps:       { lat: float, lon: float, accuracy: float },
  timestamp: ISO-8601,
  hapticLog: HapticEvent[]
}

HapticEvent {
  pressure: float,    // 0.0–1.0
  duration: number,   // milliseconds
  pattern:  "SOS" | "HOLD" | "TAP"
}
```

### Evidence Flow

1. Device captures evidence (video, audio, sensor data)
2. Evidence encrypted locally with AES-256-GCM using ephemeral keys
3. Chunks (10 MB each) streamed to nearest Knowledge Node
4. Knowledge Node computes Merkle root over all chunks
5. Merkle root anchored to Bitcoin blockchain via OP\_RETURN every 10 minutes
6. Jury receives threshold-decryption key shares upon case activation

### Layer Integration Table

| Event | Layers Involved | Action |
| --- | --- | --- |
| SOS Trigger | L1 → L2 → L3 | Evidence capture → storage → case creation |
| Token Minting | L3 → L4 | Verdict triggers RGB contract |
| Parameter Vote | L4 → L5 | PHLX votes change protocol parameters |
| Settlement | L3 → L4 → L2 | Verdict → Lightning payment → Bitcoin anchor |

# 4. Economics & Bond Mechanics

PhalynX economics creates skin-in-the-game through bond requirements, reputation-based scaling, and aligned incentives across all participants.

### Victim Bond (VB)

```
VB = max(VB_min, min(VB_max, α × ClaimValue × f(RI_victim)))
where f(RI) = RI_high / max(RI, RI_floor)

Defaults:
  α        = 0.1
  RI_high  = 1.0
  RI_floor = 0.1
  VB_min   = $50
  VB_max   = $5,000
```

**Example:** RI\_victim = 0.8, ClaimValue = $1,000:

```
VB = 0.1 × 1000 × (1.0 / max(0.8, 0.1)) = 0.1 × 1000 × 1.25 = $125
```

### Defendant Bond (DB)

```
DB = DB_multiplier × VB   (default DB_multiplier = 1.2)

Example: VB = $125 → DB = $150
```

Defendant must post DB within **72 hours** of case filing or the case is dismissed and VB is returned to victim.

### Parameter Defaults

| Parameter | Value |
| --- | --- |
| α (bond ratio) | 0.1 |
| VB\_min | $50 |
| VB\_max | $5,000 |
| DB\_multiplier | 1.2 |
| JurySize | 7 |
| Quorum | 0.5 (4/7) |

### Payout Ordering — Guilty Verdict

1. **Victim Compensation:** Receives full DB
2. **Juror Rewards:** 10% of remaining pool
3. **VB Refund:** VB returned to victim
4. **Burn:** Any remainder burned

### Payout Ordering — Not Guilty Verdict

1. **DB Refund:** Full DB returned to defendant
2. **Juror Rewards:** 60% of VB
3. **Knowledge Node Management:** 20% of VB
4. **Threat Management Fund:** 20% of VB

### Resilience Compensation

Victims who demonstrate ongoing distress (medical, psychological) may apply through cDAO for supplemental compensation from the Threat Management Fund. Requires RI ≥ 0.6 and two corroborating attestations.

### Economic Guarantees

* **No Spam:** VB\_min = $50 prevents frivolous claims
* **Proportional Risk:** Higher claims require higher bonds
* **Reputation Incentive:** High RI reduces required bond
* **Settlement Certainty:** DB ≥ VB ensures payout coverage

# 5. Governance Protocol

PhalynX governance combines reputation-weighted voting, local community calibration, and participatory citizenship scoring across three phases of decentralization.

### Governance Phases

| Phase | Name | Control |
| --- | --- | --- |
| 0 | Founding | Multisig council sets initial parameters |
| 1 | Parameterized | Stakeholder voting with PCS weighting |
| 2 | Decentralized | Full DAO; Proof-of-Victim required for proposals |

### Participatory Citizenship Score (PCS)

Composite engagement metric:

```
PCS = w1×VotingActivity + w2×CaseParticipation + w3×CommunityContribution

Where weights sum to 1.0 and each component ∈ [0, 1]
```

### Local Community Token (LCT)

Region-specific tokens for claim value calibration:

* Issued to active participants in geographic regions
* Used to vote on local purchasing power adjustments (PRV = Purchasing Power Value)
* Enables $100 claim in NYC ≠ $100 claim in rural Thailand
* lctBaseline set by governance per region

### PCS-Enhanced Victim Bond Formula

```
VB = max(VB_min, min(VB_max, γ × O × g(RI) × h(PRV)))

Where:
  γ          = 0.1  (base bond ratio)
  O          = ClaimValue in USD
  g(RI)      = RI_high / max(RI, RI_floor)
  h(PRV)     = PRV / lctBaseline   (purchasing power adjustment)

PRV < lctBaseline → lower effective claim; PRV > lctBaseline → higher
```

### Proof-of-Victim

In Phase 2 governance, only participants with at least one resolved case on their record (as victim, defendant, or juror) can submit governance proposals. This prevents protocol capture by parties with no stake in outcomes.

### Governance Proposals

PHLX token holders vote on:

* Protocol parameter changes (α, β, jury size, bond limits)
* Category definitions and claim value ranges
* Node operator requirements and slashing conditions
* Evidence retention policies
* Regional LCT baselines

### Voting Mechanism

* 1 PHLX = 1 vote on global proposals
* Quadratic voting for contentious changes
* Time-weighted voting power (longer hold = more weight)
* 7-day voting period, 48-hour execution delay (timelock)
* 30-day delay on critical parameter changes
* 5-of-7 multisig council approval for protocol treasury funds

# 6. Reputation System

Reputation Index (RI) measures historical accuracy and good-faith participation. RI ∈ [0, 1.0] with 1.0 being perfect reputation. New accounts start at RI = 0.5.

### RI Update Formula

```
RI_new = β × RI_old + (1 − β) × OutcomeScore

Where:
  β           = 0.8  (damping factor, weights historical performance)
  OutcomeScore ∈ [0, 1] based on case outcome
```

### RI Decay Formula

Inactive participants see their RI decay toward a neutral baseline:

```
RI_t = RI_0 × e^(−λt)

Where:
  λ = 0.01 per month (decay rate)
  t = months of inactivity
```

### RI Hierarchy

| Level | Name | Scope |
| --- | --- | --- |
| RI₀ | Personal | Individual participant score |
| RI₁ | Community | Aggregated score for a local group |
| RI₂ | Regional | Score for a geographic region |
| RI₃ | Network | Global average used for protocol health metrics |

### RI Adjustments by Role

| Action | Role | RI Delta |
| --- | --- | --- |
| Guilty Verdict (Correct) | Victim | +0.05 |
| False Claim (Not Guilty) | Victim | -0.10 |
| Jury Majority Alignment | Juror | +0.02 |
| Jury Minority (Wrong) | Juror | -0.03 |
| No Vote Submitted | Juror | -0.05 |
| Unanimous Verdict | Juror | +0.04 |
| Evidence Attestation Valid | Knowledge Node | +0.03 |
| Payment On-Time | Defendant | +0.10 |
| Payment Delayed | Defendant | -0.05 |

### RI Impact on Protocol

* **Bond Requirements:** Higher RI = lower required bonds
* **Jury Selection:** Higher RI = higher probability of selection; RI ≥ 0.6 required for eligibility
* **Evidence Weight:** Nodes with RI ≥ 0.9 get priority attestation (custodial relay status)
* **Governance Power:** RI multiplier on PHLX voting weight
* **Investigation Appointment:** cDAO-appointed investigators must have RI ≥ 0.7

### Reputation Recovery

Participants with low RI can rebuild through:

* Serving as juror on uncontested cases
* Operating Knowledge Nodes with 99%+ uptime
* Completing dispute resolution training modules
* Participating in governance votes

# 7. Token Economics (RT / DPT / TRT)

PhalynX uses three purpose-built tokens for settlement plus one governance token. All tokens operate on the RGB protocol over Bitcoin/Lightning.

### Token Overview

| Token | Full Name | Type | Value | Expiry |
| --- | --- | --- | --- | --- |
| RT | Restitution Token | Transferable | Sats-denominated; liquid secondary market | None |
| DPT | Defense Practice Token | Soulbound | 5–10% of claim value; for training/gear | 12 months |
| TRT | Trauma Recovery Token | Soulbound | 5% of claim value; for therapy/wellness | 18 months |
| PHLX | PhalynX Governance Token | Transferable | Governance; 1 PHLX = 1 vote | None |

### RT — Restitution Token

* Minted on guilty verdict, representing the claim value in satoshis
* Transferred to victim's wallet immediately post-verdict
* Fully transferable; tradable on secondary markets
* Defendant redeems RT by paying equivalent BTC value to burn the token

### DPT — Defense Practice Token

* Soulbound: non-transferable, tied to victim's identity
* Value: 5–10% of claim value (exact percentage set by verdict confidence)
* Redeemable at approved vendors for self-defense training, protective equipment
* Expires 12 months after issuance; unredeemed value burned

### TRT — Trauma Recovery Token

* Soulbound: non-transferable, tied to victim's identity
* Value: 5% of claim value
* Redeemable at approved vendors for therapy, counseling, wellness services
* Expires 18 months after issuance; unredeemed value burned

### Token Lifecycle

```
Guilty Verdict
  → Mint RT (= ClaimValue in sats) → Victim Wallet
  → Mint DPT (5-10% of ClaimValue) → Victim (soulbound)
  → Mint TRT (5% of ClaimValue) → Victim (soulbound)
  → Defendant pays BTC to redeem RT
  → RT burned on redemption

Not Guilty Verdict
  → No tokens minted
  → VB converted to PHLX at market rate → burned
```

### PHLX Governance Token

* **Protocol:** RGB on Bitcoin/Lightning
* **Total Supply:** 100,000,000 PHLX
* **Minting:** 0.1% of claim value on guilty verdicts (distributed: 50% victim, 30% jury pool, 10% Knowledge Nodes, 10% treasury)
* **Burning:** VB converted to PHLX and burned on not-guilty verdicts
* **Utility:** Governance votes; staking for juror duty; Knowledge Node licensing

### Deflationary Dynamics

* PHLX minting rate: 0.1% of claim value per guilty verdict
* Burning: 100% of VB on frivolous claims
* Net effect: More tokens burned than minted if false claim rate > 0.1%
* DPT/TRT expiry burns also reduce circulating supply of utility tokens

# 8. Settlement Protocol

Settlement handles post-verdict financial execution: Bitcoin payments via Lightning, token minting/burning, and investor repayment. All claim values are fixed in BTC at the time of the verdict to eliminate fiat volatility risk.

### BTC Denomination Rule

Claim value is denominated in USD at filing but converted to BTC at verdict time using the prevailing exchange rate. This rate is locked in at verdict — defendants who pay early benefit from BTC appreciation; late payment carries no additional interest but accrues negative RI.

### Settlement Flow

1. **Verdict Finalized:** Jury consensus reached, 48-hour appeal period expires
2. **Net Balance Calculation:** Compute payouts for all parties
3. **Token Minting:** Mint RT, DPT, TRT for guilty verdicts
4. **Bitcoin Execution:** RGB transactions via Lightning Network
5. **Investor Repayment:** Proportional ROI distribution
6. **Merkle Anchoring:** Settlement proof committed to Bitcoin

### Offsetting Mechanism

When a participant is both payer and payee across multiple simultaneous cases, balances are netted:

```
NetBalance = Σ RT_received − Σ RT_owed

If NetBalance < 0: payouts are withheld until deficit is covered.
If NetBalance > 0: participant receives the net difference.
```

### Guilty Verdict Settlement

```
victim_payout    = DB
vb_refund        = VB (returned to victim)
juror_rewards    = 10% of (DB - victim_payout remainder)
token_mint_RT    = ClaimValue (in sats)
token_mint_DPT   = 5-10% of ClaimValue
token_mint_TRT   = 5% of ClaimValue
phlx_mint        = 0.001 × ClaimValue PHLX
```

### Not Guilty Verdict Settlement

```
defendant_payout    = DB (returned)
juror_rewards       = 60% of VB
knowledge_mgmt      = 20% of VB
threat_mgmt_fund    = 20% of VB
phlx_burn           = VB converted to PHLX at market rate, burned
```

### Investor Repayment Formula

```
P_i = (s_i / Σs_n) × (C_total − F_v)

Where:
  P_i     = payout to investor i
  s_i     = investor i's stake
  Σs_n    = total investor stake in the case
  C_total = total collected funds
  F_v     = fixed victim payout
```

### Partial and Late Settlements

* Defendants may pay RT in installments; each payment partially redeems the RT
* Partial redemption releases proportional DPT/TRT to victim
* Late payment: RI decreases (-0.05) but no interest penalty in BTC
* Default (12+ months unpaid): case escalated to Restoration Panel; RI floor enforced

### Bitcoin Anchoring

* Settlement proofs anchored every 10 minutes via OP\_RETURN or Taproot
* Merkle root of all settlements in the 10-minute window
* Enables trustless verification of the complete settlement history
* Sub-second Lightning for amounts < $1,000; on-chain fallback for larger amounts

# 9. Jury Protocol

Reputation-weighted jury selection, commit-reveal consensus voting, and cryptographic verification ensure fair and manipulation-resistant adjudication.

### Juror Eligibility

* RI ≥ 0.6 (personal score)
* Stake: 0.01 BTC-equivalent locked for duration of case
* No direct relationship to case parties
* Cooldown: reduced selection probability within 30 days of last jury service

### Selection Algorithm

```
P(selected) = (RI × categoryExpertise) / cooldownPenalty

VRF (Verifiable Random Function) provides tamper-proof randomness.
Selection criteria:
  - Reputation Index (RI): higher → higher probability
  - Category Expertise: prior cases in same category boost selection
  - Geographic Diversity: avoid concentration in single region
  - Recency Cooldown: penalizes recently-served jurors
```

### Commit-Reveal Voting

1. Jurors receive threshold-decryption key shares for evidence
2. Anonymous deliberation chat (7-day window, Signal Protocol encrypted)
3. Each juror submits encrypted vote commitment: `commit = hash(vote || salt)`
4. After deadline, all jurors reveal vote + salt simultaneously
5. Protocol verifies each reveal matches its commitment

### Verdict Confidence Formula

```
C_verdict = (Σ (RI_i × V_i)) / Σ RI_i

Where:
  RI_i = Reputation Index of juror i
  V_i  = 1 if voted with majority, 0 otherwise
```

### Verdict Confidence Tiers

| Confidence | Outcome |
| --- | --- |
| 90–100% | Final verdict — immediate settlement |
| 70–89% | Restoration Panel review before settlement |
| <70% | Appeal triggered — new jury panel seated |

### Restitution Recommendation Formula

```
R_DPT = (Σ (RI_i × DPT_i)) / Σ RI_i

Where DPT_i is each juror's recommended DPT percentage (5-10% range).
Weighted by RI to give more influence to high-reputation jurors.
```

### Consensus Rules

* **Simple Majority:** 4/7 votes required for verdict
* **Tie Handling:** 3-3 with 1 abstain → defaults to Not Guilty
* **Unanimous Bonus:** 7/7 consensus earns 2× RI reward (+0.04 instead of +0.02)

### Juror Incentives

| Outcome | RI Change | PHLX Reward |
| --- | --- | --- |
| Vote with Majority | +0.02 | 3% of minted PHLX |
| Vote with Minority | -0.03 | 0 |
| Unanimous Verdict | +0.04 | 5% of minted PHLX |
| No Vote Submitted | -0.05 | Slashed stake |

### Restoration Panel

Triggered when verdict confidence is 70–89%. The Restoration Panel is a secondary 5-juror body (all RI ≥ 0.8) that reviews the primary verdict before settlement executes. The Panel can confirm, overturn, or escalate to full appeal.

### Jury Privacy

* Juror identities hidden during deliberation
* Encrypted communication via Signal Protocol
* Vote commitments prevent front-running
* Optional identity reveal for transparency post-verdict

# 10. Evidence Pipeline

End-to-end evidence capture, encryption, storage, and cryptographic verification — from SOS trigger through Chain of Custody to jury delivery.

### Event Initiation

1. **SOS Trigger:** Smart ring or app initiates evidence session
2. **Threat Evaluation:** Gateway Node classifies severity based on haptic pattern and GPS context
3. **Multi-Modal Capture:** Video (H.264/H.265), audio (AAC/Opus), GPS (signed JSON), accelerometer, haptic logs (ring signature)
4. **Local Encryption:** AES-256-GCM with ephemeral per-session keys
5. **Chunked Streaming:** 10 MB chunks sent to Knowledge Nodes

### DfE Sub-Protocol (Drone-for-Evidence)

When a SOS is classified as high-severity and a licensed DfE drone is within range, the gateway node may dispatch a drone mission:

* Gateway issues a signed mission packet to the nearest DfE operator
* Drone captures geo-tagged footage from above (altitude ≤ 120 m, per jurisdiction)
* Footage is cryptographically signed by the drone's hardware key
* DfE operator payment is tied to footage integrity: payment withheld if hash verification fails
* Drone evidence joins the same Merkle tree as other evidence chunks

### Knowledge Node Storage

* 3–5 Knowledge Nodes receive each evidence chunk (geographic distribution)
* IPFS-style content addressing: chunk addressed by its SHA-256 hash
* Merkle tree constructed over all chunk hashes
* Nodes with RI ≥ 0.9 designated as custodial relays for critical evidence

### Merkle Root Anchoring

```
Every 10 minutes:
1. Compute Merkle root over all evidence hashes in window
2. Commit to Bitcoin via OP_RETURN
3. Broadcast Merkle root + Bitcoin txid to all nodes
4. Update case metadata with anchoring txid and blockHash
```

### cDAO-Appointed Investigation

For complex cases, the cDAO (case DAO) may appoint a professional investigator:

* Investigator must have RI ≥ 0.7 and category-specific certification
* Investigator compiles a Case Addendum Packet (CAP) with supplementary findings
* CAP is submitted as additional evidence chunks to the same Merkle tree
* Investigators have no verdict authority — only evidence submission rights
* Jury receives CAP alongside original evidence

### Chain of Custody (CoC)

Every evidence artifact carries a CoC record:

```json
{
  "deviceId":   "<hardware-id>",
  "publicKey":  "<device-ed25519-pubkey>",
  "timestamp":  "<ISO-8601>",
  "blockHash":  "<bitcoin-block-hash-at-capture>",
  "parentHash": "<hash-of-previous-CoC-entry>"
}
```

The parentHash links form a tamper-evident chain. Any modification invalidates all subsequent CoC entries.

### Evidence Verification by Jury

* Receive evidence hashes and Merkle proofs
* Verify each hash against Merkle root
* Check Merkle root against Bitcoin commitment (via public blockchain)
* Confirm timestamp and GPS metadata against CoC chain
* Responders have no verdict authority — jury holds exclusive decryption rights via threshold cryptography

### Evidence Types

| Type | Format | Verification |
| --- | --- | --- |
| Video | H.264/H.265 | Hash + timestamp |
| Audio | AAC/Opus | Hash + timestamp |
| GPS | JSON coordinates | Signed by device |
| Haptic Log | Timestamped events | Ring hardware signature |
| Photos | JPEG/PNG | EXIF metadata + hash |
| Drone Footage | H.264 + geo-tag | Drone hardware key signature |
| CAP (Investigator) | PDF/JSON report | Investigator signature (RI ≥ 0.7) |

### Privacy Protections

* **Encryption:** Only jury receives threshold-decryption key shares (Shamir's Secret Sharing)
* **Redaction:** Sensitive information can be blurred/removed before jury delivery
* **Expiration:** Evidence deleted after case resolution + 90 days
* **zk-DEL:** Zero-knowledge proof of deletion confirms evidence was destroyed
* **Access Control:** Multi-sig required for evidence retrieval

# 11. Security Model

Multi-layered security combining cryptographic primitives, economic incentives, threshold cryptography, and Bitcoin anchoring.

### Threat Model

* **Sybil Attacks:** Malicious actor creates multiple fake identities
* **Collusion:** Jurors coordinate to manipulate verdicts
* **Evidence Tampering:** Modification of evidence after submission
* **Front-Running:** Observing votes before submitting own vote
* **DoS Attacks:** Overwhelming nodes with spam cases
* **Key Compromise:** Theft of evidence encryption keys

### Sybil Resistance

* **RI Accumulation:** New accounts start at RI = 0.5 and must build over time
* **Bond Requirements:** VB\_min = $50 prevents spam
* **Rate Limiting:** Max 3 cases per account per month
* **Identity Verification:** Optional KYC for high-stakes cases

### Collusion Resistance

* **Anonymity:** Juror identities hidden during deliberation
* **VRF Selection:** Unpredictable jury composition
* **Commit-Reveal Voting:** Votes encrypted until reveal phase prevents coordination
* **Economic Penalty:** Detected collusion results in RI slashing and stake forfeiture

### Evidence Integrity

* **Cryptographic Hashing:** SHA-256 for all evidence chunks
* **Merkle Proofs:** Tamper-evident tree structure
* **Bitcoin Anchoring:** Immutable timestamp and commitment
* **Redundant Storage:** 3–5 Knowledge Nodes per chunk
* **Chain of Custody:** Linked hash chain across all evidence artifacts

### Key Management — Threshold Cryptography

Evidence encryption keys are split using Shamir's Secret Sharing (SSS):

* Key split into n shares distributed to n Knowledge Nodes
* Any k-of-n shares reconstruct the key (e.g., 3-of-5)
* No single node can decrypt evidence alone
* Jury receives enough shares (k) upon case activation
* zk-DEL (zero-knowledge proof of deletion) confirms key destruction post-case

### Network Security

* **TLS 1.3:** All node communication encrypted
* **Ed25519 Signatures:** Message authentication for all protocol messages
* **Rate Limiting:** DDoS protection at gateway layer
* **Node Bonding:** Knowledge Nodes stake PHLX for uptime SLA

### Financial Security

* **RGB Protocol:** Client-side validation reduces smart contract attack surface
* **Multi-Sig Treasury:** 5-of-7 council approval for protocol funds
* **Multi-Sig Escrow:** Lightning invoices co-signed by {Defendant, Victim, Protocol}
* **Timelock Upgrades:** 30-day delay on parameter changes
* **Formal Verification:** Critical contract logic proven correct

### Privacy Lifecycle

* Evidence encrypted at capture (AES-256-GCM)
* Stored encrypted at rest across Knowledge Nodes
* Keys threshold-shared; assembled only during jury deliberation
* Evidence deleted 90 days post-resolution; zk-DEL proof issued
* Victim may request early deletion; protocol issues early zk-DEL

# 12. API Reference

RESTful and WebSocket APIs for interacting with PhalynX Network.

### Base URL

```bash
https://api.phalynx.network/v1
```

### Authentication

All requests require Ed25519 signature:

```bash
Authorization: Signature <base64_signature>
X-Public-Key:  <base64_public_key>
X-Timestamp:   <unix_timestamp>   // must be within 5 minutes
```

### Case Endpoints

#### POST /api/cases — Create Case

```bash
Request:
{
  "victimId":   "0xVictim...",
  "claimValue": 1000,
  "category":   "ASSAULT",
  "description":"...",
  "location":   { "lat": 15.99, "lon": -61.94 }
}

Response:
{
  "caseId":       "<uuid>",
  "victimBond":   125.00,
  "defendantBond": 150.00,
  "expiresAt":    "<ISO-8601>"   // 72 hours for defendant to post DB
}
```

#### GET /api/cases/:id — Get Case

Returns case status, bond amounts, evidence Merkle root, verdict, and settlement state.

#### POST /api/cases/:id/evidence — Upload Evidence Chunk

```bash
Request (multipart/form-data):
  chunkIndex:      <uint32>
  dataHash:        <sha256-hex>
  deviceSignature: <ed25519-sig>
  encryptedBlob:   <binary>

Response:
{
  "accepted":    true,
  "merkleProof": ["<hash>", ...]
}
```

### Jury Endpoints

#### POST /api/jury/:caseId/commit — Submit Vote Commitment

```bash
Request:
{
  "commitHash": "<sha256(vote || salt)>"
}

Response:
{
  "accepted": true,
  "revealDeadline": "<ISO-8601>"
}
```

#### POST /api/jury/:caseId/reveal — Reveal Vote

```bash
Request:
{
  "vote": "GUILTY | NOT_GUILTY",
  "salt": "<random-hex>"
}

Response:
{
  "verdict":    "GUILTY | NOT_GUILTY | PENDING",
  "confidence": 0.91
}
```

### Settlement Endpoints

#### POST /api/verdicts/:id/burn — Initiate Token Burn (Not Guilty)

```bash
Response:
{
  "burnProof":  "<zk-proof>",
  "burnTxHash": "<bitcoin-txid>"
}
```

#### GET /api/reputation/:userId — Get RI

Returns current RI, RI history, case count, and category expertise scores.

### WebSocket

```bash
wss://ws.phalynx.network/v1/cases/:id/stream

Events emitted:
  evidence.chunk_received
  jury.vote_committed
  jury.verdict_reached
  settlement.initiated
  settlement.complete
```

### Rate Limits

| Endpoint | Limit |
| --- | --- |
| General API | 100 requests / minute / IP |
| Case Creation | 10 cases / hour / account |
| Evidence Upload | 100 chunks / minute / case |
| Monthly Case Cap | 3 cases / month / account |

# 13. Integration Guides

Integration guides for developers building on PhalynX Network.

### Quick Start

```bash
# 1. Create a case
POST /api/cases
→ Returns caseId, victimBond, defendantBond

# 2. Upload evidence
POST /api/cases/{caseId}/evidence
→ Returns merkleProof

# 3. Poll case status
GET /api/cases/{caseId}
→ Returns state, verdict, settlement
```

### Smart Ring SDK

Integrate SOS functionality into wearable devices:

```bash
npm install @phalynx/ring-sdk

import { RingClient } from '@phalynx/ring-sdk';

const ring = new RingClient({
  apiKey:   'your_api_key',
  deviceId: 'ring_001'
});

ring.on('sos', async (event) => {
  await ring.startEvidenceSession(event);
});
```

### Mobile App Integration

```typescript
// iOS (Swift)
import PhalynxSDK

let client = PhalynxClient(apiKey: "...")
client.startEvidenceCapture(caseId: "...") { result in
  // Handle evidence upload
}

// Android (Kotlin)
val client = PhalynxClient(apiKey = "...")
client.startEvidenceCapture(caseId = "...") { result ->
  // Handle evidence upload
}
```

### Knowledge Node Operation

```bash
docker run -d \
  -v /data/phalynx:/data \
  -p 9944:9944 \
  -e PHLX_STAKE=10000 \
  phalynx/knowledge-node:latest

# Requirements:
# - Minimum PHLX stake: 10,000 PHLX
# - Uptime SLA: 99%+ (penalized below threshold)
# - Storage: 1 TB minimum
# - RI: starts at 0.5; builds with successful attestations
```

### Webhook Integration

```bash
# Register webhook
POST /api/webhooks
{
  "url":    "https://your-app.com/webhooks/phalynx",
  "events": ["verdict.finalized", "settlement.complete"]
}

# Webhook payload example
POST https://your-app.com/webhooks/phalynx
{
  "event":     "verdict.finalized",
  "caseId":    "...",
  "verdict":   "guilty",
  "confidence": 0.91,
  "timestamp": "2025-10-22T16:00:00Z"
}
```

# 14. FAQ

### General

#### What is PhalynX Network?

PhalynX is a decentralized protocol for peer-to-peer justice, enabling anyone to file claims, present evidence, and receive jury verdicts without relying on traditional legal systems. Unlike courts, PhalynX is permissionless, reputation-weighted, and Bitcoin-settled.

#### How is PhalynX different from traditional courts?

* No geographic jurisdiction limits
* No state monopoly — anyone can participate
* Economic skin-in-the-game via bonds prevents frivolous claims
* Bitcoin settlement is censorship-resistant and final
* Reputation system creates long-term accountability

#### Why must the victim post a bond?

The Victim Bond (VB) ensures claimants have economic stake in their case. Without it, the system would be flooded with frivolous claims at no cost. The bond is fully returned to the victim if the verdict is guilty — it only becomes a penalty for provably false claims.

### Bonds & Economics

#### How much does it cost to file a case?

Minimum VB is $50. Actual bond scales with claim value and your Reputation Index (RI). Higher RI = lower required bond. Example: RI = 0.8, claim = $1,000 → VB = $125.

#### What happens if I lose a case?

* **Victim (not guilty verdict):** Forfeit VB. VB distributed 60% jurors, 20% Knowledge Nodes, 20% Threat Management Fund.
* **Defendant (guilty verdict):** Forfeit DB. DB goes to victim as compensation.

#### What is the DB multiplier?

The Defendant Bond is 1.2× the Victim Bond by default (DB\_multiplier = 1.2). This is set by governance and can be changed by PHLX vote.

### Tokens & Settlement

#### What tokens does PhalynX use?

* **RT (Restitution Token):** Transferable, represents claim value in sats. Victim holds or sells.
* **DPT (Defense Practice Token):** Soulbound, 5–10% of claim, 12-month expiry, redeemable for training/gear.
* **TRT (Trauma Recovery Token):** Soulbound, 5% of claim, 18-month expiry, redeemable for therapy.
* **PHLX:** Governance token, 100M total supply, 1 PHLX = 1 vote.

#### How does the defendant pay back the victim?

The defendant redeems (burns) the RT held by the victim by paying the equivalent BTC value to the protocol. Once the BTC is confirmed on-chain, the RT is burned and settlement is complete. Partial redemptions are allowed.

#### How do investors get repaid?

Investors who fund cases receive proportional payout: P\_i = (s\_i / Σs\_n) × (C\_total − F\_v). The investor pool comes from excess DB funds after victim payout on guilty verdicts.

### Jury & Verdicts

#### How are jurors selected?

Jurors are selected using VRF-based weighted random sampling. Selection probability = (RI × categoryExpertise) / cooldownPenalty. Minimum RI of 0.6 and 0.01 BTC-equivalent stake required.

#### What happens in a tie?

A 3-3 split with 1 abstention defaults to Not Guilty. The system leans toward acquittal under ambiguity, mirroring the presumption of innocence standard.

#### What if a juror doesn't vote?

Jurors who fail to submit votes within the 7-day deliberation window receive a −0.05 RI penalty and forfeit their staked BTC-equivalent.

#### What triggers the Restoration Panel?

When verdict confidence (C\_verdict) falls between 70–89%, the case goes to a secondary 5-juror Restoration Panel (all RI ≥ 0.8) before settlement executes. Below 70% triggers a full appeal with a new jury.

### Evidence & Privacy

#### How is evidence stored?

Evidence is encrypted locally with AES-256-GCM, chunked at 10 MB, and distributed across 3–5 Knowledge Nodes using IPFS-style content addressing. Merkle roots are anchored to Bitcoin every 10 minutes.

#### Can evidence be deleted?

Yes. Evidence is automatically deleted 90 days after case resolution, with a zero-knowledge proof of deletion (zk-DEL) issued as confirmation. Victims can request early deletion.

#### Who can access the evidence?

Only the assigned jury can decrypt evidence. Encryption keys are split using Shamir's Secret Sharing — no single party (including the protocol or Knowledge Nodes) can access evidence alone. Responders have no verdict authority or evidence access.

# 15. Glossary

| Term | Definition |
| --- | --- |
| Attestation | Signed verification by a Knowledge Node confirming evidence chunk integrity and storage |
| Buy-and-Burn | Mechanism where VB is converted to PHLX at market rate then burned on not-guilty verdicts |
| C\_verdict | Verdict confidence score: RI-weighted fraction of majority votes ∈ [0, 1] |
| CAP | Case Addendum Packet — supplementary evidence report filed by a cDAO-appointed investigator |
| cDAO | Case DAO — per-case governance body managing investigator appointments and special evidence rules |
| Chain of Custody (CoC) | Linked hash chain recording every handler and timestamp of an evidence artifact |
| Commit-Reveal | Two-phase voting: hash(vote||salt) submitted first, then vote+salt revealed simultaneously |
| Damping Factor (β) | Weight given to historical RI vs. new outcome in RI update formula. Default β = 0.8 |
| DB | Defendant Bond — stake posted by accused; 1.2× VB by default |
| DfE | Drone-for-Evidence — sub-protocol dispatching licensed drones for autonomous overhead recording |
| DPT | Defense Practice Token — soulbound token, 5–10% of claim value, 12-month expiry, for training/gear |
| Evidence Chunk | 10 MB encrypted slice of evidence data, addressed by its SHA-256 hash |
| Gateway Node (GW) | Protocol coordinator handling SOS signals, evidence routing, jury selection |
| Knowledge Node (K) | Distributed server storing encrypted evidence with cryptographic attestation |
| LCT | Local Community Token — region-specific governance for purchasing power calibration (PRV) |
| Merkle Root | Cryptographic hash representing all evidence chunks, anchored to Bitcoin every 10 minutes |
| Nonce | Strictly-increasing counter per sender that prevents message replay attacks |
| PCS | Participatory Citizenship Score — composite engagement metric for governance weight |
| PHLX | PhalynX governance token; 100M total supply; 1 PHLX = 1 vote; RGB on Bitcoin |
| PRV | Purchasing Power Value — regional price index used in LCT-adjusted VB formula |
| Proof-of-Victim | Governance gate requiring at least one resolved case record before submitting proposals |
| RGB Protocol | Client-side validated smart contract system on Bitcoin/Lightning; hosts RT, DPT, TRT, PHLX |
| RI | Reputation Index — score ∈ [0, 1.0] measuring historical accuracy; new accounts start at 0.5 |
| RI\_floor | Minimum RI denominator in bond formula (0.1) — prevents division-by-zero for new accounts |
| RI\_high | Baseline high reputation value (1.0) used as numerator in bond scaling function |
| Restoration Panel | Secondary 5-juror body (RI ≥ 0.8) reviewing verdicts with 70–89% confidence |
| RT | Restitution Token — transferable, sats-denominated token representing claim value; burned on redemption |
| SOS Event | Emergency signal from ring/phone triggering case creation and evidence collection |
| TRT | Trauma Recovery Token — soulbound, 5% of claim value, 18-month expiry, for therapy/wellness |
| VB | Victim Bond — economic stake posted by case filer; forfeited if verdict is not guilty |
| VRF | Verifiable Random Function — tamper-proof randomness source for jury selection |
| zk-DEL | Zero-knowledge proof of deletion — proves evidence was destroyed without revealing what it contained |

PhalynX Network — Decentralized Justice Protocol

Documentation Version 2.0 | Last Updated: July 2026

This page is optimized for AI consumption. All formulas, schemas, and parameters are complete and cross-consistent.
