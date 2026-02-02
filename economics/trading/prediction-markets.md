---
tags: economics
---

applies [[position-sizing]] and kelly criterion to probabilistic events

### what are prediction markets?
- markets where you trade contracts on the outcome of real-world events
- prices reflect the crowd's probability estimate
- if you buy "yes" at $0.40, market implies 40% chance
- if event happens, contract pays $1. if not, pays $0.

### why they matter
- most efficient information aggregation mechanism known
- outperform polls, experts, and models in many domains
- reveal what people *actually believe* when money is on the line
- less efficient than stock markets → more edge available

### major platforms

| platform | type | settlement | edge |
|----------|------|------------|------|
| Polymarket | crypto (Polygon) | USDC | largest liquidity, political/crypto events |
| Kalshi | regulated US | USD | CFTC regulated, economic events |
| Manifold | play money | mana | practice, niche markets, no risk |
| PredictIt | regulated US | USD | political, 850 share limits |

### market mechanics

#### order book markets (Polymarket, Kalshi)
- bid/ask spread like stocks
- limit orders and market orders
- liquidity varies by market popularity
- slippage on large orders

#### AMM markets (some DeFi)
- automated market maker sets prices
- price impact based on pool size
- always liquidity but worse pricing on size

### reading the odds
- price = implied probability
- $0.65 yes = market thinks 65% chance
- your edge = your probability - market probability
```
if you think 75% and market says 65%:
edge = 0.75 - 0.65 = 0.10 (10% edge)
```

### applying kelly to prediction markets
- from [[position-sizing]], kelly formula adapts directly
- for binary markets (yes/no):
```
f* = (p - market_price) / (1 - market_price)

where:
p = your probability estimate
market_price = current yes price
```
- example: you estimate 75%, market at 65%
```
f* = (0.75 - 0.65) / (1 - 0.65)
f* = 0.10 / 0.35
f* = 0.286 → bet 28.6% of bankroll
```
- use half-kelly in practice (14.3%)

### finding edge

#### where edge comes from
- better domain expertise than the crowd
- faster information processing (news, data)
- understanding market biases
- arbitrage across platforms

#### common biases to exploit
- **favorite-longshot bias** - people overpay for longshots (cheap yes contracts)
- **recency bias** - overweight recent events
- **narrative bias** - compelling stories get overpriced
- **illiquidity premium** - less popular markets are less efficient

### information sources
- primary sources beat commentary
- look for leading indicators others miss
- specialized knowledge compounds (bet on what you know)
- on-chain data for crypto markets

### arbitrage opportunities
- same event priced differently across platforms
- yes + no on different platforms < $1 = free money
- rare but exists, especially during volatile news
- factor in fees and settlement risk

### risk factors
- **resolution risk** - ambiguous outcomes, disputes
- **counterparty risk** - platform solvency (less on crypto)
- **liquidity risk** - can't exit large positions
- **regulatory risk** - legal status varies by jurisdiction
- **timing risk** - opportunity cost of locked capital

### practical workflow
1. find market where you have domain knowledge
2. form independent probability estimate *before* looking at price
3. compare your estimate to market price
4. calculate edge and kelly size
5. scale down to half-kelly or less
6. track all bets for calibration review

### calibration
- are you actually good at this?
- track: prediction, confidence, outcome
- if your 70% calls hit 70% of the time, you're calibrated
- most people are overconfident
- calibration improves with feedback loops

### connection to trading
- same skills transfer: edge identification, sizing, discipline
- prediction markets = pure probability trading
- no technical analysis, no price action
- fundamentals and information only

### tools to build
- odds tracker across platforms
- kelly calculator with your estimates
- calibration tracker (log predictions, review accuracy)
- news sentiment scraper for fast information

### key takeaways
1. price = probability, your edge = your estimate minus price
2. use kelly sizing (half-kelly in practice)
3. bet on what you know, not what's popular
4. track everything - calibration is the meta-skill
5. biases exist and are exploitable
