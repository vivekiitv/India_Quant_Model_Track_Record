# India Quant Model — Public Track Record

A cryptographically verifiable, third-party-timestamped record of the daily **alpha signal** and
**book-of-record** of an Indian **long-only** top-1000 equity strategy operated by
**Vivek ([`@vivekiitv`](https://github.com/vivekiitv))**. Its purpose is to let a track record be
**proven** — not merely asserted — while keeping contents confidential until selectively disclosed.

This is the **second** chain under this account, alongside the US strategy's
[`US_Quant_Model_Track_Record`](https://github.com/vivekiitv/US_Quant_Model_Track_Record) — a
separate strategy on a separate market, run by the same operator under the same doctrine. Each
chain's exclusivity claim covers its own market.

Launched **2026-08-21** (`L`). Everything under `_historical/` is a one-time pre-commitment as of `L`; the
daily forward chain runs from the next session onward, each ledger entry committed after its
session's close and each **optimizer target committed before the session at which it trades**.

## Performance (backtest)

Backtest **2011–2026-08-20**, net of modelled transaction costs (30 bps round-trip); long-only; all
figures on NAV. A blind tear sheet will follow; every figure derives from the sealed book-of-record
in this repository.

| Ann. return (net CAGR) | Ann. vol | Net Sharpe | Max DD | Bench CAGR (cap-wt top-1000) | Active IR | Turnover (mo, 1-side) | Median names |
|---|---|---|---|---|---|---|---|
| 38.8% | 15.7% | 2.17 | −35.7% | 12.1% | 2.03 | 31.4% | 31 |

Long-only Indian top-1000 (NSE cash equities), multi-factor proprietary alpha optimized against a
Barra-style factor risk model, monthly rebalance solved at each month's last session and executed
two sessions later, ~30–40 positions, uninvested balance at a 6% cash rate.

## How to verify (3 steps)

Requires Python with `pip install cryptography opentimestamps-client`.

1. **Clone** this repository.
2. Obtain a **disclosure keyfile** (JSON), provided directly for the window under review.
3. Run:
   ```
   python verify.py --repo . --keys <keyfile.json> --ots
   ```
   For each covered artifact it decrypts the ciphertext, re-computes the SHA-256, and matches it
   against the `*.sha256` committed on that date; `--ots` also checks the OpenTimestamps Bitcoin
   proof. It prints `PASS`/`FAIL` per artifact.

## What proves what

| claim | mechanism |
|---|---|
| **What** existed | SHA-256 of the plaintext, committed publicly (`*.sha256`) — you re-hash the revealed file yourself |
| **When** it existed | GitHub's public push-event record ([GH Archive](https://www.gharchive.org/), server-recorded, not settable) + OpenTimestamps → Bitcoin. Commits are SSH-signed ("Verified") for authorship |
| **Confidential** | AES-256-GCM; only ciphertext + hashes are public; per-file keys → any subset selectively disclosable |
| **One unbroken chain** | one entry per artifact per trading day; no deletions, no history rewrites; gaps explained in `CHANGELOG.md` |

## Contents

```
alpha/YYYYMMDD/                                        daily alpha signal (the NAV-independent prediction)
alpha/_historical/<year>/                              2011..L, one-time, historical-stamped-L
backtest/top1000_long_only/_historical/ledger/<year>/     2011..L book-of-record, one-time
backtest/top1000_long_only/_historical/optimizer/<year>/  2011..L targets, one-time
live/top1000_long_only/ledger/YYYYMMDD/                daily LIVE paper book (Rs 10 crore from flat at L)
live/top1000_long_only/optimizer_output/YYYYMMDD/      targets, keyed by TRADE date, sealed before it
verify.py                                              the reviewer tool above
```

Each artifact folder holds `<name>.enc` (ciphertext), `<name>.sha256` (the commitment), and
`<name>.sha256.ots` (the OpenTimestamps proof). Files are frozen at commit time: CSV, UTF-8, sorted
by `sec_id`, dual-keyed by `sec_id` **and** point-in-time-resolved NSE `ticker`, all floating
values at 4 decimals.

**Historical vs live.** `_historical/` shards are **stamped-at-launch**: they prove existence *as
of* `L`, not before the (already-known) returns — a frozen pre-commitment, not a before-the-outcome
proof. Only the daily `YYYYMMDD/` folders committed forward are the strong record; within them the
**optimizer targets** carry the strongest property (sealed before the session at which they trade).
The `backtest/` tree is historical-only and is retired forward: the single forward walk is `live/`.

## Long-only conventions

- Weights satisfy `sum(w) <= 1`; the uninvested balance is cash earning **6%/yr** (`INRCASH` row,
  ledger `sec_id = -1`).
- NAV basis **Rs 10 crore**, flat cash at `L`. The optimizer is NAV-independent (weights only), so
  the NAV is a display basis, not a strategy input.
- Transaction cost **15 bps per side** (30 bps round-trip) on traded weight.
- Rebalance: monthly — solved at the month's **last session** `T`, executed at `T+2` sessions.
- Position floor 1% (hold >= 1% of NAV or hold nothing); per-name cap 5%; portfolio vol cap 16%.
- Returns quoted raw (not excess); Sharpe daily-computed, net of costs.
- The benchmark referenced in summaries is the cap-weighted top-1000 of the same universe with
  weight and membership lagged one session; it is reconstructable from public data and is not
  separately sealed.

## Exclusivity statement

> This repository is the **sole** verification chain for the **sole** Indian equity strategy
> operated by Vivek ([`github.com/vivekiitv`](https://github.com/vivekiitv)). **One entry per
> trading day. No resets. No deletions.** A terminated strategy, if ever, will be sealed here —
> not removed. The US strategy's separate chain is linked above; no other chains exist.
>
> **Canonical anchor — repo ID `1341563504 (node R_kgDOT_aicA)`** (immutable, survives renames; a delete+recreate gets
> a different ID). Identify this chain by its **ID**, not its name, and verify its public history
> via **GH Archive** keyed on the repo ID.

## Uniqueness — honest limitations

Uniqueness is **not** cryptographically provable (that would require proving a negative). It is
made expensive and discoverable: the public-witness standard (GH Archive), the un-fabricable
12-year account history, and the cross-linked two-chain statement above. A fully separate identity
cannot be cryptographically excluded — deterred, not disproven.

## Contact

Reach out via GitHub — [`@vivekiitv`](https://github.com/vivekiitv) — or open an issue on this
repository for disclosure requests.
