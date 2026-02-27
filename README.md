# Open Venture Engine (OVE)

An autonomous Agentic VC boilerplate secured by Sigil's deterministic intent routing. 



## Overview

The Open Venture Engine (OVE) is a pre-wired, Web3-native technology stack that allows anyone to spin up a fully autonomous Venture Capital firm. It aggregates the best execution primitives into one template, while hardwiring the necessary structural brakes so the agent cannot go rogue and drain its own treasury.

### The Stack
* **The Brain:** ELIZA / LangChain (Evaluates market conditions and proposes trades).
* **The Engine:** Coinbase AgentKit (Handles wallet creation and EVM transaction formatting).
* **The Brakes:** Sigil OS & `@sigilcore/agent-hooks` (Intercepts the transaction and enforces the `ASSURANCE.md` policy).
* **Identity & Yield:** ERC-6551 (Token Bound Accounts) and Superfluid (for streaming automated yield back to the human GP).

## Getting Started

```bash
git clone [https://github.com/sigilcore/ove-boilerplate.git](https://github.com/sigilcore/ove-boilerplate.git)
cd ove-boilerplate
npm install

# Configure your .env variables
cp .env.example .env

# Edit your operational constraints
nano ASSURANCE.md

# Start the Agentic VC
npm run start
# Open Venture Engine (OVE)

*A fully autonomous Agentic Venture Capital stack secured by deterministic Intent Attestation enforcement.*

---

## Executive Summary

The **Open Venture Engine (OVE)** is a pre-wired, Web3-native infrastructure stack that allows anyone to deploy a fully autonomous Venture Capital agent.

OVE aggregates best-in-class execution primitives while structurally enforcing deterministic governance through Sigil’s execution firewall.

This ensures the agent cannot:

- Drain its own treasury
- Execute unauthorized trades
- Bypass fiduciary constraints
- Mutate infrastructure without policy approval

OVE is designed to demonstrate how autonomous capital deployment can operate within strict structural boundaries.

---

## Architecture Overview

OVE separates execution into three distinct layers:

### 🧠 The Brain
- **ELIZA / LangChain**
- Evaluates market conditions
- Proposes investments or yield strategies
- Generates structured transaction intent

### ⚙️ The Engine
- **Coinbase AgentKit**
- Handles wallet provisioning
- Formats EVM transactions
- Generates ERC-4337 UserOperations

### 🛑 The Brakes
- **Sigil Sign**
- `@sigilcore/agent-hooks`
- Enforces deterministic `ASSURANCE.md` policy
- Issues short-lived Ed25519-signed **Intent Attestations**

No transaction may execute without a valid Intent Attestation.

---

## Identity & Yield Stack

OVE integrates modern Web3 primitives:

- **ERC-6551** — Token Bound Accounts (VC Agent is the NFT)
- **Safe (Gnosis)** — Treasury custody
- **Superfluid** — Automated revenue streaming to the human GP
- **ERC-4337** — Account abstraction and programmable execution

All outbound execution must route through Sigil.

---

## The Sigil OS Independent Build Bounty

Building an Agentic VC this week? We are running an independent developer bounty parallel to ongoing ecosystem hackathons.

### The Challenge

The first developer or team to successfully route their ELIZA agent's transaction intents through the Sigil Sentry API (utilizing the Open Venture Engine) will receive a $1,500 USDC grant.

**Note:** This is an independent grant issued directly by Sigil Core and is not affiliated with or sponsored by third-party hackathon organizers. Payout is contingent on a successful, verifiable API integration and Intent Attestation generation.

---

### Submission Deadline

All qualifying integrations must be submitted and verifiable on or before **March 18, 2026 at 23:59 UTC**.

Submissions after this deadline will not be eligible for the grant.

---

### Verification Criteria

To qualify for the $1,500 USDC grant, the submission must demonstrate:

1. A live or reproducible ELIZA-based agent integration.
2. A real `POST /v1/authorize` request to `sign.sigilcore.com`.
3. Successful receipt of a valid Ed25519-signed **Intent Attestation**.
4. The Intent Attestation being appended to a real EOA transaction or ERC-4337 UserOperation.
5. On-chain verification that the transaction was executed only after authorization.

Mocked responses, simulated attestations, or hardcoded JWTs will not qualify.

---

## How Intent Attestation Works

Before execution:

1. The agent proposes a transaction.
2. The transaction intent is sent to `POST /v1/authorize`.
3. Sigil evaluates the request against `ASSURANCE.md`.
4. If compliant, Sigil returns a short-lived Ed25519-signed Intent Attestation.
5. The transaction is executed only if the attestation is appended.

If denied, the agent receives a deterministic JSON Rebound and must halt execution.

---

## Getting Started

```bash
git clone https://github.com/sigil-core/ove.git
cd ove
npm install

# Configure environment variables
cp .env.example .env

# Edit deterministic policy constraints
nano ASSURANCE.md

# Start the Agentic VC
npm run start
```

---

## Repository Structure

```
/contracts
    Smart contract templates (if applicable)

/agent
    Agent orchestration logic

/policy
    ASSURANCE.md examples

/integrations
    Sigil Sign + AgentKit adapters
```

---

## Who OVE Is For

- Autonomous Venture Capital experiments
- DAO treasury automation
- Onchain investment protocols
- Agentic yield strategies
- Web3-native governance tooling

---

## The Strategic Goal

OVE demonstrates that autonomous capital deployment does not require blind trust.

By structurally enforcing deterministic authorization through Sigil Sign, OVE proves:

- Autonomous agents can operate within fiduciary boundaries
- Governance can be cryptographically enforced
- Liability can be bounded by architecture
- Execution can be provably authorized before capital moves
