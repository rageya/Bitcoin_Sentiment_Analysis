# Trader Performance and Market Sentiment Analysis

A data science project analysing how Bitcoin market sentiment
influences trader behaviour and performance on Hyperliquid,
a decentralised perpetual futures exchange.

---

## Project Summary

This analysis merges two datasets — historical trade records
from Hyperliquid and the Bitcoin Fear & Greed Index — to
uncover how market sentiment affects profitability, trade
sizing, directional bias, and overall trader behaviour.

The project goes beyond basic exploratory analysis by
incorporating fee-adjusted PnL, statistical hypothesis
testing, coin-level breakdowns, and unsupervised machine
learning (K-Means) to segment traders into behavioural
archetypes.

---

## Key Findings

**Finding 1 — The Contrarian Advantage**
Traders who open positions during Fear phases consistently
earn higher fee-adjusted PnL compared to those trading during
Greed. This difference is statistically significant
(Mann-Whitney U, p < 0.05).

**Finding 2 — Greed Drives Oversizing**
Average position size (USD) peaks during Extreme Greed,
indicating traders systematically overcommit capital when
sentiment is euphoric. This is the primary driver of large
drawdowns on sentiment reversals.

**Finding 3 — Profit Factor Diverges at Extremes**
Profit factor exceeds 1.0 only during Fear and Extreme Fear
phases. During Greed, the ratio drops below 1.0, meaning
traders lose more on losing trades than they gain on winners
— even when win rate appears stable.

**Finding 4 — Distinct Trader Archetypes Exist**
K-Means clustering (optimal K selected via Silhouette Score)
identifies clear trader segments. The top-performing cluster
(Disciplined Traders) earns more while maintaining lower PnL
volatility and higher trade selectivity than the average.

---

## Project Structure

```
trader-sentiment-analysis/
│
├── analysis.ipynb                     # Full analysis notebook
│
├── outputs/
│   ├── sentiment_performance_summary.csv
│   ├── coin_sentiment_pnl.csv
│   ├── trader_clusters.csv
│   ├── chart0_coin_sentiment_heatmap.png
│   ├── chart1_core_performance.png
│   ├── chart2_timeseries.png
│   ├── chart3_kmeans_clusters.png
│   └── chart4_cluster_heatmap.png
│
└── README.md
```

---

## Methodology

| Step | Approach |
|---|---|
| PnL adjustment | Fee deduction from gross PnL + IQR winsorizing (1st–99th percentile) to handle outliers |
| Sentiment merge | Date-normalised left join between trade timestamps and daily FG classification |
| Sentiment streaks | Consecutive same-label days counted to capture compounding behavioural effects |
| Statistical tests | Mann-Whitney U (Fear vs Greed) and Kruskal-Wallis (all 5 groups) |
| Trader features | 9 features: win rate, profit factor, PnL volatility, position size, trade count, fear/greed trade %, long ratio, weekend activity |
| Clustering | K-Means with Silhouette Score for optimal K selection (range 2–7) |
| Visualisation | 5 chart panels using Matplotlib and Seaborn |

---

## How to Run

**Step 1 — Clone the repository**
```bash
git clone https://github.com/rageya/Bitcoin_Sentiment_Analysis.git
cd Bitcoin_Sentiment_Analysis
```

**Step 2 — Place the dataset files in the project root**
```
historical_data.csv
fear_greed_index.csv
```

**Step 3 — Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
```

**Step 4 — Run the notebook**

Open `analysis.ipynb` in Jupyter or Google Colab and run
all cells from top to bottom. All charts and CSV files will
be saved automatically to the `outputs/` folder.

---

## Dependencies

| Library | Purpose |
|---|---|
| pandas | Data loading, cleaning, merging |
| numpy | Numerical operations |
| matplotlib | Charting and visualisation |
| seaborn | Heatmaps and statistical plots |
| scipy | Mann-Whitney U and Kruskal-Wallis tests |
| scikit-learn | K-Means clustering and feature scaling |

---

## Dataset Sources

Both datasets were provided by Primetrade.ai as part of a
Data Science internship assignment.

- **Historical Trades** — Hyperliquid perpetual futures exchange trade records
- **Fear & Greed Index** — Daily Bitcoin market sentiment classifications

---

## Author

**Rageya Singh**
B.Tech Computer Science — KIIT University, Bhubaneswar

- GitHub: [github.com/rageya](https://github.com/rageya)
- Email: rageyasinghr@gmail.com

---

*This project was completed as part of the Primetrade.ai Data Science Internship selection process.*
