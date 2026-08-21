# AI Trading Agent — RESUME (for a fresh chat)

Last updated: 2026-06-10 ~2:40 PM ET. Copy the prompt at the bottom into a new chat to continue the loop.

## Current state (snapshot)
- **Account:** Robinhood Agentic CASH account ••••8890 (`995608890`). NEVER trade the Individual margin account ••••5088 (`463795088`) — read-only, `agentic_allowed:false`.
- **Authorization:** 2026-06-09 autonomy override — execute verified trades WITHOUT per-trade approval, but hard rules + verification NOT waived. NO "maximize money" mandate; disciplined cluster-following only.
- **Portfolio:** ~$200 (started $200). 4 positions filled, ~$108 cash buffer.

## Live positions (entry → synthetic stop / take-profit)
All fractional → Robinhood rejects resting stop orders, so stops are SYNTHETIC (the loop enforces them each tick by selling at market if hit).

| Ticker | Shares | Cost | Stop | Take-profit | Signal |
|---|---|---|---|---|---|
| RYAN | 0.682695 | $33.69 | **$33.69** (breakeven, post-6/8 Goldman downgrade) | n/a | 3 insiders |
| NCLH | 1.249327 | $18.41 | $15.65 (−15%) | $23.01 (+25%) | 7 insiders |
| ADC | 0.304487 | $75.54 | $64.21 (−15%) | $94.42 (+25%) | 4 insiders |
| RLI | 0.424682 | $54.16 | $46.03 (−15%) | $67.70 (+25%) | 4 insiders |

## Standing config
- **Social layer (authorized 6/10):** pre-buy freshness check + live-position news-watch + social-led lead discovery. Social can DISQUALIFY or trigger an exit, NEVER originate a buy. Every entry still needs a verified primary-source cluster.
- **RYAN note:** 6/8 Goldman downgrade-to-Neutral already known → decided HOLD w/ breakeven stop. Only a HARDER new catalyst (real probe/guidance cut/exec exit) escalates to an earlier exit.
- **Drones/Defense watchlist** 🛩️ (id 564c2a43-a8b6-4b9f-93bc-a4f5120034a5): DRNZ, ONDS, AVAV, UMAC, RCAT, KTOS, DRS, TDG, BWXT, PLTR, RTX, LMT, NOC, GD, LHX, AXON. Folded into periodic scans.
- **Warm watch (a 2nd buyer makes a cluster):** DRS (lone director Jeffery, 5/19); Rep. April McClain Delaney solo-loading TDG + BWXT. If a 2nd insider/member joins → EDGAR-verify + social-check + flag, ask before a 5th position.
- **Loop cadence:** ~10 min. Stop-and-ask if portfolio down >20% ($160). Periodic fresh signal scan ~every 2.5h. Post-notify on any fill/trigger/new cluster; silent on no-op ticks except the log.

## Hard limits (never waived)
Long US equities/ETFs only; no options/crypto/leverage/penny/<$5/<$2B/OTC; ≤35% per position; ≥5% cash; no chase >15% since source buy; no earnings within 2 trading days; EDGAR code-P + non-10b5-1 + 2+ insiders required for every insider buy. Loop runs ONLY while a session is live — no overnight/unattended monitoring.

---

## COPY THIS INTO A FRESH CHAT:

```
Resume the AI trading agent intraday loop. FIRST read these for full state:
- ai-trading-agent-sop/RESUME.md (current positions, stops, config — start here)
- ai-trading-agent-sop/SKILL.md (the SOP + hard rules)
- ai-trading-agent-sop/trade-log.md (full history)

Trade ONLY the Robinhood Agentic cash account 995608890 (••••8890). NEVER touch the
Individual margin account 463795088. Autonomy override is active (execute verified trades
without per-trade approval; hard rules + verification NOT waived; no "maximize money").

Then run one loop tick now to confirm clean resume: get_portfolio + get_equity_positions
+ get_equity_quotes on RYAN/NCLH/ADC/RLI, confirm cost-basis + synthetic stops match
RESUME.md, enforce the synthetic stops (RYAN $33.69 / NCLH $15.65 / ADC $64.21 / RLI $46.03)
and +25% take-profits, run the social news-watch, and re-arm the ~10-min ScheduleWakeup loop.
If the market is closed, give the end-of-day summary instead and resume at the next open.
Log every tick to trade-log.md. Post-notify on any fill/trigger/new cluster.
```
