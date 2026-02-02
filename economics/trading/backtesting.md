---
tags: economics
---

validates [[trading-strategies]] before risking capital in [[automated-trading]]

### what is backtesting?
- testing a trading strategy on historical data
- simulates what *would have* happened if you traded that strategy in the past
- the scientific method applied to trading
- goal: determine if a strategy has edge before deploying real money

### why backtest?
- **validate edge** - does this strategy actually make money?
- **quantify risk** - what's the worst drawdown? how often do you lose?
- **optimize parameters** - what settings work best?
- **build confidence** - trust the system when live trading gets hard
- **kill bad ideas fast** - most strategies fail backtesting (this is good)

### the backtesting process

```
┌─────────────────┐
│  define rules   │ ← entry, exit, sizing
└────────┬────────┘
         ↓
┌─────────────────┐
│  get history    │ ← clean historical data
└────────┬────────┘
         ↓
┌─────────────────┐
│   simulate      │ ← walk through data bar by bar
└────────┬────────┘
         ↓
┌─────────────────┐
│   analyze       │ ← metrics, equity curve, drawdowns
└────────┬────────┘
         ↓
┌─────────────────┐
│   validate      │ ← out-of-sample, walk-forward
└─────────────────┘
```

### key metrics to evaluate

#### return metrics
- **total return** - overall profit/loss percentage
- **CAGR** - compound annual growth rate
- **average trade return** - mean profit per trade

#### risk metrics
- **max drawdown** - largest peak-to-trough decline
- **sharpe ratio** - return per unit of volatility (>1 is decent, >2 is good)
- **sortino ratio** - like sharpe but only penalizes downside volatility
- **calmar ratio** - CAGR / max drawdown

#### trade metrics
- **win rate** - percentage of winning trades
- **profit factor** - gross profit / gross loss (>1.5 is good)
- **average win / average loss** - reward to risk realized
- **number of trades** - statistical significance requires enough trades

### the overfitting trap
- biggest danger in backtesting
- strategy works perfectly on historical data, fails live
- caused by too many parameters tuned to past data
- the more you optimize, the more you overfit

#### signs of overfitting
- amazing backtest results (too good to be true)
- strategy has many parameters
- works only on specific time periods
- fails on out-of-sample data
- complex rules with no logical basis

#### how to avoid overfitting
- keep strategies simple (fewer parameters)
- require logical reasoning for every rule
- test on out-of-sample data
- use walk-forward optimization
- be suspicious of perfect results

### out-of-sample testing
- split data into two periods
- **in-sample** - develop and tune strategy here
- **out-of-sample** - test final strategy here (never peek)
```
[---- in-sample (70%) ----][-- out-of-sample (30%) --]
      develop here              validate here
```
- if it fails out-of-sample, the edge isn't real

### walk-forward optimization
- more robust than simple out-of-sample
- rolling window approach
```
period 1: [train----][test]
period 2:    [train----][test]
period 3:       [train----][test]
```
- reoptimize parameters on each training window
- test on subsequent window
- concatenate test results for realistic performance

### accounting for reality

#### slippage
- difference between expected price and fill price
- always assume some slippage (0.1-0.5% per trade)
```python
fill_price = signal_price * (1 + slippage)  # for buys
fill_price = signal_price * (1 - slippage)  # for sells
```

#### fees and commissions
- subtract from every trade
- can destroy marginally profitable strategies
- know your broker's fee structure

#### liquidity constraints
- can you actually get filled at that price?
- large orders move the market
- filter out low-volume bars or assets

#### look-ahead bias
- accidentally using future information
- common mistake: using today's close to decide today's trade
- always use data available *at the time* of the decision

#### survivorship bias
- historical data only includes assets that still exist
- excludes bankruptcies, delistings
- makes strategies look better than reality

### practical implementation

#### using vectorbt (fast, pythonic)
```python
import vectorbt as vbt
import pandas as pd

# get data
price = vbt.YFData.download('BTC-USD', start='2020-01-01').get('Close')

# define signals
fast_ma = vbt.MA.run(price, window=10)
slow_ma = vbt.MA.run(price, window=30)

entries = fast_ma.ma_crossed_above(slow_ma)
exits = fast_ma.ma_crossed_below(slow_ma)

# run backtest
portfolio = vbt.Portfolio.from_signals(
    price,
    entries,
    exits,
    init_cash=10000,
    fees=0.001  # 0.1% fees
)

# analyze
print(f"Total Return: {portfolio.total_return():.2%}")
print(f"Sharpe Ratio: {portfolio.sharpe_ratio():.2f}")
print(f"Max Drawdown: {portfolio.max_drawdown():.2%}")
```

#### using backtrader (full-featured)
```python
import backtrader as bt

class MyStrategy(bt.Strategy):
    params = (('fast', 10), ('slow', 30))

    def __init__(self):
        self.fast_ma = bt.ind.SMA(period=self.p.fast)
        self.slow_ma = bt.ind.SMA(period=self.p.slow)
        self.crossover = bt.ind.CrossOver(self.fast_ma, self.slow_ma)

    def next(self):
        if self.crossover > 0:
            self.buy()
        elif self.crossover < 0:
            self.sell()

cerebro = bt.Cerebro()
cerebro.addstrategy(MyStrategy)
cerebro.adddata(bt.feeds.YahooFinanceData(dataname='BTC-USD'))
cerebro.run()
cerebro.plot()
```

### data sources
- **Yahoo Finance** - free, good for stocks (yfinance library)
- **CCXT** - crypto historical data from exchanges
- **Polygon.io** - professional stock/crypto data
- **Binance** - free crypto OHLCV data
- **Alpha Vantage** - free tier available

### interpreting results

#### good signs
- positive returns out-of-sample
- sharpe ratio > 1
- profit factor > 1.5
- reasonable drawdowns you can stomach
- enough trades for statistical significance (30+)
- simple logic that makes sense

#### red flags
- only works on specific time period
- sharpe ratio > 3 (probably overfit)
- too few trades (<30)
- requires precise parameter values
- no logical explanation for why it works
- max drawdown exceeds your risk tolerance

### from backtest to live

1. **pass out-of-sample test** - edge survives unseen data
2. **paper trade** - run live with fake money
3. **compare results** - paper should match backtest expectations
4. **start small** - deploy with minimal capital
5. **monitor and log** - track live vs expected performance
6. **scale gradually** - increase size as confidence grows

### connection to position sizing
- backtest gives you win rate and win/loss ratio
- feed these into [[position-sizing]] kelly formula
- backtest different position sizing approaches
- optimize for growth vs drawdown tradeoff

### common mistakes
- optimizing too many parameters
- not accounting for fees and slippage
- peeking at out-of-sample data
- using unrealistic fill assumptions
- ignoring drawdown (only looking at returns)
- insufficient sample size
- data snooping (testing many strategies, keeping winners)

### key takeaways
1. never trade a strategy you haven't backtested
2. out-of-sample performance is the only truth
3. simple strategies that make sense > complex optimized ones
4. account for slippage, fees, and liquidity
5. if it looks too good, it's overfit
6. backtesting is the bridge between idea and deployment
