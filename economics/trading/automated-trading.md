---
tags: economics
---

turns [[trading-strategies]], [[position-sizing]], and [[prediction-markets]] into running systems

### what is automated trading?
- software that executes trades based on predefined rules
- removes emotion, adds speed, enables scale
- ranges from simple alerts to full autonomous systems
- your edge in code, running 24/7

### why automate?
- **speed** - react to signals in milliseconds
- **consistency** - no emotional deviation from strategy
- **scale** - monitor hundreds of instruments simultaneously
- **backtesting** - validate before risking capital
- **compounding** - runs while you sleep, build, or learn

### levels of automation

| level | description | complexity |
|-------|-------------|------------|
| alerts | notify you when conditions met | low |
| semi-auto | generates orders, you approve | medium |
| full auto | executes without intervention | high |
| adaptive | adjusts parameters based on conditions | very high |

start at alerts, graduate up as you trust your systems

### architecture of a trading bot

```
┌─────────────┐
│  data feed  │ ← prices, news, on-chain
└──────┬──────┘
       ↓
┌─────────────┐
│   signal    │ ← your strategy logic
│  generator  │
└──────┬──────┘
       ↓
┌─────────────┐
│    risk     │ ← position sizing, exposure limits
│   manager   │
└──────┬──────┘
       ↓
┌─────────────┐
│  execution  │ ← order placement, fills
│   engine    │
└──────┬──────┘
       ↓
┌─────────────┐
│   logging   │ ← track everything for review
└─────────────┘
```

### key APIs by market

#### stocks
- **Alpaca** - commission-free, great API, paper trading
- **Interactive Brokers** - professional grade, complex API
- **Tradier** - simple REST API, options support

#### crypto
- **CCXT** - unified API for 100+ exchanges
- **Binance API** - largest liquidity, good docs
- **Coinbase Advanced** - US regulated, solid API

#### prediction markets
- **Polymarket API** - REST + WebSocket, USDC settlement
- **Kalshi API** - regulated, economic events
- **Manifold API** - play money, good for testing

### core components

#### 1. data fetching
```python
# example: fetch price data with ccxt
import ccxt

exchange = ccxt.binance()
ohlcv = exchange.fetch_ohlcv('BTC/USDT', '1h', limit=100)
# returns: [[timestamp, open, high, low, close, volume], ...]
```
- historical data for backtesting
- real-time data for live signals
- order book data for execution

#### 2. signal generation
- encode your [[trading-strategies]] as functions
- input: market data
- output: signal (buy/sell/hold) + confidence
```python
def generate_signal(prices):
    sma_fast = prices[-10:].mean()
    sma_slow = prices[-30:].mean()

    if sma_fast > sma_slow:
        return 'buy', 0.7  # signal, confidence
    elif sma_fast < sma_slow:
        return 'sell', 0.7
    return 'hold', 0.0
```

#### 3. position sizing
- implement [[position-sizing]] kelly formula
```python
def calculate_position_size(account_balance, win_rate, win_loss_ratio, kelly_fraction=0.5):
    b = win_loss_ratio
    p = win_rate
    q = 1 - p

    kelly = (b * p - q) / b
    return account_balance * kelly * kelly_fraction  # half-kelly
```

#### 4. execution
- market orders for speed, limit orders for price
- handle partial fills
- implement retry logic
```python
def execute_order(exchange, symbol, side, amount):
    try:
        order = exchange.create_market_order(symbol, side, amount)
        return order
    except Exception as e:
        log_error(e)
        return None
```

#### 5. risk management
- max position size per trade
- max portfolio exposure
- stop losses in code
- kill switch for anomalies
```python
def check_risk_limits(portfolio, new_order):
    max_position_pct = 0.10  # 10% max per position
    max_portfolio_heat = 0.25  # 25% max total exposure

    if new_order.size / portfolio.value > max_position_pct:
        return False, "exceeds position limit"
    if portfolio.total_exposure + new_order.size > max_portfolio_heat:
        return False, "exceeds portfolio heat"
    return True, "approved"
```

### backtesting before live
- never deploy untested strategies
- use historical data to simulate performance
- account for slippage, fees, latency
- libraries: `backtrader`, `vectorbt`, `zipline`
```python
# vectorbt example
import vectorbt as vbt

price = vbt.YFData.download('BTC-USD').get('Close')
entries = fast_ma > slow_ma
exits = fast_ma < slow_ma

portfolio = vbt.Portfolio.from_signals(price, entries, exits)
print(portfolio.total_return())
```

### paper trading
- simulate live trading without real money
- Alpaca and Binance offer paper trading modes
- run for weeks before going live
- compare paper results to backtest expectations

### common automated strategies

#### mean reversion
- price deviates from average, bet on return
- works in ranging markets
- RSI oversold/overbought signals

#### momentum / trend following
- price moving in direction, bet it continues
- works in trending markets
- moving average crossovers

#### arbitrage
- price differences across venues
- requires speed and low fees
- crypto CEX vs DEX spreads

#### market making
- provide liquidity, capture spread
- requires sophisticated inventory management
- high frequency, low margin per trade

### prediction market automation
- fetch odds from Polymarket API
- compare to your probability model
- auto-bet when edge exceeds threshold
```python
def check_prediction_edge(market_price, your_estimate, min_edge=0.05):
    edge = your_estimate - market_price
    if edge > min_edge:
        kelly_size = (your_estimate - market_price) / (1 - market_price)
        return True, kelly_size * 0.5  # half kelly
    return False, 0
```

### infrastructure considerations
- **hosting** - cloud VPS for uptime (AWS, DigitalOcean)
- **latency** - co-locate near exchange servers if speed matters
- **redundancy** - backup systems, health monitoring
- **secrets** - never hardcode API keys, use environment variables

### logging and monitoring
- log every decision, order, fill, error
- dashboard for real-time portfolio state
- alerts for anomalies (position size spike, unusual loss)
- review logs weekly to improve

### common mistakes
- overfitting backtests to historical data
- ignoring slippage and fees
- no kill switch for runaway losses
- deploying without paper trading
- position sizing too aggressive early
- not logging enough data

### progression path
1. build a price alert system
2. add signal generation (no execution)
3. paper trade with auto-execution
4. live trade with tiny size
5. scale up as you trust the system
6. add more strategies and instruments

### tools and libraries
- **ccxt** - unified crypto exchange API
- **alpaca-trade-api** - stock trading
- **vectorbt** - fast backtesting
- **pandas** - data manipulation
- **apscheduler** - job scheduling
- **websocket** - real-time data streams

### key takeaways
1. automation turns knowledge into running systems
2. start with alerts, graduate to execution
3. backtest → paper trade → small live → scale
4. risk management in code is non-negotiable
5. log everything - your edge improves with data
