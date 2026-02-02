---
tags: economics
---

how markets actually work under the hood - essential for [[automated-trading]] execution

### what is market microstructure?
- the mechanics of how trades happen
- how prices form from individual orders
- the infrastructure between "I want to buy" and "I own it"
- understanding this = better execution, finding edges

### the order book
- central data structure of most markets
- two sides: bids (buyers) and asks (sellers)
```
        asks (sellers)
        $101.50  500 shares
        $101.25  200 shares
        $101.00  1000 shares  ← best ask (lowest sell)
        ------- spread -------
        $100.75  800 shares   ← best bid (highest buy)
        $100.50  300 shares
        $100.25  1500 shares
        bids (buyers)
```
- best bid and best ask = "top of book"
- depth = volume at each price level

### bid-ask spread
- difference between best bid and best ask
- the cost of immediacy
```
spread = best_ask - best_bid
spread % = spread / midpoint
```
- tight spread = liquid market, low cost to trade
- wide spread = illiquid, expensive to trade
- spread is profit for market makers, cost for takers

### midpoint price
- theoretical "fair" price
```
midpoint = (best_bid + best_ask) / 2
```
- used as reference for measuring execution quality
- your fill vs midpoint = your execution cost

### order types

#### market order
- execute immediately at best available price
- guarantees fill, not price
- crosses the spread (pays the spread cost)
- use when speed matters more than price

#### limit order
- execute only at specified price or better
- provides liquidity, earns the spread
- may not fill if price doesn't reach your level
- use when price matters more than speed

#### stop order
- becomes market order when price hits trigger
- used for stop losses and breakout entries
- can get poor fills in fast markets (slippage)

#### stop-limit order
- becomes limit order when price hits trigger
- more price control but may not fill
- dangerous for stop losses (might not exit)

### makers vs takers

#### market makers (liquidity providers)
- post limit orders on both sides
- earn the spread on each round trip
- take inventory risk (holding positions)
- profit from spread, lose from adverse selection

#### takers (liquidity consumers)
- use market orders, cross the spread
- pay the spread cost for immediacy
- informed traders are often takers
- moving the market is expensive

### price impact
- your order moves the price against you
- larger orders = more impact
```
buy 100 shares at $100 → fills at $100
buy 10,000 shares at $100 → fills at $100.50 average
```
- eating through multiple price levels
- why large funds break orders into pieces

### slippage
- difference between expected price and actual fill
```
slippage = fill_price - expected_price
```
- caused by: price impact, latency, volatility
- always model slippage in [[backtesting]]
- reduces or eliminates edge if not managed

### liquidity
- ability to trade without moving the price
- measured by: spread, depth, volume
- high liquidity: tight spread, deep book, high volume
- low liquidity: wide spread, thin book, low volume

#### why liquidity matters
- determines your execution costs
- limits your position size
- affects how fast you can exit
- illiquid markets = hidden costs

### market maker economics
- make money from spread, lose from informed flow
```
profit per trade = spread / 2
loss from informed = adverse selection cost
```
- widen spreads when uncertainty is high
- narrow spreads when flow is uninformed
- this is why spreads widen around news events

### adverse selection
- trading against someone who knows more than you
- market makers fear informed traders
- informed flow = losing trades for the maker
- uninformed flow = profitable trades for the maker
- makers adjust prices to protect against this

### order flow
- the stream of buy and sell orders
- **informed flow** - traders with edge/information
- **uninformed flow** - retail, random, noise
- tracking order flow reveals who's trading

### market impact models

#### linear impact
```
impact = k × order_size / daily_volume
```
- simple but rough approximation

#### square root model
```
impact = k × sqrt(order_size / daily_volume)
```
- more accurate for large orders
- used by institutional traders

### execution strategies

#### TWAP (time-weighted average price)
- split order evenly over time
- simple, predictable
- doesn't adapt to market conditions

#### VWAP (volume-weighted average price)
- trade proportional to market volume
- blend in with the crowd
- benchmark for institutional execution

#### implementation shortfall
- minimize total cost (impact + timing risk)
- trade faster when urgent, slower when patient
- most sophisticated approach

### latency
- time delay in market data and order execution
- lower latency = see prices faster, execute faster
- matters for: arbitrage, market making, HFT
- less critical for: swing trading, position trading

### market structure by venue

#### stock exchanges (NYSE, NASDAQ)
- central limit order book
- regulated, transparent
- multiple exchanges = fragmentation
- dark pools for large orders

#### crypto exchanges (Binance, Coinbase)
- similar order book structure
- 24/7 trading
- less regulated
- CEX (centralized) vs DEX (decentralized)

#### DEX (Uniswap, etc.)
- automated market makers (AMMs)
- no order book - liquidity pools
- price determined by formula: x × y = k
- always liquidity but high slippage on size

#### prediction markets (Polymarket)
- order book for each outcome (yes/no)
- prices = probabilities
- liquidity varies by market popularity
- from [[prediction-markets]]: factor in spread when sizing

### AMM deep dive
- liquidity providers deposit token pairs
- price = ratio of tokens in pool
```
constant product formula:
token_A × token_B = k (constant)

if pool has 100 ETH and 200,000 USDC:
price = 200,000 / 100 = $2,000 per ETH
```
- buying ETH removes ETH, adds USDC, price rises
- large trades = significant price impact

### finding microstructure edges

#### spread capture
- post limit orders, earn spread
- requires inventory management
- risk: adverse selection, being picked off

#### latency arbitrage
- exploit price differences across venues
- requires speed advantage
- highly competitive, diminishing returns

#### statistical arbitrage
- trade mean reversion in related assets
- pairs trading, index arbitrage
- requires understanding of correlations

#### order flow prediction
- predict short-term price moves from order flow
- tape reading, imbalance signals
- used by market makers and HFT

### practical applications

#### for automated trading
- factor spread into entry/exit calculations
- use limit orders when possible
- model slippage based on order size
- avoid trading illiquid instruments
- time trades to avoid low liquidity periods

#### for backtesting
- from [[backtesting]]: include realistic slippage
- model spread crossing for market orders
- account for partial fills on limit orders
- test on different liquidity regimes

#### for position sizing
- from [[position-sizing]]: liquidity constrains max size
- can't size bigger than market can absorb
- impact cost increases with size

### metrics to monitor
- **bid-ask spread** - cost of immediacy
- **depth** - volume at each price level
- **volume** - total daily activity
- **volatility** - affects spread width
- **fill rate** - percentage of limit orders that execute

### key takeaways
1. the order book is the core data structure of markets
2. spread = cost of trading, paid by takers, earned by makers
3. price impact increases with order size
4. liquidity determines execution quality
5. model slippage and spread in all backtests
6. use limit orders to save spread when time permits
7. understanding microstructure reveals where edges live
