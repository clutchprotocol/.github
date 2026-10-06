<div align="center">
  <img src="https://avatars.githubusercontent.com/u/211993100" width="140" alt="Clutch Protocol Logo" />

  # Clutch Protocol

  **Open-source ride-sharing on a blockchain — the whole ride lifecycle settles on-chain, keys stay in your own wallet, and drivers get paid in seconds instead of next week.**

  *Aura consensus · Rust node · GraphQL Hub API · JavaScript SDK*

  [![Alpha](https://img.shields.io/badge/status-alpha-orange.svg)](#status)
  [![Mainnet](https://img.shields.io/badge/mainnet-capped%20pilot%20live-brightgreen.svg)](#live-environments)
  [![Rust](https://img.shields.io/badge/Built%20with-Rust-orange.svg)](https://www.rust-lang.org/)
  [![Docs](https://img.shields.io/badge/docs-clutchprotocol.io-blue.svg)](https://docs.clutchprotocol.io)

  **[Mainnet app (pilot)](https://app.clutchprotocol.io)** · **[Try the testnet](https://app-stage.clutchprotocol.io)** · **[Documentation](https://docs.clutchprotocol.io)** · [Website](https://clutchprotocol.io) · [npm SDK](https://www.npmjs.com/package/clutch-hub-sdk-js)

</div>

---

## Try in 3 steps (no install, ~5 min the first time)

1. **Open the demo** → [app-stage.clutchprotocol.io](https://app-stage.clutchprotocol.io) (public testnet) and connect your wallet (MetaMask or Trust Wallet) — Passenger or Driver.
2. **Get test CLT** → ☰ → **Wallet** → **Top up** shows your wallet's permanent Tron address. Copy it, paste it into the **USDT** box of the [Nile faucet](https://nileex.io/join/getJoinPage), pass its human check, and click Obtain — it sends 1,000 test USDT straight to that address, no Tron wallet needed. The treasury credits the matching CLT once it sees the transfer, usually within a few minutes; keep the panel open and your address is polled first.
3. **Run a ride** → passenger: request on the map · driver: view requests and submit an offer

No signup and no real money. You need a wallet that can sign a message, such as MetaMask or Trust Wallet (on a phone, open the page inside the wallet app); the app never holds your keys. Stage settles on Tron's Nile testnet, whose USDT has no value. Waiting for the deposit to be credited is most of the five minutes.

**Want the mainnet instead?** [app.clutchprotocol.io](https://app.clutchprotocol.io) is a capped pilot with real USDT: top up with USDT (TRC-20 on Tron), up to $100 per top-up and $200 per day. A network fee is taken from each top-up: $4.00 the first time and $2.00 after. The relay charges less today ($3.00 and $1.50); the difference is not refunded and stays in the reserve as backing. Withdrawals are not open yet. It is alpha software, so top up only what you can afford to lose.

Read the full guide: [Ride lifecycle](https://docs.clutchprotocol.io/getting-started/ride-lifecycle) · [Deposits](https://docs.clutchprotocol.io/clutch-treasury/deposits) · [Environments](https://docs.clutchprotocol.io/getting-started/environments)

---

## What is Clutch?

1. **What it is:** Clutch Protocol is an open-source ride-sharing blockchain. Passengers and drivers send ride requests, offers and payments as transactions on its own chain, [`clutch-node`](https://github.com/clutchprotocol/clutch-node).
2. **How apps use it:** [`clutch-hub`](https://github.com/clutchprotocol/clutch-hub) has the Hub API, a JavaScript SDK that signs on the user's device, and a reference app for passengers and drivers. [`clutch-explorer`](https://github.com/clutchprotocol/clutch-explorer) shows the blocks and transactions.
3. **Money and servers:** Rides are paid in CLT, a token fully backed by USDT, and [`clutch-treasury`](https://github.com/clutchprotocol/clutch-treasury) gives CLT for USDT and pays USDT back. [`clutch-deploy`](https://github.com/clutchprotocol/clutch-deploy) runs the public testnet and the mainnet. The mainnet is live as a capped pilot: top-ups are open, withdrawals are not open yet.

**Why on-chain actually buys you something here — not just "no middleman":**

- **Payout speed.** Payment settles on-chain in seconds when a ride completes. No weekly payout cycle, no "pending balance." The driver has the money before the next pickup.
- **No chargebacks.** The passenger signs the payment directly, so there's no card issuer that can claw it back three weeks later. (The honest flip side: passengers give up that protection — see [What's not built yet](#honest-status).)
- **You own the account.** No email/password. Your own wallet holds the keypair (MetaMask and Trust Wallet work); keys never leave it. Auth is a signed challenge, not a stored credential.
- **Auditable end to end.** Every step — request, offer, acceptance, payment, cancellation — is a typed transaction on a public ledger.
- **Fully open source.** Run the entire stack locally with one `docker compose` command (below).

**CLT economics:** Drivers keep the remainder of each fare. Referrers earn up to 4% (default 2%+2%) on RidePay. Validators earn a flat 1,000 CLT ($0.001) fee per transaction, credited to the block author — no block reward, no share of the fare. CLT is fully reserved: 1 USD = 1,000,000 CLT, minted only against USDT deposits and redeemable back to USDT. See [CLT Economics](https://docs.clutchprotocol.io/clutch-node/clt-economics).

---

## Honest status — what works, what doesn't {#honest-status}

Clutch is **alpha** and built in the open. Being upfront about the edges:

**Working today**
- On-chain ride lifecycle: request → offer → acceptance → pay → cancel, all as signed transactions
- Rust node with Aura consensus (~1s blocks), libp2p P2P, WebSocket JSON-RPC
- GraphQL Hub API with wallet-based (signed-challenge) JWT auth
- Fully-reserved CLT: USDT (TRC-20) deposits mint CLT, redemptions burn it back to USDT (live since 2026-09-04)
- Client SDK (npm), reference React demo, block explorer, one-command local stack
- Public stage testnet you can use right now
- Mainnet pilot (chain 1000): open to every account since 2026-10-05, with small limits. Top-ups are open; withdrawals are not open yet

**Not built yet (and this is the interesting part)**
- **Production hardening of the mainnet** — the pilot's three validators run on one host, the treasury's mint and payout keys are plain keys on the server, and the crypto has not been audited. That is why the limits are small. See [Mainnet readiness](https://docs.clutchprotocol.io/reference/mainnet-readiness)
- **Reputation / ratings** — no driver or rider scoring
- **Dispute resolution** — cancellations are on-chain, but there's no arbitration when two parties disagree, and no no-show / fraud handling beyond cancel
- **DAO governance** — on the roadmap, not in the code
- Matching is simple; there's no surge/pricing engine or geospatial optimization

The operational layer (disputes, reputation, matching) is genuinely the hard part, and it's where I'd most value ideas and contributors. If you've built payment or marketplace infra, [the discussions](https://github.com/orgs/clutchprotocol/discussions) are open.

---

## Run locally in 3 steps

1. **Clone and set a JWT secret** — the Hub API refuses the placeholder shipped in `.env.example`
   ```bash
   git clone https://github.com/clutchprotocol/clutch-deploy.git && cd clutch-deploy
   cp .env.example .env
   sed -i "s/^JWT_SECRET=.*/JWT_SECRET=$(openssl rand -hex 32)/" .env
   ```
   (PowerShell equivalent in the [Quick Start](https://docs.clutchprotocol.io/getting-started/quickstart).)
2. **Start the stack** → `docker compose up -d`, then open the demo at http://localhost:5173 · API health → http://localhost:3000/health
3. **Build with the SDK** → `npm install clutch-hub-sdk-js` — see [Quick Start](https://docs.clutchprotocol.io/getting-started/quickstart)

---

## Repositories

| Repository | Role | Stack |
|------------|------|-------|
| [clutch-node](https://github.com/clutchprotocol/clutch-node) | Blockchain core (Aura, custom txs) | Rust |
| [clutch-hub](https://github.com/clutchprotocol/clutch-hub) | The Hub API (GraphQL app bridge, JWT auth), the client SDK (signing, queries, subscriptions) and the reference passenger/driver demo | Rust + TypeScript + React |
| [clutch-treasury](https://github.com/clutchprotocol/clutch-treasury) | Fully-reserved CLT — USDT deposits, four-eyes mint, redemptions | Rust |
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
  clutch-hub-api     (GraphQL + WebSocket subscriptions)
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

// Pass the private key so the SDK can sign the auth challenge + transactions locally.
// In a browser app, pass a signer for the user's wallet (MetaMask, Trust Wallet) instead of a key:
//   const signer = await connectWallet((await discoverInjectedWallets())[0]);
const sdk = new ClutchHubSdk('http://localhost:3000', publicKey, privateKey);

// Fund the wallet first: deposit USDT (TRC-20) to its Tron address — there is no faucet.
// https://docs.clutchprotocol.io/clutch-treasury/deposits

const unsigned = await sdk.createUnsignedRideRequest({
  pickup: { latitude: 35.7, longitude: 51.4 },
  dropoff: { latitude: 35.8, longitude: 51.5 },
  fare: 5_000_000n, // $5.00 — amounts are bigint, at 1 USD = 1,000,000 CLT
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
| Mainnet | https://app.clutchprotocol.io | https://api.clutchprotocol.io |

Stage runs the public testnet (chain 2077). Mainnet runs chain 1000 as a capped pilot and has been open to every account since 2026-10-05. You get CLT there by topping up with USDT (TRC-20 on Tron): at most $100 per top-up and $200 per day. A network fee is taken from each top-up: $4.00 the first time and $2.00 after (the relay charges less today, $3.00 and $1.50, and the difference is not refunded: it stays in the reserve as backing). Withdrawals are not open yet. It is alpha software with real money, so use only what you can afford to lose. There is no mainnet explorer yet.

---

## Technology

| Layer | Technology |
|-------|------------|
| Consensus | Aura (authority round-robin, ~1s blocks) |
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
| **Every transaction** | Flat fee to the block author — no block reward, no share of the fare | 1,000 CLT ($0.001) |
| **Supply** | Fully reserved: minted only against USDT deposits, burned on redemption | 1 USD = 1,000,000 CLT |

Example: $5.00 fare (5,000,000 CLT), one RidePay, both referrers → driver 4,800,000 CLT ($4.80), each referrer 100,000 CLT ($0.10).

Full details: [docs.clutchprotocol.io/clutch-node/clt-economics](https://docs.clutchprotocol.io/clutch-node/clt-economics)

---

## Roadmap {#roadmap}

| Phase | Status | Milestone |
|-------|--------|-----------|
| Core stack + demo | Done | Node, Hub API, SDK, demo app, deploy |
| Developer docs | Done | [docs.clutchprotocol.io](https://docs.clutchprotocol.io) |
| Block explorer | Done | [clutch-explorer](https://github.com/clutchprotocol/clutch-explorer) |
| Public testnet (stage) | Live | Stage URLs; test CLT via Nile USDT deposits |
| Fully-reserved CLT | Live | USDT deposits mint CLT; redemptions burn it back (on the testnet since 2026-09-04) |
| Mainnet pilot | Live | Chain 1000, open to every account since 2026-10-05. Small limits ($100 per top-up, $200 per day). Top-ups are open; withdrawals are not open yet |
| Production mainnet | Planned | Independent validator operators, audited crypto, treasury keys behind a hardware boundary, higher limits. No fixed date — see [Mainnet readiness](https://docs.clutchprotocol.io/reference/mainnet-readiness) |
| Dispute resolution | Built, partly active | The rule that stops a rider taking a ride and keeping the money — a held fare releases to the driver after a set time — is implemented and merged. It is a genesis-committed consensus parameter: 5 minutes on the testnet and 2 hours on the mainnet. Arbitration and no-show handling are not built. |
| Reputation | Planned | Ratings, and the history a rating would have to be earned against |
| DAO governance | Planned | On-chain community voting |
| Cross-chain (Cosmos IBC) | Planned | Interoperability |
| Layer-2 scaling | Planned | Higher throughput |

---

## Status {#status}

Alpha software — APIs may change without notice. Use at your own risk. The mainnet pilot handles real money in small amounts: use only what you can afford to lose.

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

- Private keys never leave the user's device — a browser app holds none: the user's wallet (MetaMask, Trust Wallet) signs through the SDK
- Wallet-based JWT auth via signed challenge (no username/password)
- Every transaction is auditable on-chain

Details: [Security](https://docs.clutchprotocol.io/reference/security)

---

<div align="center">

**Building decentralized mobility, one block at a time**

*Created and maintained by [Mehran Mazhar](https://github.com/MehranMazhar)*

**[Star us](https://github.com/clutchprotocol) · [Stage demo](https://app-stage.clutchprotocol.io) · [Docs](https://docs.clutchprotocol.io) · [Discussions](https://github.com/orgs/clutchprotocol/discussions)**

</div>
