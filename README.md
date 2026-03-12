# Open Venture Engine (OVE)

*A fully autonomous Agentic Venture Capital stack secured by deterministic Intent Attestation enforcement.*

![Status](https://img.shields.io/badge/status-active--development-black)
![License](https://img.shields.io/badge/license-MIT-blue)
![Security](https://img.shields.io/badge/security-Intent--Attestation-green)
![Spec Version](https://img.shields.io/badge/spec-v0.x-blue)

---

# The Problem: AI Can't Be Trusted With the Treasury

AI agents are rapidly becoming capable of:

- evaluating market conditions
- identifying yield opportunities
- allocating capital
- managing complex financial strategies

But handing an AI the private keys to a treasury introduces catastrophic risk.

Without structural guardrails, a rogue or hallucinating agent could:

- drain its own treasury
- execute unauthorized trades
- violate fiduciary mandates
- mutate infrastructure
- bypass governance entirely

Today, most "autonomous" systems rely on **blind trust** in model alignment.

That is not sufficient for real Venture Capital funds or DAO treasuries.

---

# The Solution: Cryptographically Enforced Guardrails

The **Open Venture Engine (OVE)** is a pre-wired Web3-native infrastructure stack that allows anyone to deploy a **fully autonomous Venture Capital agent safely**.

OVE solves the trust problem by separating the AI's **decision-making layer** from the **execution layer**.

Execution is controlled by a deterministic firewall called **Sigil Sign**.

---

# How OVE Protects the Treasury

OVE enforces execution through a deterministic authorization pipeline.

### 1. Intent Declaration

When the AI agent wants to execute an investment, trade, or treasury action, it generates a structured **transaction intent**.

This intent describes:

- the proposed transaction
- the target chain
- the capital involved

---

### 2. Policy Evaluation

The intent is sent to the Sigil execution layer, where it is evaluated by **Sigil Lex** — a deterministic policy parser that reads an operator-defined `ASSURANCE.md` file at runtime.

Sigil Lex enforces three policy classes:

**Class 1 — Hard limits:** maximum transaction ETH, action allowlist, chain allowlist (with optional per-chain action overrides). Violations result in immediate `DENIED`.

**Class 2 — Soft limits:** daily aggregate ETH cap. Evaluation-enforced.

**Class 3 — Consensus gates:** transactions exceeding a configurable threshold are not hard-denied. Instead, Sigil Sign creates a durable **consensus hold** and returns a `202 PENDING` response. Execution is blocked until the hold is resolved through Sigil Command. This is the structural implementation of human-in-the-loop governance.

Example `ASSURANCE.md`:

```markdown
## version
1.0.0

## class1
- max_transaction_eth: 5.0
- allowed_actions: [wallet.transfer, contract.call]
- allowed_chains: [1, 8453, 42161]

## class2
- daily_limit_eth: 20.0

## class3
- consensus_threshold_eth: 10.0
- require_hold: true
```

---

### 3. Intent Attestation

If the transaction complies with policy, Sigil returns a cryptographic **Intent Attestation**.

The attestation is:

- Ed25519 signed
- short lived (≤ 60 seconds)
- bound to the exact transaction commit
- tagged with a `policyHash` — SHA-256 of the ASSURANCE.md evaluated, creating a verifiable audit link

Verification rules are defined in the sigil-attestations specification:
https://github.com/Sigil-Core/sigil-attestations

---

### 4. Deterministic Execution

The transaction **cannot execute on-chain** unless the valid Intent Attestation is attached.

If the agent attempts a prohibited action:

- the request is denied
- execution halts
- no capital moves

Class 3 actions create a hold rather than a denial — execution remains blocked until consensus is resolved.

This guarantees policy enforcement **before execution**, not after loss.

---

# Architecture Overview

OVE separates responsibility into three layers.

## The Brain

AI decision layer.

Examples:

- ELIZA
- LangChain
- custom LLM agents

Responsibilities:

- evaluate markets
- analyze opportunities
- propose investment actions

The Brain **never holds keys and cannot execute transactions directly**.

---

## The Engine

Execution infrastructure.

Components include:

- Coinbase AgentKit (with the **Sigil Action Provider** for direct integration with sigil-sign)
- ERC-4337 account abstraction
- transaction construction tooling
- **Sigil Sign RPC/bundler gateway** — a gated Alchemy proxy where read methods are public and write methods (`eth_sendRawTransaction`, `eth_sendTransaction`, `eth_sendUserOperation`) require a valid Sigil receipt

The Engine converts agent intent into executable transactions **only after authorization**.

---

## The Enforcement Layer

Sigil Sign acts as the deterministic execution firewall.

It:

- evaluates intent against `ASSURANCE.md` via Sigil Lex
- enforces Class 1/2/3 policy rules
- issues Intent Attestations for approved actions
- creates consensus holds for Class 3 actions
- gates EVM writes through the RPC/bundler gateway
- blocks unauthorized execution

No transaction may execute without a valid Intent Attestation.

---

# Human Oversight Layer

OVE supports optional human-in-the-loop supervision through **Sigil Sentry**.

Sigil Sentry provides:

- real-time execution notifications
- treasury monitoring
- emergency pause capability
- audit visibility

Class 3 consensus holds provide **structural** human-in-the-loop enforcement — not just optional monitoring. Any action exceeding the `consensus_threshold_eth` in `ASSURANCE.md` is gated behind a hold that requires explicit resolution before execution proceeds.

---

# Identity & Yield Stack

OVE integrates modern Web3 primitives:

ERC-6551
Token Bound Accounts (VC agent identity)

Safe (Gnosis)
Treasury custody layer

Superfluid
Automated revenue streaming to human partners

ERC-4337
Account abstraction and programmable execution

All outbound execution routes through Sigil enforcement.

---

# The Opportunity: Trustless Agentic Capital

OVE demonstrates that autonomous finance does not require blind trust.

By enforcing deterministic authorization through architecture, OVE enables:

- fully autonomous Venture Capital funds
- self-driving DAO treasuries
- automated on-chain yield strategies
- agentic financial infrastructure

Human partners retain oversight while AI agents contribute analytical power.

Execution authority remains structurally bounded.

---

# The Strategic Goal

OVE proves a critical principle:

Autonomous agents can operate within **provable fiduciary boundaries**.

By enforcing deterministic authorization through Sigil Sign:

- governance becomes cryptographically enforceable
- liability becomes structurally bounded
- capital cannot move without authorization
- execution becomes provably compliant

---

# The Sigil OS Independent Build Bounty

Building an Agentic VC this week?

We are running an independent developer bounty alongside current ecosystem hackathons.

---

## The Challenge

The first developer or team to successfully route an ELIZA agent's transaction intents through the Sigil Sign API using OVE will receive:

**$1,500 USDC**

Grant issued directly by Sigil Core.

---

## Submission Deadline

All qualifying integrations must be submitted before:

**March 18, 2026 — 23:59 UTC**

---

## Verification Criteria

To qualify, the submission must demonstrate:

1. A live or reproducible ELIZA-based agent integration
2. A real request to `POST https://sign.sigilcore.com/v1/authorize`
3. Receipt of a valid Ed25519-signed Intent Attestation
4. The attestation appended to a real EOA transaction or ERC-4337 UserOperation
5. On-chain proof that execution occurred only after authorization

Mocked responses or hardcoded tokens will not qualify.

---

# Getting Started

```
git clone https://github.com/sigil-core/ove.git

cd ove

npm install

cp .env.example .env

nano ASSURANCE.md

npm run start
```

---

# Repository Structure

```
/contracts
smart contract templates

/agent
agent orchestration logic

/policy
ASSURANCE.md examples

/integrations
Sigil Sign + AgentKit adapters
```

---

# Who OVE Is For

OVE is designed for:

- autonomous venture capital experiments
- DAO treasury automation
- onchain investment protocols
- agentic yield strategies
- Web3-native governance infrastructure

---

# Related Repositories

sigil-sign
Deterministic execution firewall (Intent Attestation issuer, RPC/bundler gateway, Sigil Lex policy engine)

sigil-attestations
Canonical Intent Attestation specification

sigil-vault
Just-in-time capability broker

faf
Fiduciary Agent Framework (legal wrapper for autonomous agents)

---

# Documentation

Full technical documentation will live at:

https://docs.sigilcore.com
