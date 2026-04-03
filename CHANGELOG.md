# Changelog

All notable changes to the KAT Score API are documented here.

---

## v0.2.0 — April 2026

### Added

- **Wallet type classification** — every score response now includes a `wallet_type` field classifying the wallet as one of:
  - `autonomous_agent` — consistent automated behaviour, agent-compatible
  - `likely_exchange` — high-volume hub patterns typical of centralised exchanges
  - `smart_contract` — contract address detected
  - `retail_wallet` — human-operated wallet with irregular patterns
  - `insufficient_history` — fewer than 10 transactions; score is provisional
  - `unknown` — insufficient signals to classify

- **`scope_warning` field** — when the wallet type materially affects score interpretation, a plain-English warning is included in the response explaining how to interpret the score for that wallet type (e.g. exchange wallets score differently by design)

- **Taostats API integration for Bittensor / TAO scoring** — replaced limited RPC block-scan fallback with the full Taostats API data pipeline:
  - Transfer history (up to 50 transactions) via `api/transfer/v1`
  - Account data including balance, wallet age, and subnet staking positions via `api/account/latest/v1`
  - Alpha balances (per-subnet staking positions) extracted from account response for validators operating across multiple subnets
  - Stake portfolio and miner registration where available on current API plan
  - Falls back to Substrate RPC if API key is not configured

- **Extended TAO behavioral features** — TAO scoring now surfaces:
  - `nonce` — total lifetime extrinsics (proxy: total transfer count via Taostats pagination)
  - `subnet_count` — number of subnets the wallet holds alpha positions on
  - `stake_total` — total TAO staked across all positions
  - `is_delegate` — delegate/hotkey status inferred from account data
  - `inbound_count` / `outbound_count` — directional transfer breakdown
  - `volume_total` — sum of all transfer amounts in TAO

- **Bittensor scoring context updated** — Claude Haiku scoring prompt now includes explicit thresholds: nonce > 1000 is a strong positive signal; subnet_count > 0 indicates active participation; stake_total > 1 TAO indicates meaningful network investment; is_delegate = true is a strong positive signal

- **Extended chain support** — added five additional chains:
  - Bitcoin (`btc`)
  - Solana (`sol`)
  - Avalanche (`avax`)
  - Hyperliquid (`hype`)
  - Bittensor / TAO (`tao`)

- **Chain stats endpoint** — `GET /api/v1/chain-stats` returns per-chain scoring statistics including query volume, average score, and score distribution

- **Pay-as-you-go pricing** — `$0.005 per query` top-up model now available; free tier remains 100 queries on signup with no expiry

### Changed

- TAO scoring: `wallet_age_days` now derived from Taostats `created_on_date` field (accurate calendar date) rather than estimated from block number
- TAO scoring: subnet registrations now pulled from `alpha_balances` array in account response, capturing all subnets where the coldkey holds staking positions — significantly more complete than the miner registration endpoint alone
- `force_refresh` parameter is now a **query parameter** (`?force_refresh=true`), not a request body field
- README and QUICKSTART updated to reflect 10-chain support, wallet type classification, scope warnings, and current pricing

### Fixed

- Taostats API authentication: corrected from `Authorization: Bearer <key>` to `Authorization: <key>` (Taostats uses raw key, no Bearer prefix)
- Taostats transfer pagination: removed `page=0` parameter (Taostats uses 1-based pagination; `page=0` returns empty results)

---

## v0.1.0 — March 2026

Initial beta release.

### Added

- **KAT Score endpoint** — `POST /api/v1/score` returns a full Known Agent Trust Score for any EVM wallet address
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
- **Rate limiting** — registration endpoint rate-limited to 3 attempts/IP/hour

---

*For questions or feedback: [hello@kaelai.io](mailto:hello@kaelai.io)*
