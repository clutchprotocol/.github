# Start here — Clutch Protocol welcome thread

**Use this file as the body for a pinned GitHub Discussion.**

## How to publish

1. Open https://github.com/orgs/clutchprotocol/discussions/new
2. If Discussions is disabled: **Organization settings → General → Discussions** → enable for the org
3. **Category:** Announcements (or General)
4. **Title:** `Start here — Clutch Protocol welcome thread`
5. Copy everything below the line into the discussion body and publish
6. Pin: **⋯** menu on the discussion → **Pin discussion**

---

## Paste below this line into GitHub Discussions

---

Welcome to **Clutch Protocol** — an open-source stack for decentralized ride-sharing where the full ride lifecycle (request → offer → accept → pay → cancel) lives on-chain, with **client-side signing** and **driver-first CLT economics**.

> **Alpha software** — public testnet for experimentation. APIs may change. No mainnet yet.

---

## Try it (no install)

| Resource | Link |
|----------|------|
| **Stage demo** (recommended) | https://app-stage.clutchprotocol.io |
| **Documentation** | https://docs.clutchprotocol.io |
| **Website** | https://clutchprotocol.io |
| **npm SDK** | https://www.npmjs.com/package/clutch-hub-sdk-js |

**Quick try on stage:**

1. Open https://app-stage.clutchprotocol.io
2. Choose **Passenger** or **Driver** and generate a wallet
3. Request test CLT from the built-in faucet
4. Passenger: request a ride on the map · Driver: view requests and submit an offer

---

## Run locally (full stack)

```bash
git clone https://github.com/clutchprotocol/clutch-deploy.git
cd clutch-deploy
cp .env.example .env
docker compose up -d
```

| Service | URL |
|---------|-----|
| API health | http://localhost:3000/health |
| GraphQL | http://localhost:3000/graphql |
| Demo app | http://localhost:5173 |
| Explorer | http://localhost:5174 |
| Grafana | http://localhost:3030 (admin/admin) |

Full guide: https://docs.clutchprotocol.io/getting-started/quickstart

---

## Repositories (8 project repos)

| Repo | What it does |
|------|----------------|
| [clutch-node](https://github.com/clutchprotocol/clutch-node) | Blockchain core — Aura consensus, custom RLP txs, WebSocket JSON-RPC |
| [clutch-hub-api](https://github.com/clutchprotocol/clutch-hub-api) | GraphQL bridge, wallet JWT auth, testnet faucet |
| [clutch-hub-sdk-js](https://github.com/clutchprotocol/clutch-hub-sdk-js) | JavaScript/TypeScript SDK — client-side signing, subscriptions |
| [clutch-hub-demo-app](https://github.com/clutchprotocol/clutch-hub-demo-app) | Reference React demo (passenger + driver) |
| [clutch-explorer](https://github.com/clutchprotocol/clutch-explorer) | Block indexer, REST API, web UI |
| [clutch-deploy](https://github.com/clutchprotocol/clutch-deploy) | Docker Compose for the full stack |
| [clutch-docs](https://github.com/clutchprotocol/clutch-docs) | Developer docs (Docusaurus) |
| [clutchprotocol.github.io](https://github.com/clutchprotocol/clutchprotocol.github.io) | Marketing site |

---

## How a ride works

```
Your app + SDK  →  Hub API (unsigned tx)  →  sign locally  →  submit signed tx  →  Clutch Node
```

1. **Build** — App asks the Hub API for an unsigned transaction (`createUnsignedRideRequest`, etc.)
2. **Sign** — User signs the hash locally with secp256k1 (**private keys never sent to the server**)
3. **Submit** — App sends signed RLP hex via `sendRawTransaction`
4. **Settle** — Node verifies signature/nonce, updates ride state, includes tx in a block

Tutorial: https://docs.clutchprotocol.io/getting-started/ride-lifecycle

---

## CLT economics (summary)

- **Drivers** receive most of each fare on `RidePay`
- **Referrers** earn up to **4%** per payment installment (default **2% request + 2% offer**)
- **Validators** earn a fixed **50 CLT/block** reward — separate from ride fares

**App developers:** run your own Hub API, set your wallet as referrer in config, and earn CLT when users complete rides on your deployment.

Details: https://docs.clutchprotocol.io/getting-started/app-developer-incentives

---

## Honest limitations (alpha)

- Public **testnet only** — no mainnet
- **DAO / governance** is on the roadmap — not implemented yet
- `ConfirmArrival` / `ComplainArrival` tx types exist as **stubs** in the node
- Hub **subscriptions poll** the node (~0.5–1s), not push-from-chain
- Small validator set on the public stage testnet

FAQ: https://docs.clutchprotocol.io/reference/faq

---

## Roadmap snapshot

| Milestone | Status |
|-----------|--------|
| Public stage testnet (multi-node Aura) | **Live** |
| Hub API + SDK + demo + explorer | **Live** |
| DAO governance | Planned |
| Arrival confirmation tx types | Planned (stubs in node) |
| Mainnet | Planned — no fixed date |

---

## Contribute

We welcome issues, discussions, and pull requests.

1. **Fork** the relevant repo
2. **Branch** — e.g. `feature/my-change`
3. **Commit** — use [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, etc.)
4. **Open a PR** — link to an issue when possible

Check each repo for `CONTRIBUTING.md` where available (e.g. [clutch-node](https://github.com/clutchprotocol/clutch-node/blob/main/CONTRIBUTORS.md)).

### Good first issues

Search open issues across the org:

https://github.com/orgs/clutchprotocol/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22

If no labeled issues exist yet, useful entry points:

- **Docs** — examples, tutorials, typo fixes ([clutch-docs](https://github.com/clutchprotocol/clutch-docs))
- **Tests** — unit/integration coverage ([clutch-hub-api](https://github.com/clutchprotocol/clutch-hub-api), [clutch-hub-sdk-js](https://github.com/clutchprotocol/clutch-hub-sdk-js))
- **Explorer UI** — readability and search ([clutch-explorer](https://github.com/clutchprotocol/clutch-explorer))
- **Demo app** — UX polish ([clutch-hub-demo-app](https://github.com/clutchprotocol/clutch-hub-demo-app))

---

## Get help

- **This discussion** — ask questions, share ideas, introduce yourself
- **Repo issues** — bugs and feature requests per repository
- **Docs FAQ** — https://docs.clutchprotocol.io/reference/faq
- **Email** — hello@clutchprotocol.io

---

## Questions for the community

We would love your feedback on:

1. **Domain-specific chain vs. smart contracts** — is a custom non-EVM chain the right tradeoff for ride-sharing?
2. **Referrer-fee model** — does on-chain app-builder incentives (2%+2% on RidePay) make sense?
3. **What would you build** on this stack?

Reply below — maintainer is active and happy to go deep on architecture, tx format, or deployment.

---

*Maintained by [Mehran Mazhar](https://github.com/MehranMazhar) and contributors. MIT / Apache-2.0 per repo.*
