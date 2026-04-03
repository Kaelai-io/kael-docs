# Quickstart — KAT Score API

Five steps to your first trust score.

---

## Step 1 — Get your API key

Visit **[kaelai.io](https://kaelai.io)** and fill in the signup form. Your `kael_live_` key is generated instantly and shown once — store it securely.

No credit card. No waitlist. **100 free queries** included on signup — no expiry.

---

## Step 2 — Make your first request

Replace `kael_live_YOUR_KEY` with your actual key and the wallet address with any supported chain address:

### EVM (Ethereum, Base, Polygon, BSC, Arbitrum, Avalanche)

```bash
curl -X POST https://kaelai.io/api/v1/score \
  -H "Authorization: Bearer kael_live_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "wallet_address": "0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045",
    "chain": "eth"
  }'
```

### Bittensor / TAO

```bash
curl -X POST https://kaelai.io/api/v1/score \
  -H "Authorization: Bearer kael_live_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "wallet_address": "5GKH9FPPnWSUoeeTJp19wVtd84XqFW4pyK2ijV2GsFbhTrP1",
    "chain": "tao"
  }'
```

> **Bittensor tip:** Score the **hotkey** address for richer behavioural data and higher confidence. Coldkey addresses (treasury/owner keys) have limited direct transaction history — the hotkey is where validator activity lives.

You'll receive a full KAT Score response in under 10ms for cached wallets, or under 5 seconds for a fresh on-chain analysis.

---

## Step 3 — Understand the response

```json
{
  "wallet_address": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
  "overall_score": 78,
  "grade": "A",
  "confidence": 0.91,
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
  "reasoning": "Established wallet with 2+ years of consistent on-chain activity..."
}
```

### Key fields

| Field | Description |
|---|---|
| `overall_score` | 0–100 trust score |
| `grade` | Bond-style rating: AAA → CCC |
| `confidence` | 0–1 reliability of the score based on data depth |
| `wallet_type` | Classification: `autonomous_agent`, `likely_exchange`, `smart_contract`, `retail_wallet`, `insufficient_history`, or `unknown` |
| `scope_warning` | Plain-English note when wallet type affects score interpretation (e.g. exchange wallets score differently than agent wallets by design) |
| `reasoning` | AI-generated explanation of the score |

### Grade scale

| Grade | Score Range | What it means |
|-------|-------------|---------------|
| AAA   | 95–100 | Highest trust. Long history, consistent behaviour, clean counterparties. |
| AA    | 88–94  | Very high trust. Minor gaps at most. |
| A     | 80–87  | High trust. Solid on-chain profile. |
| BBB   | 70–79  | Good trust. Some minor flags or limited history. |
| BB    | 60–69  | Moderate trust. Proceed with normal diligence. |
| B     | 50–59  | Below average. Short history or anomalous patterns. |
| CCC   | 0–49   | Low trust. Significant risk signals. Transact with caution. |

### Five dimensions (each 0–20)

- **Behavioral Consistency** — Are transaction patterns regular and predictable?
- **Transaction Legitimacy** — Do transactions involve reputable contracts and protocols?
- **Wallet Age & History** — How long has the wallet been active?
- **Counterparty Quality** — Who has this wallet transacted with?
- **Volume Stability** — Is transaction volume stable or erratic?

---

## Step 4 — Force a fresh score

Results are cached for 24 hours. To bypass cache and trigger a fresh on-chain analysis, pass `force_refresh=true` as a query parameter:

```bash
curl -X POST "https://kaelai.io/api/v1/score?force_refresh=true" \
  -H "Authorization: Bearer kael_live_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"wallet_address": "0x...", "chain": "eth"}'
```

---

## Step 5 — Query score history and trend

Retrieve the full scoring history for any wallet (newest first):

```bash
curl https://kaelai.io/api/v1/score/0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/history \
  -H "Authorization: Bearer kael_live_YOUR_KEY"
```

Check whether a wallet's trust score is improving, stable, or declining:

```bash
curl "https://kaelai.io/api/v1/score/0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/trend?window=5" \
  -H "Authorization: Bearer kael_live_YOUR_KEY"
```

The `window` parameter controls how many recent scores to analyse (default 5, max 20). Response includes `direction` (`improving` / `stable` / `declining`), `delta`, and the individual scores.

---

## Pricing

| Tier | Cost | Notes |
|---|---|---|
| Free | 100 queries | Included on signup, no card required, never expires |
| Pay-as-you-go | $0.005 / query | Top up balance, pay per score |
| Subscriptions | Coming Q2 2026 | Monthly plans with volume discounts |

---

## Next steps

- Full API reference: [kaelai.io/docs](https://kaelai.io/docs)
- Questions: [hello@kaelai.io](mailto:hello@kaelai.io)
