---
tags: economics
---

extends [[trading-strategies]] - component #4

### what is position sizing?
- determining how much capital to allocate to a single trade or bet
- the bridge between *having an edge* and *making money*
- controls risk exposure and determines long-term survival

### why it matters
- a 50% loss requires a 100% gain to recover
- a 90% loss requires a 900% gain to recover
- even with a winning strategy, poor sizing leads to ruin
- proper sizing maximizes growth while controlling drawdown

### the kelly criterion
- formula for optimal bet sizing given known edge and odds
- developed by John Kelly at Bell Labs (1956) for signal noise, applied to gambling/trading

#### the formula
```
f* = (bp - q) / b

where:
f* = fraction of capital to bet
b  = odds received (profit/loss ratio)
p  = probability of winning
q  = probability of losing (1 - p)
```

#### example
- you have a trade with 60% win rate
- winners return 1.5x what losers lose (b = 1.5)
```
f* = (1.5 × 0.6 - 0.4) / 1.5
f* = (0.9 - 0.4) / 1.5
f* = 0.33 → bet 33% of capital
```

### fractional kelly
- full kelly is mathematically optimal but *emotionally brutal*
- drawdowns can exceed 50% even with edge
- most practitioners use half-kelly or quarter-kelly
	- half-kelly = 75% of the growth, 50% of the volatility
	- reduces risk of ruin significantly

| kelly fraction | growth rate | max drawdown |
|----------------|-------------|--------------|
| full (1.0)     | 100%        | severe       |
| half (0.5)     | 75%         | moderate     |
| quarter (0.25) | 50%         | mild         |

### fixed fractional sizing
- simpler alternative: risk a fixed % of capital per trade
- common values: 1%, 2%, or 5% risk per trade
```
position size = (account × risk%) / (entry - stop loss)
```
- if account = $10,000, risk = 2%, stop = $5 away from entry:
```
position size = ($10,000 × 0.02) / $5 = 40 shares
```

### volatility-adjusted sizing (ATR method)
- uses [[moving-averages]] concept applied to true range
- normalizes position size across different volatility regimes
```
position size = (account × risk%) / (ATR × multiplier)
```
- higher volatility → smaller position
- lower volatility → larger position

### risk of ruin
- probability of losing enough capital to stop trading
- depends on:
	- win rate
	- reward/risk ratio
	- percentage risked per trade
- rule of thumb: if risking 2% per trade with 50% win rate and 1:1 R/R, risk of ruin is ~13%
- reducing to 1% drops risk of ruin to ~2%

### portfolio heat
- total risk across all open positions
- correlated positions compound risk
- general guidelines:
	- max 6% total portfolio risk at any time
	- max 2-3 correlated positions
	- reduce size when correlation spikes

### common mistakes
- sizing based on conviction rather than math
- ignoring correlation between positions
- increasing size after losses (martingale)
- not adjusting for volatility changes
- using full kelly (overconfidence in edge estimate)

### application to prediction markets
- kelly is *native* to betting markets like polymarket
- market odds give you implied probability
- your edge = your probability estimate - market probability
- size bets using kelly based on perceived edge

### key takeaways
1. never risk more than you can calculate
2. survival > optimization
3. half-kelly is the practitioner's standard
4. volatility changes → position size changes
5. correlated bets are secretly one big bet
