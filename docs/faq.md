<!--
Source: https://phalynx.network/docs/faq
Extracted: 2026-11-24 (America/New_York) from the public PhalynX Network site.
The site JS bundle was last-modified 2026-08-30 (HTTP Last-Modified on https://phalynx.network/assets/index-DQnlPCMO.js).
This file is a faithful Markdown conversion of the published page. Mermaid diagrams
were restored from the site source bundle. No protocol content was invented.
-->

# Frequently Asked Questions

## General

### How is PhalynX different from traditional courts?

PhalynX operates as a decentralized protocol rather than a centralized institution. Key differences include:

* **Economic bonds** replace filing fees and enforcement mechanisms
* **Cryptographic evidence** ensures tamper-proof chain of custody
* **Decentralized juries** selected randomly with economic stake alignment
* **Automated settlement** in BTC rather than months-long execution
* **Reputation-based access** discourages frivolous claims

### Why is victim participation required?

The victim-required principle ensures cases have genuine claimants with economic skin in the game. This prevents:

* Third-party prosecution without victim consent
* State-initiated cases against victim wishes
* Frivolous claims by non-injured parties

> Victims post Victim Bonds (VB) which are returned if they win, creating a clear economic incentive structure.

## Bonds & Economics

### What happens to bonds if I win my case?

**If you're the victim and win (Guilty verdict):**

* You receive compensation up to your claim value from defendant's bond
* Your Victim Bond (VB) is returned in full
* Your Reputation Index (RI) increases, lowering future bond costs

**If you're the defendant and win (Not Guilty verdict):**

* Your Defendant Bond (DB) is returned in full
* Your RI increases

### What happens to bonds if I lose my case?

**If you're the victim and lose:**

* You forfeit your VB which is used to pay jurors, knowledge management, and threat management
* Your RI decreases, increasing future bond costs
* The defendant receives their DB back

**If you're the defendant and lose:**

* You forfeit your DB
* Your RI decreases significantly
* DB is distributed: victim compensation → juror rewards → burn

### How are bond amounts calculated?

**Victim Bond (VB):** Scaled inversely by your Reputation Index. Higher reputation = lower bond requirement.

**Defendant Bond (DB):** Proportional to claim value (typically 120% to ensure adequate coverage).

> See the [Economics](economics.md) section for detailed formulas and examples.

## Tokens & Settlement

### What are verdict tokens?

Verdict tokens are BTC-denominated instruments representing settlement obligations. They use a buy-and-burn mechanism:

1. Tokens are minted when a verdict is reached
2. Protocol buys equivalent BTC using oracle price feeds
3. BTC is distributed according to payout ordering
4. Tokens are burned after settlement completes

This ensures settlements are transparent, automated, and executed in BTC rather than requiring manual enforcement.

### Why Bitcoin and not USD or another cryptocurrency?

BTC is chosen for settlement because:

* **Neutrality:** Not controlled by any government or corporation
* **Finality:** Irreversible settlements prevent chargebacks
* **Accessibility:** Global reach without banking infrastructure
* **Store of value:** Long-term settlement preservation

## Jury & Verdicts

### How are jurors selected?

Jurors are randomly selected from an active pool, weighted by:

* Reputation score (higher reputation = higher selection probability)
* Staked amount (minimum stake required to participate)
* Historical performance (consistent voters preferred)

### What prevents jury collusion?

Several mechanisms prevent collusion:

* **Random selection:** Jurors don't know panel composition until commitment phase
* **Commit-reveal voting:** Votes are hidden until all commits are submitted
* **Economic penalties:** Jurors who fail to reveal forfeit stake
* **Reputation tracking:** Voting patterns are monitored for anomalies

### What if the jury is split 50-50?

The protocol requires a simple majority (>50%) for consensus. In rare ties, the case defaults to "Not Guilty" following the principle of reasonable doubt. Future versions may implement appeal mechanisms for high-value disputed cases.

## Evidence & Privacy

### How is evidence kept secure?

Evidence security uses multiple layers:

* **E2E encryption:** Evidence encrypted at source before transmission
* **Threshold decryption:** Requires quorum of Knowledge Nodes to decrypt
* **Merkle anchoring:** Cryptographic proof of integrity
* **Access control:** Only authorized parties (victim, defendant, jury) can view

### Can evidence be deleted or modified?

No. Once evidence is submitted and anchored with a Merkle root, any modification invalidates the cryptographic proof. This is immediately detectable and results in case dismissal.

## Integration & Usage

### How do I integrate my Ring camera or IoT device?

See the [Device Integration](https://phalynx.network/docs/integrations/devices) guide for step-by-step instructions. The process involves:

1. Register your device with the Gateway API
2. Configure evidence streaming endpoints
3. Implement signature-based authentication
4. Test evidence submission and attestation

### Can I use PhalynX for small claims?

Yes. Minimum claim values start at $50 (the minimum VB). The protocol is designed to be economical for both small and large claims through reputation-scaled bonds.

### What jurisdictions does PhalynX operate in?

The protocol is jurisdiction-agnostic as a technical system. The initial pilot is launching in Próspera, Honduras, which has regulatory frameworks supporting alternative dispute resolution. Expansion to other jurisdictions will follow based on legal compatibility.

> **Legal Disclaimer**
>
> PhalynX is a protocol for decentralized dispute resolution. Users should consult local legal counsel to understand how verdicts may be recognized or enforced in their jurisdiction.
