# Handoff — read this first in a fresh session

This SOP package (SKILL.md + references/) was uploaded by the user (Sam Whipple,
samgwhipple991@gmail.com) on 2026-08-21 and adopted for the Robinhood **Agentic**
account. It was originally written by someone else ("Ryan Doser") for a different
account — ignore all account numbers, dollar amounts, and "Ryan" references inside
SKILL.md/RESUME.md/trade-log.md itself; the real current state is below.

## Real current state (2026-08-21, established this session)

- **Account:** Robinhood Agentic cash account, account_number `746043736`
  (displays as ••••3736), connector name `Robinhood`. Confirmed via `get_accounts`
  as the only account with `agentic_allowed: true`. The other account on this
  login (••••8191, margin, `agentic_allowed: false`) must NEVER be traded —
  it isn't even reachable by this agent's tools.
- **Started:** $100.00 cash, 2026-08-21.
- **Standing authorization:** Sam explicitly granted autonomy in-conversation on
  2026-08-21 — execute verified trades WITHOUT per-trade approval. Every Hard
  Rule in SKILL.md stays in force, as do the SOP's own "stop and ask no matter
  what" triggers (portfolio down >20% from $100 i.e. below $80, any hard-rule
  breach, ambiguous data, a brand-new sector, anything that doesn't clearly fit).
  On any of those: stop, don't place the trade, tell Sam what needs input.
- **Positions opened 2026-08-21** (see trade-log.md for full reasoning): BRK.B
  ($20, politician cluster), ET ($20, insider cluster — company founder Kelcy
  Warren + a director), APTV ($20, insider cluster — CEO + 2 directors). ~$40
  cash remaining. Full detail, including everything that was screened out and
  why, is in trade-log.md under "2026-08-21 — First live run, new session".
- **Network access:** this environment's egress allowlist was widened
  mid-session to include SEC EDGAR (`www.sec.gov`, `efts.sec.gov` — send a
  descriptive `User-Agent` header on every request or you get a 403), Kalshi
  (`api.elections.kalshi.com`), Polymarket (`clob.polymarket.com`), FRED
  (`fred.stlouisfed.org`), and Cleveland Fed (`www.clevelandfed.org`, though
  its actual nowcast numbers are JS-rendered and weren't reachable even after
  allowlisting). `openinsider.com` was added but the site itself resets the
  connection (looks like bot/datacenter-IP protection, not a policy block) —
  don't rely on it; SEC EDGAR's own daily full-index files
  (`www.sec.gov/Archives/edgar/daily-index/...`) work as the direct discovery
  path instead, or delegate that pull to a subagent as SKILL.md recommends.
  `raw.githubusercontent.com` (for the Kadoa congress-trading feed) has always
  worked without needing the custom allowlist.
- **Two scheduled Routines exist** (re-pointed at this new session as part of
  this handoff — check `trig_...` IDs the setting-up message gave you, or ask
  Sam / look them up):
  1. Daily full scan-and-trade, weekdays ~9:40am ET (Paths A/B/C fresh each day,
     apply shared gate, place anything that clears, log it).
  2. Hourly stop-loss/take-profit check, weekdays ~10:30am-3:30pm ET (existing
     positions only, no new signal scanning — sells at -15%/+25% from cost,
     hard-stops the whole book if portfolio value drops below $80).
  Both push a notification (not just a log line) if something blocks the
  normal cadence — a blocked order, a dead data source, a stop-and-ask trigger,
  connector auth failure — but stay silent on routine no-trade days.
- **Known open risk:** it's untested whether Robinhood order placement (via
  `place_equity_order`) will actually succeed when a Routine fires unattended
  with no live user message in that turn — it was blocked once mid-conversation
  by the harness's own permission layer, then succeeded after Sam typed an
  explicit "go ahead". If a Routine's order gets blocked, don't retry-loop it —
  push-notify Sam and log it.
- **Why this new session exists:** the prior session's Robinhood connector
  became disconnected mid-conversation (`enabledInChat: false` in
  `ListConnectors`, even after Sam re-confirmed it was connected in claude.ai
  settings) and never recovered. This session should be verified working
  (`ListConnectors` shows `enabledInChat: true` and `mcp__Robinhood__*` tools
  are actually callable) before relying on it for anything.

Read SKILL.md next for the actual trading rules, then trade-log.md for full
history before making any new decision.
