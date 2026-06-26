<div align="center">
  <img src="https://avatars.githubusercontent.com/u/211993100" width="140" alt="Clutch Protocol Logo" />

  # Clutch Protocol

  **Open-source ride-sharing blockchain — on-chain ride lifecycle, client-side signing, driver-first CLT payouts.**

  *Aura consensus · Rust node · GraphQL Hub API · JavaScript SDK*

  [![Alpha](https://img.shields.io/badge/status-alpha-orange.svg)](#status)
  [![Rust](https://img.shields.io/badge/Built%20with-Rust-orange.svg)](https://www.rust-lang.org/)
  [![Docs](https://img.shields.io/badge/docs-clutchprotocol.io-blue.svg)](https://docs.clutchprotocol.io)

  **[Try stage demo](https://app-stage.clutchprotocol.io)** · **[Documentation](https://docs.clutchprotocol.io)** · [Website](https://clutchprotocol.io) · [npm SDK](https://www.npmjs.com/package/clutch-hub-sdk-js)

</div>

---

## Try in 3 steps (no install)

1. **Open the demo** → [app-stage.clutchprotocol.io](https://app-stage.clutchprotocol.io) (public testnet)
2. **Create a wallet** → choose Passenger or Driver, then click **Request CLT** (faucet)
3. **Run a ride** → passenger: request on the map · driver: view requests and submit an offer

Read the full guide: [Ride lifecycle](https://docs.clutchprotocol.io/getting-started/ride-lifecycle) · [Environments](https://docs.clutchprotocol.io/getting-started/environments)

---

## Run locally in 3 steps

1. **Start the stack**
   ```bash
   git clone https://github.com/clutchprotocol/clutch-deploy.git && cd clutch-deploy
   cp .env.example .env && docker compose up -d
   ```
2. **Open the demo** → http://localhost:5173 · API health → http://localhost:3000/health
3. **Build with the SDK** → `npm install clutch-hub-sdk-js` — see [Quick Start](https://docs.clutchprotocol.io/getting-started/quickstart)

---

## What is Clutch?

Clutch Protocol is an open, modular blockchain stack for decentralized ride-sharing. Apps connect through a GraphQL Hub API and JavaScript SDK; transactions are signed client-side and settled on-chain with Aura consensus.

**New here?** Start with the pinned [Discussions welcome thread](https://github.com/orgs/clutchprotocol/discussions) or the [docs intro](https://docs.clutchprotocol.io/intro).

**CLT economics:** Drivers keep most of each fare. Referrers earn up to 4% (default 2%+2%) on RidePay. Validators earn a fixed block reward (50 CLT/block), separate from rides. See [CLT Economics](https://docs.clutchprotocol.io/clutch-node/clt-economics).

> **Note:** Community governance (DAO) is on the [roadmap](#roadmap). It is not yet implemented in the current codebase.

---

## Repositories

| Repository | Role | Stack |
|------------|------|-------|
| [clutch-node](https://github.com/clutchprotocol/clutch-node) | Blockchain core (Aura, custom txs) | Rust |
| [clutch-hub-api](https://github.com/clutchprotocol/clutch-hub-api) | App bridge — GraphQL, faucet, JWT auth | Rust |
| [clutch-hub-sdk-js](https://github.com/clutchprotocol/clutch-hub-sdk-js) | Client SDK — signing, queries, subscriptions | TypeScript |
| [clutch-hub-demo-app](https://github.com/clutchprotocol/clutch-hub-demo-app) | Reference passenger/driver demo | React / Vite |
| [clutch-explorer](https://github.com/clutchprotocol/clutch-explorer) | Block explorer (indexer + REST API) | Rust + React |
| [clutch-deploy](https://github.com/clutchprotocol/clutch-deploy) | Full-stack Docker Compose | Docker |
| [clutch-docs](https://github.com/clutchprotocol/clutch-docs) | Developer documentation site | Docusaurus |
| [clutchprotocol.github.io](https://github.com/clutchprotocol/clutchprotocol.github.io) | Marketing website | HTML / CSS |
| [.github](https://github.com/clutchprotocol/.github) | Organization profile | — |

**Canonical docs:** https://docs.clutchprotocol.io

---

## Architecture

```
Demo App / Your dApp
        │
        ▼
  clutch-hub-sdk-js  (client-side signing)
        │
        ▼
  clutch-hub-api     (GraphQL + /faucet)
        │
        ▼
  clutch-node        (WebSocket JSON-RPC, Aura validators)
        │
        ▼
  clutch-explorer    (indexes blocks → Postgres → REST UI)
```

---

## SDK example

```bash
npm install clutch-hub-sdk-js
```

```javascript
import { ClutchHubSdk } from 'clutch-hub-sdk-js';

const sdk = new ClutchHubSdk('http://localhost:3000', publicKey);

await sdk.requestFaucet(publicKey);

const unsigned = await sdk.createUnsignedRideRequest({
  pickup: { latitude: 35.7, longitude: 51.4 },
  dropoff: { latitude: 35.8, longitude: 51.5 },
  fare: 1000,
});
const signed = await sdk.signTransaction(unsigned, privateKey);
await sdk.submitTransaction(signed.rawTransaction);
```

See [Ride Lifecycle](https://docs.clutchprotocol.io/getting-started/ride-lifecycle) for the full passenger/driver flow.

---

## Live environments

| Environment | Demo | API |
|-------------|------|-----|
| Local | http://localhost:5173 | http://localhost:3000 |
| Stage | https://app-stage.clutchprotocol.io | https://api-stage.clutchprotocol.io |
| Production demo | https://demo.clutchprotocol.io | — |

---

## Technology

| Layer | Technology |
|-------|------------|
| Consensus | Aura (authority round-robin) |
| Blockchain | Custom Rust, non-EVM RLP transactions |
| Signing | secp256k1, Keccak-256, client-side only |
| P2P | libp2p |
| Hub API | GraphQL HTTP + WebSocket subscriptions |
| Node RPC | WebSocket JSON-RPC |

---

## CLT economics

| Layer | Mechanism | Default |
|-------|-----------|---------|
| **RidePay** | Referrer fees + driver remainder | 2% request + 2% offer |
| **Blocks** | Reward to block author | 50 CLT per block |

Example: 10 CLT fare, one RidePay, both referrers → driver 8 CLT, referrers 1 CLT each.

Full details: [docs.clutchprotocol.io/clutch-node/clt-economics](https://docs.clutchprotocol.io/clutch-node/clt-economics)

---

## Roadmap {#roadmap}

| Phase | Status | Milestone |
|-------|--------|-----------|
| Core stack + demo | Done | Node, Hub API, SDK, demo app, deploy |
| Developer docs | Done | [docs.clutchprotocol.io](https://docs.clutchprotocol.io) |
| Block explorer | Done | [clutch-explorer](https://github.com/clutchprotocol/clutch-explorer) |
| Public testnet (stage) | Live | Stage URLs + faucet |
| DAO governance | Planned | On-chain community voting |
| Cross-chain (Cosmos IBC) | Planned | Interoperability |
| Layer-2 scaling | Planned | Higher throughput |

---

## Status {#status}

Alpha software — APIs may change without notice. Use at your own risk.

---

## Contribute

1. Fork a repository
2. Create a feature branch
3. Follow [Conventional Commits](https://www.conventionalcommits.org/)
4. Open a pull request

- [GitHub Discussions](https://github.com/orgs/clutchprotocol/discussions)
- [Documentation](https://docs.clutchprotocol.io)
- Report bugs via GitHub Issues in the relevant repo

---

## Security

- Private keys never leave the client — all signing is done via the SDK
- Wallet-based JWT auth (no username/password)
- Every transaction is auditable on-chain

Details: [Security](https://docs.clutchprotocol.io/reference/security)

---

<div align="center">

**Building decentralized mobility, one block at a time**

*Created and maintained by [Mehran Mazhar](https://github.com/MehranMazhar)*

**[Star us](https://github.com/clutchprotocol) · [Stage demo](https://app-stage.clutchprotocol.io) · [Docs](https://docs.clutchprotocol.io) · [Discussions](https://github.com/orgs/clutchprotocol/discussions)**

</div>
