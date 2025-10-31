# Temp.csv Dataset Overview

## Data Summary
- **Source file**: `temp.csv`
- **Tickers covered**: Samsung Electronics (005930.KS), Apple (AAPL), NVIDIA (NVDA)
- **Metrics provided**: open, high, low, close prices and trading volume.
- **Date range**: 2023-10-16 to 2025-10-10 (482–499 trading days per ticker).

The CSV uses a three-row header. The first column stores the trading date (`Price_Ticker_Date`).
Subsequent columns combine metric name and ticker symbol (for example, `Close_AAPL`).

## Descriptive Statistics
The table below captures core descriptive statistics computed across the available period for each ticker.

| Ticker | Metric | Count | Mean | Median | Min | Max |
| --- | --- | --- | --- | --- | --- | --- |
| 005930.KS | Close | 482 | 66,471.53 | 68,812.25 | 48,968.97 | 94,400.00 |
| 005930.KS | High | 482 | 67,202.08 | 69,490.01 | 50,784.92 | 94,500.00 |
| 005930.KS | Low | 482 | 65,822.65 | 68,408.07 | 48,968.97 | 92,700.00 |
| 005930.KS | Open | 482 | 66,509.00 | 68,872.64 | 49,263.38 | 94,000.00 |
| 005930.KS | Volume | 482 | 19,481,204.69 | 17,577,060.00 | 2,957,915.00 | 57,691,266.00 |
| AAPL | Close | 499 | 209.52 | 212.02 | 163.82 | 258.10 |
| AAPL | High | 499 | 211.47 | 213.70 | 165.21 | 259.24 |
| AAPL | Low | 499 | 207.33 | 209.35 | 162.91 | 256.72 |
| AAPL | Open | 499 | 209.29 | 210.92 | 164.17 | 257.99 |
| AAPL | Volume | 499 | 56,558,297.39 | 50,036,300.00 | 23,234,700.00 | 318,679,900.00 |
| NVDA | Close | 499 | 115.60 | 120.67 | 40.30 | 192.57 |
| NVDA | High | 499 | 117.54 | 122.40 | 40.85 | 195.62 |
| NVDA | Low | 499 | 113.41 | 117.41 | 39.21 | 191.06 |
| NVDA | Open | 499 | 115.59 | 120.32 | 40.43 | 193.51 |
| NVDA | Volume | 499 | 325,122,504.81 | 289,680,000.00 | 105,157,000.00 | 1,142,269,000.00 |

## Notable Observations
- **Trading span**: The dataset holds roughly two years of trading data per company, with Samsung having slightly fewer entries (likely due to market holidays).
- **Relative price levels**: Samsung trades in the ₩48,969–₩94,400 range, Apple in $163.82–$258.10, and NVIDIA in $40.30–$192.57 across the sample.
- **Volume extremes**: Highest recorded volumes occurred on 2024-01-11 (Samsung, 57.7M shares), 2024-09-20 (Apple, 318.7M shares), and 2024-03-08 (NVIDIA, 1.14B shares).
- **Volatility snapshots**:
  - Samsung’s steepest daily swing was -10.30% between 2024-08-02 and 2024-08-05.
  - Apple’s largest jump was +15.33% on 2025-04-09 following a $172.00 to $198.36 move.
  - NVIDIA’s biggest move was +18.72% on 2025-04-09, rebounding from $96.29 to $114.32.

## Reproducing the Analysis
Use the Python standard library to parse the multi-row header and compute statistics:

```python
import csv
from datetime import datetime

with open("temp.csv", newline="") as f:
    reader = csv.reader(f)
    header1, header2, header3 = [next(reader) for _ in range(3)]
    cols = ["_".join(filter(None, parts)) or f"col{i}" for i, parts in enumerate(zip(header1, header2, header3))]

    records = [dict(zip(cols, row)) for row in reader if row[0]]

# Example: mean close price for Apple
aapl_closes = [float(r["Close_AAPL"]) for r in records if r["Close_AAPL"]]
mean_aapl_close = sum(aapl_closes) / len(aapl_closes)
```

This README captures the headline findings; tailor or extend the code to perform deeper analytics (e.g., rolling averages or correlation analysis) as needed.
