# 📊 Hyperliquid Sentiment Analysis

> Analyzing how Bitcoin market sentiment (Fear/Greed Index) relates to trader behavior and performance on Hyperliquid.

---

## Table of Contents

- [Overview](#overview)
- [Datasets](#datasets)
- [Project Structure](#project-structure)
- [Key Steps](#key-steps)
- [Results & Findings](#results--findings)
- [Insights & Recommendations](#insights--recommendations)
- [Next Steps](#next-steps)
- [Tech Stack](#tech-stack)

---

## Overview

This project explores the relationship between **Bitcoin market sentiment** and **real trader activity** on Hyperliquid, one of the most active on-chain perpetuals platforms. By merging daily sentiment scores with granular trade-level data, we uncover measurable patterns in how fear and greed influence trader decision-making and profitability.

**Core question:** Does market sentiment predict trader performance — and if so, how?

---

## Datasets

### 1. Fear & Greed Index
| Column | Description |
|---|---|
| `date` | Daily timestamp |
| `value` | Numeric sentiment score (0–100) |
| `classification` | Label: `Extreme Fear` → `Extreme Greed` |

### 2. Hyperliquid Historical Trader Data
| Column | Description |
|---|---|
| `account` | Trader wallet address |
| `execution_price` | Price at which trade was executed |
| `side` | `buy` or `sell` |
| `size_usd` | Trade size in USD |
| `closed_pnl` | Realized profit/loss |
| `timestamp` | Trade datetime |

---

## Project Structure

```
hyperliquid-sentiment-analysis/
│
├── data/
│   ├── fear_greed_index.csv
│   └── hyperliquid_trades.csv
│
├── notebooks/
│   └── sentiment_analysis(test).ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── feature_engineering.py
│   └── visualization.py
│
├── outputs/
│   └── figures/
│
├── requirements.txt
└── README.md
```

---

## Key Steps

### 1. Data Cleaning & Preprocessing
- Standardized date formats across both datasets
- Merged on `date` field to align sentiment with trade activity
- Encoded sentiment classification as ordinal integers:

  | Label | Encoded Value |
  |---|---|
  | Extreme Fear | 0 |
  | Fear | 1 |
  | Neutral | 2 |
  | Greed | 3 |
  | Extreme Greed | 4 |

- Filtered and retained only relevant trade columns

### 2. Feature Engineering

**Trade-Level Features**
- `pnl_bin` — Binary profit/loss flag (1 = profitable, 0 = loss)
- `side_binary` — Buy = 1, Sell = 0
- `normalized_pnl` — PnL adjusted by trade size (removes size bias)

**Account-Level Daily Aggregates**
- Total PnL per trader per day
- Profit rate (% of profitable trades)
- Buy ratio (% of trades that are buys)
- Average trade size

### 3. Analysis & Visualization
- Boxplots of PnL distribution segmented by sentiment class
- Buy/sell ratio shifts across sentiment regimes
- Trade size and volume patterns by sentiment
- All visualizations built with `seaborn` and `matplotlib`

---

## Results & Findings

### Performance Varies Significantly with Sentiment

| Sentiment | Avg PnL | Profit Rate | Notes |
|---|---|---|---|
| Extreme Fear | ↓ Low | ↓ Low | Higher loss frequency |
| Fear | Below avg | Below avg | — |
| Neutral | Baseline | Baseline | — |
| Greed | ↑ High | ↑ High | Strong upward trend |
| Extreme Greed | ↑↑ High | ↑ High | Momentum-driven gains |

### Trade Direction is Sentiment-Driven
- **Buy-side dominates** during Greed and Extreme Greed phases
- **Sell/short activity increases** noticeably during Fear
- Traders behaviorally mirror market mood rather than trading against it

### Risk-Taking Scales with Sentiment
- Average trade size is **larger during Greed** periods
- Trade volume also increases when sentiment is positive
- During Fear, traders reduce size and frequency — consistent with risk-off behavior

---

## Insights & Recommendations

### For Individual Traders
- Use the daily sentiment score as a **macro filter** before entering trades
- Avoid overtrading during Fear phases — the data shows lower win rates
- During Greed, momentum tends to be real — but implement position sizing to protect against reversals

### For Algorithmic Strategy Design
- Include `sentiment_score` as a feature in any ML-based trade prediction model
- Implement **dynamic position sizing** that contracts during Fear and expands during Greed
- Consider **sentiment-conditional stop-loss logic** as a risk management layer

### For Analysts & Firms
- Segment performance reports by sentiment class to normalize for macro conditions
- Identify traders who **outperform during Fear** — these may be contrarians or mean-reverters with a real edge worth studying

---

## Next Steps

- [ ] Build a **Streamlit dashboard** for live sentiment + trader performance monitoring
- [ ] Run **clustering analysis** to define trader personas by sentiment response profile
- [ ] Train an **ML classifier** to predict profitable trades using sentiment + trade features as inputs
- [ ] Integrate live Fear & Greed API feed for real-time analysis

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.x-lightgrey?logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-teal)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Plotting-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)

---

## License

MIT License — feel free to use, fork, and build on this.

