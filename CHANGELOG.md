# Changelog

All notable changes to the KAT Score API are documented here.

---

## v0.1.0 — March 2026

Initial beta release.

### Added

- **KAT Score endpoint** — `POST /api/v1/score/` returns a full Known Agent Trust Score for any EVM wallet address
- **Five-dimension scoring engine** — each wallet is scored across five independent dimensions (0–20 each):
  - Behavioral Consistency
  - Transaction Legitimacy
  - Wallet Age & History
  - Counterparty Quality
  - Volume Stability
- **Bond-style grade** — overall score mapped to AAA / AA / A / BBB / BB / B / CCC rating
- **Plain-English reasoning** — every response includes an AI-generated explanation of the score
- **Redis caching** — 24-hour score cache; average cached response time 9ms
- **Score history endpoint** — `GET /api/v1/score/{address}/history` returns full scoring history for a wallet, newest first
- **Score trend endpoint** — `GET /api/v1/score/{address}/trend` returns trend direction (improving / stable / declining) over a configurable window
- **Force refresh** — `?force_refresh=true` query parameter bypasses cache and triggers a fresh on-chain analysis
- **Self-serve API key registration** — `POST /api/v1/keys/register` generates a `kael_live_` key instantly, no waitlist
- **Public stats endpoint** — `GET /api/v1/stats` returns live usage statistics (cached 5 minutes)
- **Multi-chain support** — ETH, Base, Polygon, BSC, Arbitrum
- **Rate limiting** — 100 queries/hour on the free tier; registration endpoint rate-limited to 3 attempts/IP/hour

---

*For questions or feedback: [hello@kaelai.io](mailto:hello@kaelai.io)*
