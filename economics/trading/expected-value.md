---
tags: economics
---

the mathematical foundation for [[position-sizing]], [[prediction-markets]], and [[backtesting]]

### what is expected value?
- the average outcome of a decision if repeated many times
- weighted average of all possible outcomes by their probabilities
- the single number that tells you if a bet is good or bad
- positive EV = take the bet. negative EV = don't.

### the formula
```
EV = Σ (probability × outcome)

or for a simple bet:
EV = (p_win × win_amount) - (p_lose × lose_amount)
```

### example: simple bet
- you bet $100 to win $150
- you estimate 50% chance of winning
```
EV = (0.50 × $150) - (0.50 × $100)
EV = $75 - $50
EV = +$25
```
- positive EV: take this bet every time

### example: trading
- trade risks $100 to make $200
- based on [[backtesting]], win rate is 40%
```
EV = (0.40 × $200) - (0.60 × $100)
EV = $80 - $60
EV = +$20 per trade
```
- positive EV despite losing more often than winning

### why EV matters more than win rate
- a strategy can win 30% of the time and be highly profitable
- a strategy can win 70% of the time and lose money
- what matters: (win rate × avg win) vs (loss rate × avg loss)

| strategy | win rate | avg win | avg loss | EV |
|----------|----------|---------|----------|-----|
| A | 70% | $50 | $150 | -$10 |
| B | 30% | $300 | $50 | +$55 |

strategy B is far better despite lower win rate

### expected value vs variance
- EV tells you the average outcome
- variance tells you how bumpy the ride is
- two strategies can have same EV but different variance
```
strategy 1: always returns +$10
strategy 2: 50% chance of +$110, 50% chance of -$90
both have EV = +$10, but very different experiences
```
- [[position-sizing]] manages variance while capturing EV

### the law of large numbers
- individual outcomes are random
- over many trials, results converge to EV
- this is why you need enough trades (sample size)
- short-term: anything can happen
- long-term: EV dominates

### probability fundamentals

#### basic rules
```
P(A) = outcomes where A happens / total outcomes
P(not A) = 1 - P(A)
P(A and B) = P(A) × P(B)  [if independent]
P(A or B) = P(A) + P(B) - P(A and B)
```

#### conditional probability
- probability of A given B has occurred
```
P(A|B) = P(A and B) / P(B)
```
- critical for updating beliefs with new information

#### bayes' theorem
- how to update probability with new evidence
```
P(hypothesis|evidence) = P(evidence|hypothesis) × P(hypothesis) / P(evidence)
```
- prior belief + new data = updated belief
- foundation of rational thinking under uncertainty

### common probability mistakes

#### gambler's fallacy
- believing past outcomes affect future independent events
- "red came up 5 times, black is due"
- each flip/spin/trade is independent
- the market doesn't owe you a win

#### hot hand fallacy
- believing streaks indicate skill when they're random
- or dismissing real skill as randomness
- need statistical significance to tell the difference

#### base rate neglect
- ignoring how common something is in general
- "this stock matches the pattern of 10x winners"
- but if only 1% of stocks 10x, pattern is weak signal

#### overconfidence
- estimating probabilities with false precision
- saying 80% when you really mean "probably"
- calibration training fixes this

#### confirmation bias
- seeking evidence that confirms existing beliefs
- ignoring disconfirming evidence
- forces bad probability estimates

### calibration: the meta-skill
- are your probability estimates accurate?
- if you say 70% confidence, does it happen 70% of the time?
- most people are overconfident

#### how to calibrate
1. make predictions with explicit probabilities
2. track outcomes
3. compare predicted vs actual frequencies
4. adjust future estimates

#### calibration chart
```
if your 60% predictions hit 60% of the time → calibrated
if your 60% predictions hit 80% of the time → underconfident
if your 60% predictions hit 40% of the time → overconfident
```

### applying EV to decisions

#### trading decisions
- every trade is an EV calculation
- estimate: win probability, win size, loss size
- only take positive EV trades
- [[position-sizing]] determines how much to bet on positive EV

#### prediction market bets
- market price = implied probability
- your estimate vs market = your edge
- EV = (your_prob × payout) - (market_price)
- from [[prediction-markets]]: only bet when EV > 0

#### life decisions
- same framework applies
- career move: probability of success × upside vs downside
- time investment: expected return on hours spent
- learning: probability skill is useful × value of skill

### edge: the practical EV concept
- edge = your EV advantage over the market/opponent
- expressed as percentage or expected return
```
edge = your_probability - implied_probability
edge = expected_return - cost
```
- small edges compound over many bets
- large edges are rare and valuable

### edge erosion
- edges don't last forever
- others discover them
- market adapts
- fees/slippage eat into edge
- must continuously find new edges or optimize execution

### risk of ruin revisited
- positive EV doesn't guarantee success
- variance can wipe you out before EV converges
- from [[position-sizing]]: size bets to survive variance
- kelly criterion maximizes EV growth while managing ruin risk

### multi-outcome decisions
- not all bets are binary
- some have multiple possible outcomes
```
investment scenarios:
- 20% chance: 3x return
- 50% chance: 1.2x return
- 30% chance: 0.5x return

EV = (0.20 × 3) + (0.50 × 1.2) + (0.30 × 0.5)
EV = 0.6 + 0.6 + 0.15
EV = 1.35x (35% expected return)
```

### opportunity cost
- every decision has alternatives
- true EV = EV of choice - EV of best alternative
- sitting in cash has EV (risk-free rate, optionality)
- locked capital can't capture other opportunities

### expected value of information
- sometimes worth paying to reduce uncertainty
- research, data, expert opinions have value
- calculate: how much would better probability estimate be worth?
```
current: 60% confident, sizing at X
with research: 80% confident, sizing at Y
value of research = EV(Y) - EV(X) - cost of research
```

### mental models

#### think in bets
- every decision is a bet on an outcome
- "I'm betting that this trade will work"
- makes probability thinking automatic

#### expected value, not outcomes
- judge decisions by process, not results
- good EV decisions can have bad outcomes
- bad EV decisions can have good outcomes
- focus on making +EV decisions consistently

#### uncertainty is permanent
- you never have perfect information
- goal: be less wrong than others
- calibration + edge finding = profitable uncertainty

### key takeaways
1. EV = probability-weighted average outcome
2. positive EV decisions compound over time
3. win rate matters less than EV
4. variance is the enemy - sizing manages it
5. calibration is the meta-skill for probability
6. think in bets: every decision is an EV calculation
7. judge process (EV), not outcomes (luck)
