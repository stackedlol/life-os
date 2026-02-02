---
tags: economics
---

amplifies [[position-sizing]] - a tool that destroys accounts when misused

### what is leverage?
- borrowing to increase position size beyond your capital
- control $10,000 with $1,000 = 10x leverage
- multiplies gains AND losses equally
- a tool, not a strategy

### the math
```
leveraged return = unleveraged return × leverage

example at 10x leverage:
+5% move = +50% on your capital
-5% move = -50% on your capital
-10% move = -100% (liquidation)
```

### why leverage is dangerous
- asymmetric outcomes
- +100% gain doubles your money
- -100% loss = everything gone
- you can't recover from zero
```
at 10x leverage:
need only -10% move to lose everything
-10% moves happen regularly
```

### margin: the collateral
- margin = capital you put up as collateral
- borrowed funds come from exchange/broker
- margin ratio = equity / position size
```
initial margin: required to open position
maintenance margin: required to keep position open
if equity < maintenance margin → liquidation
```

### liquidation mechanics
- when losses approach your margin, position is force-closed
- exchange sells your position to recover borrowed funds
- you lose your margin (partially or fully)
- happens fast in volatile markets
```
liquidation price = entry price × (1 - 1/leverage)

at 10x long:
entry: $100
liquidation: $100 × (1 - 0.10) = $90
only 10% drop to get liquidated
```

### isolated vs cross margin

#### isolated margin
- margin dedicated to single position
- liquidation only affects that position
- other funds are safe
- easier to manage risk

#### cross margin
- entire account balance as margin
- positions share margin
- more margin = further liquidation price
- but losing trade can drain entire account
- dangerous for beginners

### leverage in different markets

#### crypto perpetual futures
- most common leveraged crypto product
- no expiration (unlike traditional futures)
- up to 100x+ leverage available
- funding rate mechanism keeps price near spot
- from [[market-microstructure]]: liquidations cascade

#### crypto margin trading
- borrow assets to trade spot
- lower leverage than perps (2-10x typical)
- pay interest on borrowed funds

#### DeFi leverage
- from [[smart-contracts]]: borrow against collateral
- Aave, Compound for lending/borrowing
- health factor determines liquidation
- can loop: deposit → borrow → deposit → borrow
- gas costs add up, liquidation is on-chain

#### stock margin accounts
- Reg T: 2x leverage for stocks
- pattern day trader: 4x intraday
- margin calls if equity drops
- lower leverage = more forgiving

### funding rates (perpetual futures)
- mechanism to keep perp price near spot price
- paid between longs and shorts
```
positive funding = longs pay shorts (market is bullish)
negative funding = shorts pay longs (market is bearish)
```
- paid every 8 hours typically
- can be significant cost (or income)
- check funding before entering positions

### position sizing with leverage
- from [[position-sizing]]: risk per trade stays the same
- leverage changes position size, not risk amount
```
without leverage:
$10,000 account, 2% risk = $200 max loss
position size = $200 / stop distance

with 10x leverage:
same $200 max loss
but can control larger position
stop must be tighter OR size must be smaller
```

#### the key insight
- don't think "I have 10x leverage, I'll 10x my position"
- think "I have the same risk budget, leverage lets me be capital efficient"
- risk the same dollar amount, regardless of leverage

### proper leverage sizing
```python
def leveraged_position_size(account, risk_pct, entry, stop, leverage):
    risk_amount = account * risk_pct
    stop_distance_pct = abs(entry - stop) / entry

    # position size based on risk
    position_value = risk_amount / stop_distance_pct

    # margin required
    margin_required = position_value / leverage

    # check if we have enough margin
    if margin_required > account:
        return None, "insufficient margin"

    return position_value, margin_required

# example:
# $10k account, 2% risk, entry $100, stop $95, 10x leverage
# risk_amount = $200
# stop_distance = 5%
# position_value = $200 / 0.05 = $4,000
# margin_required = $4,000 / 10 = $400
```

### when leverage makes sense
- **capital efficiency** - same risk, less capital tied up
- **hedging** - short positions to offset longs
- **arbitrage** - small edges require size to be profitable
- **professional strategies** - when edge is validated and risk is controlled

### when leverage destroys
- **gambling mentality** - "let it ride" with max leverage
- **no stop loss** - hoping it comes back
- **averaging down** - adding to losers with leverage
- **ignoring funding** - costs eat profits
- **emotional trading** - revenge trading after loss

### liquidation cascades
- leveraged positions liquidate in volatile moves
- liquidations are market sells (for longs)
- selling pressure causes more price drop
- more liquidations trigger
- cascades crash markets fast
```
price drops 5%
  → overleveraged longs liquidated
  → forced selling
  → price drops another 5%
  → more liquidations
  → cascade
```
- this is why crypto crashes are violent

### protecting yourself

#### use stops
- stop loss before liquidation price
- give yourself margin of safety
```
liquidation at $90
stop loss at $93
buffer for slippage and volatility
```

#### reduce leverage
- just because 100x exists doesn't mean use it
- 2-5x is plenty for most strategies
- lower leverage = more room for error

#### isolated margin
- limit damage to single position
- don't let one bad trade drain account

#### monitor funding
- high funding = crowded trade
- you're paying to hold the position
- consider closing or flipping

#### avoid liquidation zones
- price often sweeps obvious liquidation levels
- from [[market-microstructure]]: liquidity at liquidation prices
- market makers hunt stops and liquidations

### leverage and kelly criterion
- from [[position-sizing]]: kelly assumes you can't lose more than you bet
- leverage breaks this assumption
- full kelly with leverage = guaranteed ruin eventually
- use fractional kelly AND lower leverage
```
if kelly says bet 20% of account:
with 5x leverage, margin = 4% of account
still risking 20%, but capital efficient
```

### DeFi-specific leverage risks
- smart contract risk (bugs, exploits)
- oracle manipulation (flash loan attacks)
- gas costs during liquidation (may fail)
- network congestion (can't close in time)
- from [[smart-contracts]]: read the liquidation logic

### metrics to track
- **leverage ratio** - position size / equity
- **margin ratio** - equity / required margin
- **liquidation price** - know it exactly
- **funding rate** - cost of carrying position
- **unrealized PnL** - how close to liquidation

### common mistakes
- using max leverage because it's available
- not knowing liquidation price
- cross margin with multiple positions
- ignoring funding rates
- adding to losing leveraged positions
- no stop loss
- trading size based on leverage, not risk

### key takeaways
1. leverage amplifies everything - gains, losses, and mistakes
2. risk the same dollar amount with or without leverage
3. know your liquidation price before entering
4. use isolated margin to contain damage
5. lower leverage = more room for error
6. funding rates are real costs
7. liquidation cascades make crashes violent
8. leverage is a tool for capital efficiency, not gambling
