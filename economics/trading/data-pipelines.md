---
tags: economics
---

the foundation for [[backtesting]] and [[automated-trading]] - garbage in, garbage out

### what is a data pipeline?
- system that collects, processes, stores, and delivers data
- automates the flow from source to usable format
- runs continuously or on schedule
- the infrastructure that powers every trading decision

### why data pipelines matter
- [[backtesting]] requires clean historical data
- [[automated-trading]] requires real-time data
- analysis quality is limited by data quality
- manual data collection doesn't scale
- custom data = differentiated edge

### the pipeline architecture

```
┌──────────────┐
│   sources    │ ← APIs, websockets, scraping
└──────┬───────┘
       ↓
┌──────────────┐
│   ingestion  │ ← fetch, validate, normalize
└──────┬───────┘
       ↓
┌──────────────┐
│   storage    │ ← databases, files, cloud
└──────┬───────┘
       ↓
┌──────────────┐
│  processing  │ ← clean, transform, aggregate
└──────┬───────┘
       ↓
┌──────────────┐
│   delivery   │ ← to backtester, bot, dashboard
└──────────────┘
```

### data types for trading

#### price data (OHLCV)
- open, high, low, close, volume
- foundation for technical analysis
- timeframes: 1m, 5m, 1h, 1d, etc.
```python
# typical OHLCV structure
{
    'timestamp': 1704067200000,
    'open': 42150.00,
    'high': 42300.00,
    'low': 42100.00,
    'close': 42250.00,
    'volume': 1250.5
}
```

#### order book data
- from [[market-microstructure]]: bids, asks, depth
- snapshot vs incremental updates
- level 1 (top of book) vs level 2 (full depth)

#### trade data (tick data)
- every individual trade
- highest resolution available
- large storage requirements

#### fundamental data
- earnings, revenue, ratios
- economic indicators
- for stocks and macro analysis

#### on-chain data
- from [[smart-contracts]]: blockchain transactions
- wallet movements, protocol metrics
- TVL, fees, active addresses

#### alternative data
- social sentiment (Twitter, Reddit)
- news and events
- satellite imagery, web traffic
- anything not traditional market data

### data sources

#### free sources

| source | data type | markets |
|--------|-----------|---------|
| Yahoo Finance | OHLCV daily | stocks, ETFs |
| CoinGecko | OHLCV, market cap | crypto |
| CCXT | OHLCV, order book | crypto (100+ exchanges) |
| Alpha Vantage | OHLCV, fundamentals | stocks (rate limited) |
| FRED | economic indicators | macro |

#### paid sources

| source | data type | cost |
|--------|-----------|------|
| Polygon.io | stocks, crypto tick data | $29+/mo |
| Databento | institutional quality | varies |
| Kaiko | crypto market data | enterprise |
| Quandl | alternative data | varies |
| Glassnode | on-chain metrics | $29+/mo |

#### exchange APIs
- direct from source, most accurate
- Binance, Coinbase, Kraken for crypto
- rate limits apply
- often free for basic data

### fetching data

#### REST APIs
- request/response pattern
- good for historical data
- rate limited
```python
import requests

def fetch_ohlcv(symbol, interval='1d', limit=100):
    url = f'https://api.binance.com/api/v3/klines'
    params = {
        'symbol': symbol,
        'interval': interval,
        'limit': limit
    }
    response = requests.get(url, params=params)
    return response.json()
```

#### websockets
- persistent connection, real-time updates
- for live trading and monitoring
- lower latency than polling
```python
import websocket
import json

def on_message(ws, message):
    data = json.loads(message)
    process_tick(data)

ws = websocket.WebSocketApp(
    'wss://stream.binance.com:9443/ws/btcusdt@trade',
    on_message=on_message
)
ws.run_forever()
```

#### using CCXT (crypto unified API)
```python
import ccxt

exchange = ccxt.binance()

# historical OHLCV
ohlcv = exchange.fetch_ohlcv('BTC/USDT', '1h', limit=500)

# current order book
orderbook = exchange.fetch_order_book('BTC/USDT')

# works with 100+ exchanges, same interface
```

### data validation
- never trust raw data blindly
- common issues:
  - missing candles (gaps)
  - incorrect timestamps
  - outlier prices (bad ticks)
  - duplicate records
  - timezone mismatches

```python
def validate_ohlcv(df):
    issues = []

    # check for gaps
    expected_interval = df['timestamp'].diff().mode()[0]
    gaps = df[df['timestamp'].diff() > expected_interval * 1.5]
    if len(gaps) > 0:
        issues.append(f'{len(gaps)} gaps found')

    # check OHLC logic
    invalid = df[(df['high'] < df['low']) |
                 (df['close'] > df['high']) |
                 (df['close'] < df['low'])]
    if len(invalid) > 0:
        issues.append(f'{len(invalid)} invalid candles')

    # check for outliers
    returns = df['close'].pct_change()
    outliers = df[returns.abs() > 0.5]  # 50% moves
    if len(outliers) > 0:
        issues.append(f'{len(outliers)} potential outliers')

    return issues
```

### storage options

#### flat files (CSV, Parquet)
- simple, portable
- good for small datasets
- Parquet is compressed, faster than CSV
```python
import pandas as pd

# save
df.to_parquet('btc_hourly.parquet')

# load
df = pd.read_parquet('btc_hourly.parquet')
```

#### SQLite
- file-based database
- good for medium datasets
- SQL queries, no server needed
```python
import sqlite3

conn = sqlite3.connect('trading_data.db')
df.to_sql('ohlcv', conn, if_exists='append')

# query
df = pd.read_sql('SELECT * FROM ohlcv WHERE symbol = "BTC"', conn)
```

#### PostgreSQL / TimescaleDB
- production-grade database
- TimescaleDB optimized for time-series
- handles large scale, concurrent access

#### cloud storage
- S3, Google Cloud Storage
- cheap, scalable
- good for archival and large datasets

### data processing

#### cleaning
```python
def clean_ohlcv(df):
    # remove duplicates
    df = df.drop_duplicates(subset=['timestamp'])

    # sort by time
    df = df.sort_values('timestamp')

    # fill small gaps (forward fill)
    df = df.set_index('timestamp').resample('1H').ffill()

    # remove obvious bad data
    df = df[df['volume'] > 0]

    return df
```

#### normalization
- consistent column names across sources
- unified timestamp format (UTC)
- standard symbol naming (BTC/USDT not BTCUSDT)

#### aggregation
- combine lower timeframes into higher
- 1-minute → 1-hour → 1-day
```python
def aggregate_ohlcv(df, timeframe='1H'):
    return df.resample(timeframe).agg({
        'open': 'first',
        'high': 'max',
        'low': 'min',
        'close': 'last',
        'volume': 'sum'
    })
```

### scheduling pipelines

#### cron jobs
- simple time-based scheduling
- built into Linux/Mac
```bash
# fetch daily data at 1am
0 1 * * * python /path/to/fetch_daily.py
```

#### APScheduler (Python)
```python
from apscheduler.schedulers.background import BackgroundScheduler

scheduler = BackgroundScheduler()
scheduler.add_job(fetch_ohlcv, 'interval', hours=1)
scheduler.start()
```

#### Airflow / Prefect
- production workflow orchestration
- DAGs, dependencies, monitoring
- overkill for personal use, great for scale

### real-time vs historical

#### historical data pipeline
- run daily/weekly
- backfill missing data
- store for backtesting
- less time-sensitive

#### real-time pipeline
- websocket connections
- process immediately
- feed to trading bot
- latency matters

### monitoring your pipeline
- alert on failures
- track data freshness
- log ingestion stats
- check for anomalies
```python
def check_pipeline_health():
    latest = get_latest_timestamp()
    expected = datetime.now() - timedelta(hours=1)

    if latest < expected:
        send_alert('Data pipeline stale!')
```

### building alternative data edges
- everyone has price data
- edge comes from unique data

#### ideas
- **social sentiment** - Twitter API, Reddit scraping
- **on-chain flows** - whale movements, exchange flows
- **funding rates** - crypto perpetual sentiment
- **news** - NLP on headlines
- **github activity** - protocol development pace
- **google trends** - retail interest

### example: complete pipeline

```python
# daily crypto data pipeline
import ccxt
import pandas as pd
from datetime import datetime, timedelta

def run_daily_pipeline():
    exchange = ccxt.binance()
    symbols = ['BTC/USDT', 'ETH/USDT', 'SOL/USDT']

    for symbol in symbols:
        # fetch
        ohlcv = exchange.fetch_ohlcv(symbol, '1d', limit=30)

        # transform
        df = pd.DataFrame(ohlcv, columns=['timestamp', 'open', 'high', 'low', 'close', 'volume'])
        df['timestamp'] = pd.to_datetime(df['timestamp'], unit='ms')
        df['symbol'] = symbol

        # validate
        issues = validate_ohlcv(df)
        if issues:
            log_warning(f'{symbol}: {issues}')

        # store
        df.to_parquet(f'data/{symbol.replace("/", "_")}_{datetime.now().date()}.parquet')

        # also append to database
        df.to_sql('ohlcv', conn, if_exists='append', index=False)

    log_info('Daily pipeline complete')

# schedule to run at midnight UTC
scheduler.add_job(run_daily_pipeline, 'cron', hour=0)
```

### connection to other notes
- [[backtesting]] - needs clean historical data
- [[automated-trading]] - needs real-time feeds
- [[smart-contracts]] - on-chain data from blockchain
- [[market-microstructure]] - order book data

### key takeaways
1. data quality determines analysis quality
2. validate everything - never trust raw data
3. automate collection, run on schedule
4. store in queryable format (SQL or Parquet)
5. real-time needs websockets, historical needs REST
6. alternative data is where edges hide
7. your pipeline is the foundation of your trading stack
