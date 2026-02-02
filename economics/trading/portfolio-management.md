---
tags: economics
---

extends [[position-sizing]] from single trades to managing multiple positions together

### why portfolio thinking matters
- individual position sizing isn't enough
- correlated positions amplify risk
- "diversified" portfolios often aren't
- a portfolio of good trades can still blow up
- professionals think in portfolios, not trades

### the correlation problem
- correlation measures how assets move together
- ranges from -1 (opposite) to +1 (identical)
```
+1.0 = perfect positive (move together)
 0.0 = uncorrelated (independent)
-1.0 = perfect negative (move opposite)
```
- most assets are positively correlated
- correlation spikes during crashes (when you need diversification most)

### why correlation kills
- you think you have 5 independent bets
- but they're all correlated at 0.7
- one bad event hits all 5 simultaneously
- your "diversified" portfolio acts like one big bet
```
5 positions at 2% risk each = 10% portfolio risk (if uncorrelated)
5 positions at 2% risk, 0.7 correlated = effectively ~7% on one bet
```

### measuring correlation

#### correlation coefficient
```python
import pandas as pd

# calculate correlation matrix
returns = prices.pct_change()
correlation_matrix = returns.corr()

# example output:
#          BTC    ETH    SOL
# BTC     1.00   0.85   0.78
# ETH     0.85   1.00   0.82
# SOL     0.78   0.82   1.00
```

#### rolling correlation
- correlation changes over time
- use rolling window (30-90 days)
```python
rolling_corr = returns['BTC'].rolling(30).corr(returns['ETH'])
```
- monitor for regime changes

### portfolio heat revisited
- from [[position-sizing]]: total risk across positions
- now accounting for correlation
```
naive heat = sum of individual position risks
adjusted heat = accounts for correlation between positions
```
- rule of thumb: if positions are correlated >0.5, treat them as partial duplicates

### diversification math
- combining uncorrelated assets reduces portfolio volatility
- doesn't reduce expected return
```
portfolio_volatility = sqrt(w1²σ1² + w2²σ2² + 2*w1*w2*σ1*σ2*ρ)

where:
w = weight
σ = volatility
ρ = correlation
```
- when ρ = 0 (uncorrelated), cross-term disappears
- when ρ = 1, no diversification benefit

### practical diversification

#### across asset classes
- stocks, bonds, crypto, commodities
- different drivers, lower correlation
- crypto is highly correlated internally but less with traditional assets

#### across sectors/categories
- tech stocks correlate with each other
- BTC and ETH correlate heavily
- diversify across sectors, not just tickers

#### across strategies
- momentum and mean reversion often uncorrelated
- different timeframes reduce correlation
- long and short positions can hedge

#### across time
- not all positions entered at once
- staggers reduce timing risk

### correlation in crypto
- everything correlates to BTC
- typical correlations:
```
BTC-ETH: 0.80-0.90
BTC-altcoins: 0.60-0.85
altcoin-altcoin: 0.50-0.80
```
- during crashes, correlations spike to ~0.95
- "diversified" crypto portfolio is really a leveraged BTC bet
- true diversification requires non-crypto assets

### correlation in prediction markets
- related events correlate
- "Will X win election?" and "Will X's party win Senate?" are correlated
- multiple positions on same event = concentrated bet
- from [[prediction-markets]]: size total exposure to related events

### portfolio construction

#### equal weight
- simplest approach
- 1/N allocation to each asset
- surprisingly effective
```python
weights = {asset: 1/len(assets) for asset in assets}
```

#### risk parity
- weight by inverse volatility
- each position contributes equal risk
```python
volatilities = returns.std()
inverse_vol = 1 / volatilities
weights = inverse_vol / inverse_vol.sum()
```

#### mean-variance optimization
- maximize return for given risk (or minimize risk for given return)
- Markowitz efficient frontier
- sensitive to input estimates (garbage in, garbage out)
- use with caution

### position sizing in portfolio context
- from [[position-sizing]]: kelly sizes individual bets
- portfolio context adds constraints:
```
single position max: 10-20% of portfolio
correlated group max: 25-30% of portfolio
total portfolio heat: 20-40% max
```
- reduce sizes when correlation is high
- increase sizes when adding uncorrelated positions

### rebalancing
- positions drift from target weights
- winners grow, losers shrink
- rebalancing = selling winners, buying losers
- enforces "buy low, sell high" systematically

#### rebalancing approaches
- **calendar** - monthly, quarterly
- **threshold** - when drift exceeds 5-10%
- **hybrid** - check monthly, act on threshold

```python
def check_rebalance(current_weights, target_weights, threshold=0.05):
    rebalance_needed = {}
    for asset in current_weights:
        drift = abs(current_weights[asset] - target_weights[asset])
        if drift > threshold:
            rebalance_needed[asset] = target_weights[asset] - current_weights[asset]
    return rebalance_needed
```

### managing drawdowns
- drawdown = peak to trough decline
- recovery time matters as much as depth
```
10% drawdown → need 11% to recover
25% drawdown → need 33% to recover
50% drawdown → need 100% to recover
```
- portfolio construction controls max drawdown
- diversification smooths the equity curve

### beta and market exposure
- beta measures sensitivity to market moves
```
beta = 1.0 → moves with market
beta = 1.5 → 50% more volatile than market
beta = 0.5 → 50% less volatile than market
beta = 0.0 → uncorrelated with market
```
- portfolio beta = weighted average of position betas
- reduce beta in uncertain times

### hedging basics
- taking offsetting positions to reduce risk
- costs money (premium, spread, opportunity cost)
- types:
  - **direct hedge** - short the asset you're long
  - **proxy hedge** - short correlated asset
  - **options hedge** - buy puts for downside protection

### tracking your portfolio

#### key metrics
- **total return** - overall performance
- **sharpe ratio** - return per unit of risk
- **max drawdown** - worst peak-to-trough
- **correlation to benchmark** - are you actually diversified?
- **beta** - market sensitivity

#### portfolio dashboard
```python
def portfolio_metrics(returns):
    return {
        'total_return': (1 + returns).prod() - 1,
        'annualized_return': returns.mean() * 252,
        'volatility': returns.std() * np.sqrt(252),
        'sharpe': (returns.mean() * 252) / (returns.std() * np.sqrt(252)),
        'max_drawdown': (returns.cumsum() - returns.cumsum().cummax()).min()
    }
```

### common mistakes
- assuming different tickers = diversification
- ignoring correlation spikes in stress
- over-concentrating in "high conviction" bets
- not rebalancing (letting winners dominate)
- hedging too late (expensive during panic)
- optimizing on historical correlation (it changes)

### building your portfolio process

1. **define risk budget** - max drawdown you can tolerate
2. **select uncorrelated assets/strategies** - true diversification
3. **size positions** - kelly for edge, constrained by correlation
4. **monitor correlation** - watch for regime changes
5. **rebalance** - maintain target allocation
6. **review** - track metrics, adjust as needed

### connection to other notes
- [[position-sizing]] - single position → portfolio context
- [[expected-value]] - portfolio EV = sum of position EVs
- [[backtesting]] - test portfolio, not just individual strategies
- [[risk-metrics]] - portfolio-level sharpe, drawdown

### key takeaways
1. correlated positions are secretly one big position
2. diversification = uncorrelated returns, not just different tickers
3. correlation spikes when you need diversification most
4. portfolio heat > sum of individual risks when correlated
5. rebalancing enforces buy low, sell high
6. think in portfolio risk, not just position risk
7. crypto is NOT diversified - it's all one bet on BTC
