# Stock F&O Options Trading Strategy

## Overview

This repository/document contains a rules-based intraday F&O options trading strategy focused on:

- Early-session momentum
- Strict entry confirmation
- Controlled risk
- Mechanical exits
- Indicator-based confirmation
- Trade journaling
- Minimum 100-trade validation before changing the strategy

The strategy is designed to reduce discretionary decisions and prevent emotional trading.

---

## Core Trading Window

### Entry

- **Entry window:** 09:16 AM–09:30 AM
- **No entry after 09:30 AM**, even if the setup becomes attractive later.

### Exit / Position Management

- **11:15–11:30 AM:** Mandatory review of every open position.
- If the position is **in profit:** trail the stop-loss and allow the move to continue.
- If the position is **not in profit:** follow the strict exit/stop-loss rule and exit.
- **No new trade after 11:30 AM.**

---

## 1. Daily Stock Selection

Before market open:

1. Review NSE Top Gainers & Losers.
2. Shortlist liquid F&O stocks showing strong relative momentum.
3. Prefer contracts with:
   - Good option liquidity
   - Tight bid/ask spreads
   - Meaningful option volume/OI
4. Avoid:
   - Illiquid contracts
   - Very wide spreads
   - Abnormal price spikes
   - Unclear event-driven setups

---

## 2. Bullish CE Setup

All mandatory conditions must pass.

### Opening Conditions

- The 09:15–09:20 candle must have **Open = Low**, or effectively equal within a very small tick/price tolerance.
- Today's Open must be **greater than Previous Close**.

### Indicator Confirmation

The following indicators must support the bullish direction:

1. **EMA 200 High**
2. **EMA 200 Low**
3. **SuperTrend (5, 1)**
4. **Squeeze Momentum Indicator (34, 2, 20, 1.5)**

Do not enter when the indicators materially conflict with the bullish price-action setup.

---

## 3. Bearish PE Setup

All mandatory conditions must pass.

### Opening Conditions

- The 09:15–09:20 candle must have **Open = High**, or effectively equal within a very small tick/price tolerance.
- Today's Open must be **less than Previous Close**.

### Indicator Confirmation

The following indicators must support the bearish direction:

1. **EMA 200 High**
2. **EMA 200 Low**
3. **SuperTrend (5, 1)**
4. **Squeeze Momentum Indicator (34, 2, 20, 1.5)**

Do not enter when the indicators materially conflict with the bearish price-action setup.

---

## 4. Indicator Rules

### EMA 200 High

Use the 200-period EMA calculated using High prices as a directional confirmation/reference zone.

### EMA 200 Low

Use the 200-period EMA calculated using Low prices as a directional confirmation/reference zone.

### SuperTrend (5, 1)

The SuperTrend direction must agree with the intended trade:

- Bullish/uptrend → supports CE
- Bearish/downtrend → supports PE

### Squeeze Momentum (34, 2, 20, 1.5)

Use the configured Squeeze Momentum indicator as a momentum confirmation filter.

- Bullish/strengthening momentum → supports CE
- Bearish/weakening momentum → supports PE
- Conflicting momentum → avoid the trade

---

## 5. Risk Management

Current rules:

| Rule | Limit |
|---|---:|
| Maximum lots | 1–2 |
| Maximum premium deployment | ₹20,000 |
| Maximum planned loss | ₹1,500 |
| Minimum planned profit | ₹3,000+ |
| Minimum planned R:R | 1:2 |

The actual stop-loss must be calculated from the entry price and quantity before placing the trade.

### Never

- Average a losing option position.
- Increase quantity after entry to recover losses.
- Widen the stop-loss.
- Take a trade with less than 1:2 planned risk/reward.
- Force a trade when a mandatory condition fails.

---

## 6. Expiry and Strike Selection

- Select an OTM option.
- If more than 3 trading days remain to expiry, use the current-month expiry.
- If 3 or fewer trading days remain, use the next-month expiry.
- Use one fixed and predefined strike-selection methodology.
- Do not change strike-selection logic from trade to trade based on emotion or recent results.

---

## 7. Final Entry Checklist

Before entering, confirm:

- [ ] F&O-eligible and liquid underlying
- [ ] Strong momentum / relevant Gainer or Loser shortlist
- [ ] Bullish: 09:15–09:20 Open = Low OR bearish: Open = High
- [ ] Bullish: Today Open > Previous Close OR bearish: Today Open < Previous Close
- [ ] EMA 200 High confirms direction
- [ ] EMA 200 Low confirms direction
- [ ] SuperTrend (5,1) confirms direction
- [ ] Squeeze Momentum (34,2,20,1.5) confirms momentum
- [ ] Entry time is 09:16–09:30
- [ ] Correct OTM strike selected
- [ ] Correct expiry selected
- [ ] Premium deployment ≤ ₹20,000
- [ ] Position ≤ 1–2 lots
- [ ] Maximum planned loss ≤ ₹1,500
- [ ] Target ≥ ₹3,000+
- [ ] Planned R:R ≥ 1:2
- [ ] No mandatory condition has failed
- [ ] Trade is logged

**If any mandatory condition fails → NO TRADE.**

---

## 8. Time-Based Exit Discipline

### 11:15–11:30 AM Review

Every open position must be reviewed.

### Scenario A — Position in Profit

- Do not automatically exit.
- Trail the stop-loss.
- Protect accumulated profit.
- Allow the existing momentum to continue if the setup remains valid.

### Scenario B — Position Not in Profit

- Follow the strict stop-loss/exit rule.
- Exit the trade.
- Do not convert the intraday trade into a discretionary overnight hold.

### 11:30 AM

- No new entries.
- The strategy is finished for new trade initiation for the day.

---

## 9. 100-Trade Rule

The strategy must be followed **strictly for at least 100 trades**.

During the first 100 trades:

- Do not change indicator parameters.
- Do not change the entry window.
- Do not change the risk model because of a short losing streak.
- Do not change exit rules emotionally.
- Do not optimize the strategy after every few trades.

The purpose of the first 100 trades is to create a meaningful sample of results.

After 100 trades, evaluate the complete dataset before considering any modification.

---

## 10. Trade Journal

Every trade must be logged.

### Minimum fields

- Trade number
- Date
- Stock
- CE/PE
- Entry time
- Entry price
- Exit time
- Exit price
- Quantity/lots
- Stop-loss
- Target
- EMA 200 High status
- EMA 200 Low status
- SuperTrend (5,1) status
- Squeeze Momentum (34,2,20,1.5) status
- Opening candle condition
- Gap condition
- Exit reason
- Gross P&L
- Brokerage/charges
- Net P&L
- R-multiple
- Whether all rules were followed

### Important

A profitable trade that violated the strategy is still a **rule violation**.

Do not classify a rule-breaking trade as a valid strategy success simply because it made money.

---

## 11. Performance Review

After every 25 trades, review the data without changing the strategy.

Track:

- Win rate
- Average winning trade
- Average losing trade
- Total gross P&L
- Total net P&L
- Maximum losing streak
- Average R-multiple
- Rule violations

### At 100 Trades

Perform a complete strategy review.

Only after this review should parameter changes be considered.

---

## 12. Daily Trading Flow

### 09:00–09:15

Review the market and shortlist liquid F&O stocks.

### 09:15–09:20

Observe the first 5-minute candle.

### 09:20–09:30

Validate:

- Opening structure
- Gap direction
- EMA 200 High
- EMA 200 Low
- SuperTrend
- Squeeze Momentum
- Option liquidity
- Strike
- Expiry
- Risk
- Target
- R:R

### 09:16–09:30

Enter only when **every mandatory condition passes**.

### 11:15–11:30

Review open positions:

- Profit → trail SL
- Not in profit → strict exit

### After 11:30

No new trade.

---

## 13. Non-Negotiable Rules

1. **No entry after 09:30 AM.**
2. **No new trade after 11:30 AM.**
3. **No averaging losing positions.**
4. **No widening stop-loss.**
5. **No revenge trading.**
6. **No forced trades.**
7. **No discretionary parameter changes during the 100-trade validation period.**
8. **Every trade must be logged.**
9. **Every mandatory indicator must confirm the direction.**
10. **Follow the complete strategy for at least 100 trades before judging or modifying it.**

---

## 14. Repository / Document

The main strategy document is:

`Stock_FNO_Options_Trading_Rules_Updated.docx`

This README provides the quick-reference version of the same rules.

---

## Important Disclaimer

This is a rules-based trading framework and **not a guarantee of profitability**.

Options can move rapidly because of the underlying price, implied volatility, bid/ask spread, time decay and other factors.

Before committing real capital, backtest and/or paper-trade the complete rule set and include:

- Slippage
- Brokerage
- Taxes and exchange charges
- Option liquidity
- Bid/ask spread
- Realistic execution prices

The objective of the 100-trade requirement is disciplined validation, not a promise that the strategy will be profitable.
