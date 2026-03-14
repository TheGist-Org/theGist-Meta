# gistpin-Meta
Central coordination repo: high-level roadmap, cross-repo architecture, global CONTRIBUTING, global CODE_OF_CONDUCT, and cross-cutting issues.

GistPin is a location-aware micro-messaging platform built on the Stellar ecosystem
(Soroban smart contracts + Web2 stack). This repo acts as the **coordination hub**
for the entire project.

If you're new, **start here**.

---

## Repositories

GistPin is split into focused repos per track:

- **Contracts (on-chain logic)**
  - [`gistpin-contracts`](https://github.com/TheGist-Org/TheGist-contracts)
- **Backend (API + indexer + DB)**
  - [`gistpin-backend`](https://github.com/TheGist-Org/TheGist-API)
- **Web (frontend)**
  - [`gistpin-web`](https://github.com/TheGist-Org/TheGist-web)
- **Mobile**
  - [`gistpin-mobile`](https://github.com/TheGist-Org/TheGist-mobile)

Each repo has its own `README` with detailed setup and contribution info.

---

## High-Level Architecture

**Goal**: Anonymous, hyperlocal micro-posts ("gists") that are:

- Geotagged and discoverable via map UI
- Anchored on Stellar via Soroban contracts
- Indexed and queryable via a scalable Web2 backend

### Components

1. **Soroban contracts** (`gistpin-contracts`)

   - `GistRegistry` contract:
     - Stores minimal gist metadata on-chain:
       - `gist_id`
       - `author` (optional)
       - `location_cell` (coarse geo cell)
       - `content_hash` (IPFS/Arweave CID)
       - `created_at`
     - Indexes gists by location cell
   - Future:
     - Tipping / staking / moderation contracts

2. **Backend & Indexer** (`gistpin-backend`)

   - Listens to contract events
   - Stores enriched gist data in Postgres + PostGIS
   - Exposes a REST API for:
     - `GET /gists?lat=&lon=&radius=`
     - `POST /gists`
     - Future: tipping, moderation, etc.
   - Bridges to IPFS/Arweave for full content storage

3. **Web Frontend** (`gistpin-web`)

   - React + TS map UI
   - Fetches gists from `gistpin-backend`
   - Allows users to create new gists
   - Links to on-chain transactions for verification

4. **Mobile App** (`gistpin-mobile`)

   - Uses the same API as the web frontend
   - Focused on a clean, location-first UX for posting & browsing nearby gists

---

## Getting Started

1. **Read architecture**: `docs/architecture-overview.md`
2. **Pick a track**:
   - Contracts → `gistpin-contracts`
   - Backend → `gistpin-backend`
   - Web frontend → `gistpin-web`
   - Mobile → `gistpin-mobile`
3. Follow the setup instructions in that repo's `README`.

---

## Contributing

- General contribution guidelines: [CONTRIBUTING.md](./CONTRIBUTING.md)
- Code of conduct: [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)

We will manage **cross-cutting issues and milestones** in this repo, and more
granular implementation issues directly in the relevant track repo.
