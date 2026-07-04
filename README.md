# Bitcoin Trader Performance vs Market Sentiment Analysis

## Overview
This project explores the relationship between trader performance on Hyperliquid and Bitcoin market sentiment (Fear & Greed Index). The goal is to uncover behavioral patterns across different sentiment regimes and translate them into actionable trading strategy recommendations.

## Datasets Used
1. **Historical Trader Data (Hyperliquid)** — 211,224 trade records with fields including Account, Coin, Execution Price, Size (Tokens/USD), Side, Timestamp, Start Position, Direction, Closed PnL, Fee, and Transaction Hash.
2. **Bitcoin Fear & Greed Index** — 2,644 daily records (2018–2025) with Date, Value (0–100), and Classification (Extreme Fear, Fear, Neutral, Greed, Extreme Greed).

## Methodology

### 1. Data Cleaning
- Converted trade timestamps to proper datetime format and extracted trade date for merging.
- Removed duplicate rows from the trader dataset.
- Standardized the sentiment dataset's date format and column names.

### 2. Merging
- Joined trader data with sentiment data on trade date (left join), tagging every trade with the market sentiment for that day.
- Only 6 out of 211,224 trades (0.00%) had no matching sentiment label — confirming a clean merge.

### 3. Filtering
- Focused analysis on "closed trades" (Closed PnL ≠ 0), since these represent realized profit/loss events rather than position-building trades.

### 4. Analysis Performed
- **PnL by Sentiment** — average, median, total PnL, and trade count per sentiment category.
- **Win Rate by Sentiment** — percentage of profitable trades per category.
- **Trade Size by Sentiment** — average position size (USD) under each market mood.
- **Net PnL & Profit Factor** — performance after accounting for trading fees.
- **Buy vs Sell Performance** — compared long vs short trade outcomes across sentiment regimes, visualized as a heatmap.
- **Coin-Level Patterns** — identified which coins performed best under which sentiment (filtered to combinations with ≥50 trades for reliability).
- **Top Traders** — identified top 10 accounts by total realized PnL, and top 5 accounts within each sentiment category.
- **Daily-Level Aggregation** — rolled trade-level data up to daily summaries to confirm patterns hold at a broader time scale, reducing trade-level noise.
- **Data Quality Checks** — verified missing values across all key columns before drawing conclusions.

## Key Findings

| Sentiment | Win Rate | Avg PnL | Avg Trade Size (USD) |
|---|---|---|---|
| Extreme Greed | 89.2% | $130.21 | $3,112 |
| Fear | 87.3% | $112.63 | $7,816 |
| Neutral | 82.4% | $71.20 | $4,783 |
| Greed | 76.9% | $85.40 | $5,737 |
| Extreme Fear | 76.2% | $71.03 | $5,350 |

- **Extreme Greed** periods show the strongest performance overall (highest win rate and average PnL), but traders take notably smaller positions — suggesting more calculated, risk-aware behavior even in euphoric conditions.
- **Fear** periods show the second-best performance, paired with the largest average trade sizes — indicating experienced traders may treat market fear as a high-conviction buying opportunity.
- **Extreme Fear** has the weakest win rate of all categories, hinting at panic-driven or impulsive trading during sharp downturns.
- **Performance is highly concentrated**: the top account alone generated over $2.1M in realized PnL, showing that individual trader skill/discipline plays a larger role than sentiment alone.

## Strategy Recommendations
1. **Reduce position size during Extreme Greed** — win rates are high, but margins per trade are thin and crowd-driven reversals are more likely.
2. **Treat Fear periods as selective high-conviction entry points** — data supports disciplined, well-capitalized entries during market fear.
3. **Apply stricter risk controls during Extreme Fear** — this regime has the weakest win rate and is most prone to panic-driven losses.
4. **Study top-performing accounts' behavior across sentiment regimes** rather than reacting to sentiment in isolation, since consistent individual discipline outweighs broad sentiment signals.

## Tools & Libraries
`Python`, `Pandas`, `NumPy`, `Matplotlib`, `Seaborn`

## Files in this Repository
- `coding.ipynb` — Full analysis notebook (data cleaning, merging, EDA, visualizations, insights)
- `historical_data.csv` — Hyperliquid trader dataset
- `fear_greed_index.csv` — Bitcoin Fear & Greed Index dataset
- `README.md` — This file
