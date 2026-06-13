# TheGist

> A fully decentralized, anonymous hyperlocal messaging protocol built natively on Stellar and Soroban.

No servers own your data. No identity is required. Only a Stellar wallet and a location.

---

## What Is TheGist?

TheGist is a Web3 protocol where every message is a **signed, on-chain event anchored to a geographic location**. A gist is a short piece of content — text, image, or link — cryptographically signed by a Stellar keypair and permanently tied to a geohash on Soroban.

Anyone within range can read it. No account. No profile. No algorithm. Just the chain and a coordinate.

---

## How the Protocol Works

```
1. User composes a gist in a mobile or web client
2. Content is pinned to IPFS → produces a CID
3. CID + geohash (precision 7) + author public key → signed with Stellar keypair
4. Signed transaction submitted to Soroban GistRegistry contract
5. Contract emits GistPosted event on-chain
6. Indexer listens for GistPosted events → writes to PostGIS
7. Clients query indexer via GraphQL → render nearby gists on map
```

### Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Clients                              │
│         Mobile (Expo)              Web (Next.js)            │
│    WalletConnect / Freighter         Freighter Wallet        │
└──────────────┬──────────────────────────────┬──────────────┘
               │  Stellar Txn (sign + submit)  │  GraphQL Query
               ▼                              ▼
┌──────────────────────────┐   ┌──────────────────────────────┐
│    Soroban Contracts      │   │      Indexer  (Node.js)       │
│  ┌────────────────────┐  │   │                              │
│  │  GistRegistry      │──┼───►  Polls Soroban RPC for       │
│  │  GistVault         │  │   │  GistPosted events           │
│  │  LocationVerifier  │  │   │  Decodes CID + geohash       │
│  └────────────────────┘  │   │  Writes to PostGIS           │
└──────────────────────────┘   │  Serves GraphQL API          │
               │               └──────────────────────────────┘
               ▼
┌──────────────────────────┐
│           IPFS            │
│  Content-addressed store  │
│  CID pinned per gist      │
└──────────────────────────┘
```

---

## Repositories

| Repo | Description |
|------|-------------|
| [theGist-Meta](https://github.com/TheGist-Org/theGist-Meta) | Central coordination: architecture, roadmap, and contributing guidelines |
| [TheGist-contracts](https://github.com/TheGist-Org/TheGist-contracts) | Soroban smart contracts in Rust — GistRegistry, GistVault, LocationVerifier |
| [TheGist-API](https://github.com/TheGist-Org/TheGist-API) | Soroban event indexer and read-only GraphQL API built with Node.js and PostGIS |
| [TheGist-web](https://github.com/TheGist-Org/TheGist-web) | Next.js decentralized map client — post and browse gists in the browser |
| [TheGist-mobile](https://github.com/TheGist-Org/TheGist-mobile) | Expo React Native app — GPS-native iOS and Android client |

---

## Roadmap

### Phase 1 — Contracts + Indexer
- [x] GistRegistry Soroban contract
- [x] GistVault tipping contract
- [x] LocationVerifier contract
- [ ] Soroban event indexer (Node.js + Stellar SDK)
- [ ] PostGIS schema and geospatial queries
- [ ] GraphQL API (Apollo Server)

### Phase 2 — API + Web
- [ ] Next.js map interface with Mapbox GL JS
- [ ] Freighter wallet integration
- [ ] IPFS content pinning from the browser
- [ ] Gist expiry (24h default)
- [ ] Read-only GraphQL queries live in production

### Phase 3 — Mobile + Launch
- [ ] Expo iOS / Android app
- [ ] WalletConnect v2 integration
- [ ] Camera + IPFS image attachments
- [ ] Push notifications for nearby gists
- [ ] Testnet public launch
- [ ] Mainnet launch

---

## Protocol Principles

- **Decentralized** — no central server controls message routing or storage
- **Anonymous** — no email, username, or account required; only a Stellar address
- **Hyperlocal** — every gist is anchored to a geohash; relevance is distance, not engagement
- **Immutable** — on-chain anchoring ensures gists cannot be silently deleted or altered
- **Permissionless** — anyone with a Stellar wallet can post or read

---

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for development setup, branch conventions, and how to open issues or PRs across repos.

---

## License

MIT
