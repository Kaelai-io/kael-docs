# Quickstart — KAT Score API

Five steps to your first trust score.

---

## Step 1 — Get your API key

Visit **[kaelai.io](https://kaelai.io)** and fill in the signup form. Your `kael_live_` key is generated instantly and shown once — store it securely.

No credit card. No waitlist. Immediate access on the free tier (100 queries/hour).

---

## Step 2 — Make your first request

Replace `kael_live_YOUR_KEY` with your actual key and `0xYOUR_WALLET` with any EVM wallet address:

```bash
curl -X POST https://kaelai.io/api/v1/score/ \
  -H "Authorization: Bearer kael_live_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "wallet_address": "0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045",
    "chain": "eth"
  }'
```

You'll receive a full KAT Score response in under 10ms for cached wallets, or under 5 seconds for a fresh on-chain analysis.

---

## Step 3 — Understand your KAT Score

The `overall_score` is 0–100. The `grade` maps to a bond-style rating:

| Grade | Score Range | What it means |
|-------|-------------|---------------|
| AAA   | 95–100 | Highest trust. Long history, consistent behaviour, clean counterparties. |
| AA    | 88–94  | Very high trust. Minor gaps at most. |
| A     | 80–87  | High trust. Solid on-chain profile. |
| BBB   | 70–79  | Good trust. Some minor flags or limited history. |
| BB    | 60–69  | Moderate trust. Proceed with normal diligence. |
| B     | 50–59  | Below average. Short history or anomalous patterns. |
| CCC   | 0–49   | Low trust. Significant risk signals. Transact with caution. |

Each score also includes five **dimension scores** (each 0–20):

- **Behavioral Consistency** — Are transaction patterns regular and predictable?
- **Transaction Legitimacy** — Do transactions involve reputable contracts and protocols?
- **Wallet Age & History** — How long has the wallet been active?
- **Counterparty Quality** — Who has this wallet transacted with?
- **Volume Stability** — Is transaction volume stable or erratic?

---

## Step 4 — Query score history

Retrieve the full scoring history for any wallet (newest first):

```bash
curl https://kaelai.io/api/v1/score/0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/history \
  -H "Authorization: Bearer kael_live_YOUR_KEY"
```

Optional query parameter: `?limit=20` (default 50, max 200).

---

## Step 5 — Check score trend

See whether a wallet's trust score is improving, stable, or declining:

```bash
curl "https://kaelai.io/api/v1/score/0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/trend?window=5" \
  -H "Authorization: Bearer kael_live_YOUR_KEY"
```

The `window` parameter controls how many recent scores to analyse (default 5, max 20).

Response includes:
- `direction` — `improving`, `stable`, or `declining`
- `delta` — score change over the window
- `scores` — the individual scores analysed

---

## Next steps

- Full API reference: [kaelai.io/docs](https://kaelai.io/docs)
- Questions: [hello@kaelai.io](mailto:hello@kaelai.io)
