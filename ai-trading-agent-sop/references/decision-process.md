# Decision process - full detail

Table of contents:
- Path A: politician BUY process
- Path B: insider BUY process
- Shared gate
- Candidate ranking (both paths)
- SELL process (expanded)
- Proposal format

Two parallel signal paths each produce candidate tickers; both feed the shared gate. Insider detail lives in insider-signal.md; politician performance detail in performance-scoring.md.

## Path A: politician BUY process

1. **Pull signals.** Latest House + Senate trades from FMP, filtered to `transaction type = purchase`, last ~45 days of *disclosure* dates.
2. **Group by ticker, find clusters (the gate).** Bucket every buy by ticker. A ticker is a valid candidate ONLY if **2+ different members bought it within a ~6-week window** (Hard Rule 12). Discard every single-member ticker - including large-bracket and famous-trader buys.
3. **Disqualification filter (Hard Rule 14).** For each surviving cluster, look up each member on the validated leaderboard (see performance-scoring.md). **Drop every WEAK, no-live-signal, retired/resigned, fully-divested, or EXCLUDE member.** Re-check: if fewer than 2 qualifying members remain, the cluster fails - discard. UNRATED-but-active members count as AVERAGE-with-caution, never as the sole basis for a buy. This step removes dead weight; it does not pick "stars."

## Path B: insider BUY process

(Full filter rationale + transaction codes: insider-signal.md.)

1. **Pull signals.** Recent SEC Form 4 filings (EDGAR daily Ownership index, or FMP insider endpoints), last ~10 trading days.
2. **Code filter (Hard Rule 16).** Keep ONLY transaction **code P** (open-market purchase). Drop sells (S), grants (A), exercises (M/F), gifts (G), and all Table II derivatives.
3. **10b5-1 filter (Hard Rule 17).** Drop pre-planned trades (mandatory checkbox); keep only discretionary buys.
4. **Cluster gate (Hard Rule 15).** Keep only tickers with **2+ distinct insiders** buying within ~10 trading days. Discard single-insider tickers.
5. **Size + role weighting.** Require meaningful spend (~$50k-$100k floor) and/or a real % stake increase (Column 5). Weight CEO/CFO + role-diverse clusters higher; still capture opportunistic director buys.

## Shared gate

Every candidate from Path A or Path B must then pass:

1. **Apply HARD RULES.** Drop crypto, options, sub-$5/$2B, leveraged, OTC.
2. **Sanity-check the stock.** NYSE/Nasdaq, price ≥$5, market cap ≥$2B, not within 2 trading days of earnings, not already up >15% since the source trade date.
3. **Size the position.** ~$20-25, ≤35% of portfolio, keep ≥5% cash buffer, respect 3-5 position target and sector caps.
4. **Write the proposal** (name which signal(s) fired) and route to the approval workflow.

If nothing clears either path, output **no trade**.

## Candidate ranking (both paths)

Rank all surviving candidates highest to lowest on:

1. **Dual-signal first.** A ticker backed by BOTH a politician cluster AND an insider cluster is the highest-conviction setup - rank it above any single-signal candidate.
2. **Insider clusters next.** The insider-buy edge is the stronger, better-documented signal (and far less lagged). Within insider candidates: more insiders > fewer; role-diverse (CEO + CFO + director) > same-role; larger aggregate spend breaks ties.
3. **Politician clusters next.** Within these: bipartisan first (both-party agreement is the hardest-to-fake tell), then more qualifying members, then a genuinely STRONG member present (realistically only Pelosi's equity book) as a mild plus, then size/recency. Performance is a disqualifier, not a star-picker.
4. **Recency** breaks remaining ties. Neither size nor fame ever promotes a single-member/single-insider trade (Rules 13, 15).

## SELL process (expanded)

Sell when ANY is true:

- **Take profit:** position up **≥25%** → sell the full position (fractional-share scaling isn't worth the complexity at $100).
- **Stop loss:** position down **≥15%** from cost basis → sell. No averaging down, no "it'll come back."
- **Politician signal reversal:** the same member (or cluster) that triggered a Path-A buy is now disclosed selling the same stock → follow them out. (Applies to politician signals only.)
- **Thesis broke:** the reason for owning it no longer holds (e.g. the cluster was misread).
- **Stale position:** held **>90 days** with no progress toward the profit target and no fresh supporting signal → free the cash.

**Insider SELLS are NOT a sell trigger.** Insider selling is noise (taxes, diversification, planned 10b5-1) and does not predict downside. Never exit because an insider sold.

Never sell purely on a scary headline or a red day. Sells follow these rules, not emotion.

## Proposal format

One short paragraph containing:
- **What:** ticker + dollar amount + action.
- **Signal type:** politician cluster, insider cluster, or both.
- **Why:** for a politician signal - which members, brackets, dates, and each member's performance bucket. For an insider signal - which insiders, their roles, transaction code (P), dates, and dollar size. For dual-signal - both.
- **Thesis:** one sentence.
- **Rule check:** confirm it clears the relevant cluster gate(s), the filters (disqualification for politicians; code-P + non-10b5-1 for insiders), and the hard rules.
- End with the explicit ask: **Approve, reject, or modify?**
