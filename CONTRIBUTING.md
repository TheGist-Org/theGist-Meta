
---

## 4. Why This Setup Works Well for Contributors

- **Clear boundaries**: Each repo has one responsibility (contracts / backend / web / mobile).
- **Separation of tracks**:
  - Smart contract devs don’t have to touch React.
  - Frontend devs don’t need to know Soroban to contribute.
- **Central meta repo**:
  - Single entry point
  - Cross-repo issues, roadmap, architecture

When we move to **issues and contributor tasks**, we can:

- Use `gistpin-meta` for:
  - “Project: GistPin MVP” milestones
  - High-level “Epic: Location handling”, “Epic: Tipping”, etc.
- Use each track repo for:
  - Concrete implementation tickets (e.g., “Implement `post_gist` in GistRegistry”, “Implement /gists API route”, “Add MapView component”).

---

## 5. Next Step

If you’re happy with:

- The org structure
- Repo separation
- These baseline READMEs

then the next step is:

**Step 2: Define a minimal MVP scope and create initial GitHub issues per repo.**

We can do that next by:

1. Listing MVP features.
2. Breaking them into:
   - `gistpin-contracts` issues
   - `gistpin-backend` issues
   - `gistpin-web` issues
   - `gistpin-mobile` issues
3. Tagging them as `good first issue`, `track: contracts`, etc.

Before that, do you want to:

- Adjust the tech stack for any repo (e.g., Rust backend instead of Node)?
- Rename / add / remove any repos?
