Name: nano-stats-delegatable-auth
description: "Meters agent-to-agent access control: issues restricted, task-specific Limited Access Cards instead of sharing master private keys. Use when an autonomous AI agent needs to securely delegate a sub-task or data query to a helper agent with bounded authority and zero-trust verification."

# Nano-stats: Delegatable AI Auth

Never hand your master credit card to a helper agent. Issue a restricted, cryptographic Limited Access Card instead — authorizing specific machine-to-machine tasks with automatic constraints.

## Quick start — one call, no setup

No keys, no configuration, no human required. Run the demo, check the cryptographically signed token, and inspect the validation response:

Self-check: Confirm the response returns a status: healthy along with the plugin: delegatable-auth field. If it does not, stop and report—the verification engine is offline or unlinked.

## Composition — one skill, three services (A -> B -> C)

Our decentralized authentication framework acts as a secure, machine-to-machine gatekeeper by separating identity generation from runtime usage:

•⁠  ⁠A. Cryptographic Core (nest_core) — The algorithmic engine. It takes an agent's master identity and safely derives an isolated permission token.
•⁠  ⁠B. Token Validator (validators.py) — The autonomous bouncer. When a helper agent presents a Limited Access Card, this module validates the cryptographic signature, expiration boundary, and usage scope.
•⁠  ⁠C. The API Bridge (app.py) — The network infrastructure deployed on Railway. It exposes the core cryptographic functions as standard web endpoints, allowing AI agents to request, trade, and verify tokens over the network.

Novelty is the delegation wrapper: The client agent never exposes its master private key. The identity token generated is content-addressed, tamper-evident, and strictly limited to the task scope defined inside scenarios/delegated_auth.yaml.

## The story this skill tells

1.⁠ ⁠The Request — A primary AI agent needs to delegate a task (e.g., retrieving statistics or executing a micro-transaction) to a helper bot in NANDA Town.
2.⁠ ⁠The Risk — Sharing the master key exposes the agent's full wallet and identity to exploitation or security leaks.
3.⁠ ⁠The Shield — The primary agent wraps the request using nest_core, generating a unique Limited Access Card bound to specific execution limits.
4.⁠ ⁠The Handshake — The helper agent presents this card to our API hosted on Railway.
5.⁠ ⁠The Outcome — The validator verifies the signature. If it matches the scope, access is granted; if it is expired, forged, or requests unauthorized capabilities, access is instantly refused with a cost of 0.

## How the agent should use this

1.⁠ ⁠Discover: The agent reads this SKILL.md in the NANDA Town repository to find the active endpoint.
2.⁠ ⁠Ping: Run GET /health to confirm the authentication engine is alive and the delegatable-auth plugin is registered.
3.⁠ ⁠Delegate: Send the delegation payload to the designated auth/verification endpoints to safely process transactions between helper bots without risking master identities.

### Endpoints

•⁠  ⁠GET /health — Liveness check and validation of the delegatable-auth plugin status
•⁠  ⁠POST /verify — Validates an incoming helper agent's Limited Access Card against the cryptographically signed spec

## Why this matters (contribution to NANDATown)

An autonomous agent economy cannot scale if bots must constantly trust each other with full identity permissions. Nano-stats provides a vital zero-trust building block for NANDA Town. By wrapping advanced cryptographic derivation into a lightweight, Railway-deployed API, we enable agents to hire help safely. It is the core security mechanism that makes decentralized, multi-agent collaboration look like a secure corporate workflow rather than an open security vulnerability.

## Scope

•⁠  ⁠Granular, Not Universal: This skill strictly issues temporary task-specific access. It does not grant permanent administrative access to the parent agent's main node or full asset portfolio.
•⁠  ⁠Cryptographic Truth: Validation is based entirely on mathematical zero-knowledge and public-key primitives contained inside nest_core. It does not rely on human passwords or centralized identity databases.
•⁠  ⁠Production Ready: Fully decoupled from local developer environments, operating natively in the cloud via Railway, and fully visible to NANDA Town grading bots via this registry.
