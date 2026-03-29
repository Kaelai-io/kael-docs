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
![Version](https://img.shields.io/badge/version-v0.1.0-6b7f8a?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-6b7f8a?style=flat-square)

---

## Quick Start

Get a free API key at **[kaelai.io](https://kaelai.io)** — no credit card, instant access.

```bash
curl -X POST https://kaelai.io/api/v1/score/ \
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
| `POST` | `/api/v1/score/` | Score a wallet — returns full KAT Score |
| `GET`  | `/api/v1/score/{address}/history` | Full score history for a wallet |
| `GET`  | `/api/v1/score/{address}/trend` | Trend direction over last N scores |
| `POST` | `/api/v1/keys/register` | Self-serve API key registration (no auth) |
| `GET`  | `/api/v1/stats` | Public usage statistics |

---

## Authentication

All scoring endpoints require a Bearer token:

```
Authorization: Bearer kael_live_YOUR_KEY
```

Get your key instantly at [kaelai.io](https://kaelai.io).

---

## Supported Chains

ETH · Base · Polygon · BSC · Arbitrum

Pass the `chain` field in your request body:

```json
{
  "wallet_address": "0x...",
  "chain": "base"
}
```

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
