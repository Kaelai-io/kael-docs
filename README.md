```
██╗  ██╗ █████╗ ███████╗██╗
██║ ██╔╝██╔══██╗██╔════╝██║
█████╔╝ ███████║█████╗  ██║
██╔═██╗ ██╔══██║██╔══╝  ██║
██║  ██╗██║  ██║███████╗███████╗
╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚══════╝
```

# KAT Score API — Known Agent Trust Scores for Autonomous AI Agents

Kael scores autonomous AI agent wallets on-chain and returns a Known Agent Trust (KAT) Score from 0 to 100. Query the API before your agent transacts with an unknown counterparty. Built for Bittensor subnet operators, x402 protocol developers, and agent infrastructure builders.

![API Status](https://img.shields.io/badge/API-Live-00c896?style=flat-square)
![Version](https://img.shields.io/badge/version-v0.2.0-6b7f8a?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-6b7f8a?style=flat-square)

---

## Quick Start

Get a free API key at **[kaelai.io](https://kaelai.io)** — no credit card, instant access.

```bash
curl -X POST https://kaelai.io/api/v1/score \
  -H "Authorization: Bearer kael_live_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"wallet_address": "0xYourAgentWalletAddress"}'
```

### Example Response

```json
{
  "wallet_address": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
  "overall_score": 78,
  "grade": "A",
  "confidence": 0.91,
  "cache_hit": true,
  "chain": "eth",
  "transactions_analysed": 50,
  "wallet_type": "autonomous_agent",
  "scope_warning": null,
  "dimension_scores": {
    "behavioral_consistency": 17,
    "transaction_legitimacy": 15,
    "wallet_age_and_history": 18,
    "counterparty_quality": 13,
    "volume_stability": 15
  },
  "reasoning": "Established wallet with 2+ years of consistent on-chain activity. Regular interaction patterns with reputable protocols. Counterparty quality slightly reduced by two unverified contract interactions in Q3. Overall profile is consistent with a legitimate autonomous agent."
}
```

> **Note:** `wallet_type` classifies the wallet as one of: `autonomous_agent`, `likely_exchange`, `smart_contract`, `retail_wallet`, `insufficient_history`, or `unknown`. When the wallet type affects score interpretation, `scope_warning` contains a plain-English explanation.

### Grade Scale

| Grade | Score | Trust Level |
|-------|-------|-------------|
| AAA   | 95–100 | Highest trust — long-established, consistent agent |
| AA    | 88–94  | Very high trust |
| A     | 80–87  | High trust — solid on-chain history |
| BBB   | 70–79  | Good trust — minor flags |
| BB    | 60–69  | Moderate trust — limited history or minor anomalies |
| B     | 50–59  | Below average — proceed with caution |
| CCC   | 0–49   | Low trust — significant risk signals |

---

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/api/v1/score` | Score a wallet — returns full KAT Score |
| `GET`  | `/api/v1/score/{address}/history` | Full score history for a wallet |
| `GET`  | `/api/v1/score/{address}/trend` | Trend direction over last N scores |
| `POST` | `/api/v1/keys/register` | Self-serve API key registration (no auth) |
| `GET`  | `/api/v1/stats` | Public usage statistics |
| `GET`  | `/api/v1/chain-stats` | Per-chain scoring statistics |

---

## Authentication

All scoring endpoints require a Bearer token:

```
Authorization: Bearer kael_live_YOUR_KEY
```

Get your key instantly at [kaelai.io](https://kaelai.io).

---

## Supported Chains

| Chain | `chain` value |
|---|---|
| Bitcoin | `btc` |
| Ethereum | `eth` |
| Solana | `sol` |
| Base | `base` |
| BNB Smart Chain | `bsc` |
| Polygon | `polygon` |
| Arbitrum | `arbitrum` |
| Avalanche | `avax` |
| Hyperliquid | `hype` |
| Bittensor | `tao` |

Pass the `chain` field in your request body:

```json
{
  "wallet_address": "0x...",
  "chain": "base"
}
```

Default is `eth` if omitted.

### Bittensor / TAO — Coldkey vs Hotkey

On Bittensor, validators operate using two wallet types. **Coldkeys** hold funds and subnet registrations but have limited direct transaction history. **Hotkeys** contain all operational activity — weight setting, miner scoring, and validation extrinsics. For counterparty trust assessment, scoring the hotkey address returns richer behavioural data and higher confidence scores. Both wallet types are supported with `chain: tao`.

---

## Pricing

| Tier | Price | Details |
|---|---|---|
| Free | 0 | 100 queries on signup, no credit card required, never expires |
| Pay-as-you-go | $0.005 / query | Top up and query at will — no subscription required |
| Subscription tiers | Coming Q2 2026 | Monthly plans with volume discounts and additional features |

---

## Documentation

Full API reference and integration guides: **[kaelai.io/docs](https://kaelai.io/docs)**

---

## Links

- 🔑 **Get an API key:** [kaelai.io](https://kaelai.io)
- 📖 **Documentation:** [kaelai.io/docs](https://kaelai.io/docs)
- 📬 **Contact:** [hello@kaelai.io](mailto:hello@kaelai.io)

---

*Built for the agent economy — [kaelai.io](https://kaelai.io)*
