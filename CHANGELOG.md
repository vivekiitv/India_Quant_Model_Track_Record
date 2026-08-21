# CHANGELOG — India Quant Model Track Record

All corrections are **forward-only**: a sealed artifact is never modified or deleted; a material
revision is sealed as a sibling and noted here. Gaps (a session sealed late) are explained here.

## 2026-08-21 — genesis

- Chain launched. Public repo created; this and every subsequent commit SSH-signed.
- **Sealed spec v1.0** (frozen; any change is a versioned entry here): Indian top-1000 long-only,
  proprietary multi-factor alpha (`alpha_v2_neut`), absolute-mode mean-variance construction with
  per-name cap 5%, position floor 1%, portfolio vol cap 16%, one-sided turnover cap 30% per
  rebalance, cash at 6%/yr, tcost 30 bps round-trip, monthly rebalance solved at the month's last
  session and executed T+2. Model code at `india_quant_model` git `0c0ebde0133d0a8b96f1e5ca7a31861e79319b7e`.
- **Historical shards stamped** (`_historical/`, label `historical-stamped-2026-08-21`): alpha, ledger and
  optimizer per-year 2011–2026-08-20. These prove existence as of 2026-08-21 only — the span (through 2026-08-20) predates this
  chain and its returns were known when sealed. NOT an out-of-sample record.
- The historical book-of-record was materialized by a daily walk engine reconciled against the
  measurement backtest to machine epsilon (max per-cell divergence 0.0) before sealing.
- **Live paper walk begins**: Rs 10 crore flat cash at 2026-08-21; first forward session 2026-08-24.
- Wayback captures of the repo and profile at genesis: {WAYBACK_URLS}.
