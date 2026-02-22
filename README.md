# Market Neutral Pairs Trading Framework

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Streamlit](https://img.shields.io/badge/streamlit-1.28+-red.svg)](https://streamlit.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Production-ready backtesting engine for market-neutral equity strategies. Built during quantitative research internship at AperioHub for a Singapore-based Family Office ($150M AUM).

<p align="center">
  <img src="assets/demo.gif" alt="Demo" width="800"/>
</p>

## 🎯 Features

- **✅ Market Neutrality Validation** - Beta tracking vs benchmark (target: β ≈ 0)
- **✅ Z-Score Signal Generation** - Statistical mean reversion methodology
- **✅ Realistic Cost Modeling** - Configurable transaction costs (1-20 bps)
- **✅ Comprehensive Analytics** - 14+ institutional-grade performance metrics
- **✅ Interactive Interface** - Real-time parameter adjustment and visualization
- **✅ Export Capabilities** - Download results as CSV for further analysis



## 📊 Performance Metrics

The framework tracks:

- **Returns:** CAGR, Total Return, Annualized Volatility
- **Risk-Adjusted:** Sharpe Ratio, Sortino Ratio, Calmar Ratio
- **Drawdown:** Maximum Drawdown, Average Drawdown Duration
- **Trading:** Hit Rate, Win/Loss Ratio, Average Trade Duration
- **Market Neutrality:** Beta vs Benchmark, Correlation, Net Exposure
- **Execution:** Turnover, Transaction Costs, Slippage Impact

## 🛠️ Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager

### Quick Start

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/market-neutral-backtest.git
cd market-neutral-backtest

# Install dependencies
pip install -r requirements.txt

# Run the Streamlit app
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

## 📖 Usage

### Basic Example

```python
from backtest import MarketNeutralBacktest

# Initialize backtest
backtest = MarketNeutralBacktest(
    ticker1='AAPL',
    ticker2='MSFT',
    start_date='2020-01-01',
    end_date='2024-01-01'
)

# Run backtest
results = backtest.run(
    zscore_window=60,
    entry_threshold=1.5,
    exit_threshold=0.5,
    transaction_cost_bps=10
)

# Display results
print(results.metrics)
```

### Interactive Web Interface

The Streamlit app provides:

1. **Pair Selection** - Choose from preset pairs or enter custom tickers
2. **Parameter Control** - Adjust strategy parameters in real-time
3. **Visual Analytics** - Interactive charts (equity, drawdown, exposure)
4. **Market Neutrality Dashboard** - Live beta and correlation tracking
5. **Results Export** - Download complete backtest data

## 📁 Project Structure

```
market-neutral-backtest/
│
├── app.py                      # Streamlit web application
├── backtest/
│   ├── __init__.py
│   ├── engine.py              # Core backtesting engine
│   ├── signals.py             # Signal generation logic
│   ├── portfolio.py           # Portfolio construction
│   └── metrics.py             # Performance calculations
│
├── data/
│   └── sample_data.csv        # Sample price data
│
├── notebooks/
│   └── analysis.ipynb         # Jupyter notebook with examples
│
├── tests/
│   └── test_backtest.py       # Unit tests
│
├── assets/
│   └── demo.gif               # Demo screenshots
│
├── requirements.txt           # Python dependencies
├── LICENSE                    # MIT License
└── README.md                  # This file
```

## 🧪 Methodology

### Signal Generation

The framework uses **Z-score based mean reversion**:

1. Calculate price ratio: `ratio = Price₁ / Price₂`
2. Compute rolling statistics: `μ = rolling_mean(ratio)`, `σ = rolling_std(ratio)`
3. Generate Z-score: `z = (ratio - μ) / σ`
4. Trading signals:
   - **Long spread** when `z < -entry_threshold` (ratio cheap)
   - **Short spread** when `z > entry_threshold` (ratio expensive)
   - **Exit** when `|z| < exit_threshold`

### Portfolio Construction

Market-neutral positions maintain:

- **Dollar Neutrality:** Equal long and short positions (Σw = 0)
- **Beta Neutrality:** Portfolio beta ≈ 0 relative to benchmark
- **Example:** $50 long AAPL + $50 short MSFT = $0 net exposure

### Transaction Costs

Realistic cost modeling includes:

- Configurable basis points per trade (default: 10 bps)
- Applied on position changes (entry/exit/rebalance)
- Tracked separately for performance attribution

## 📈 Example Results

**Test Configuration:**
- Pair: AAPL vs MSFT
- Period: 2020-2024
- Window: 60 days
- Entry: ±1.5σ
- Transaction Costs: 10 bps

**Results:**

| Metric | Value |
|--------|-------|
| CAGR | 2.1% |
| Sharpe Ratio | 0.25 |
| Max Drawdown | -12.3% |
| Beta vs SPY | 0.08 |
| Hit Rate | 52.1% |

**Key Insight:** Framework successfully maintained market neutrality (β ≈ 0), but alpha generation was limited due to regime shifts in 2020-2024 period.

## 💡 Key Learnings

This project demonstrates:

1. **Market neutrality is a constraint, not a return generator** - Removing market exposure doesn't create alpha
2. **Correlation ≠ mean reversion** - Statistical relationships don't guarantee economic convergence
3. **Regime dependence matters** - Strategies perform differently in trending vs mean-reverting markets
4. **Process > individual results** - Rigorous testing prevents capital loss in production

## 🔧 Advanced Usage

### Walk-Forward Analysis

```python
from backtest import WalkForwardAnalysis

wfa = WalkForwardAnalysis(
    ticker1='AAPL',
    ticker2='MSFT',
    train_period=252,  # 1 year
    test_period=63     # 3 months
)

results = wfa.run()
print(results.degradation_analysis)
```

### Parameter Optimization

```python
from backtest import ParameterOptimizer

optimizer = ParameterOptimizer(
    ticker1='AAPL',
    ticker2='MSFT',
    start_date='2020-01-01',
    end_date='2024-01-01'
)

best_params = optimizer.grid_search(
    windows=[30, 60, 90],
    entry_thresholds=[1.0, 1.5, 2.0],
    exit_thresholds=[0.3, 0.5, 0.7]
)
```

## 🧰 Technologies Used

- **Python 3.8+** - Core programming language
- **pandas** - Data manipulation and analysis
- **NumPy** - Numerical computing
- **yfinance** - Market data retrieval
- **Streamlit** - Web application framework
- **Plotly** - Interactive visualizations
- **SciPy** - Statistical analysis

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Areas for Improvement

- [ ] Add regime detection (bull/bear/sideways)
- [ ] Implement machine learning signal enhancement
- [ ] Include more sophisticated cost models (slippage, market impact)
- [ ] Add multi-pair portfolio optimization
- [ ] Implement real-time data streaming
- [ ] Add options-based market-neutral strategies

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**[AARYAN GOSWAMI]**

- LinkedIn: [www.linkedin.com/in/aaryan-goswami-058920240]
- Email: aaryangoswami273@gmail.com

## 🙏 Acknowledgments

- Built during internship at **AperioHub** (Role 4: Backtest & Performance Lead)
- Project context: Market-neutral strategy evaluation for Singapore Family Office
- Special thanks to the mentors who provided guidance on institutional-grade backtesting practices

## ⚠️ Disclaimer

This is an educational project demonstrating quantitative research methodology. 

**Important:**
- Past performance does not guarantee future results
- This is NOT financial advice
- Always conduct your own due diligence before trading
- Understand the risks involved in algorithmic trading

## 📚 Further Reading

- [Quantitative Trading Strategies](https://www.quantstart.com/)
- [Statistical Arbitrage](https://en.wikipedia.org/wiki/Statistical_arbitrage)
- [Market Neutral Strategies](https://www.investopedia.com/terms/m/marketneutral.asp)
- [Pairs Trading Research](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=141615)

---

**Star ⭐ this repo if you found it helpful!**

**Questions? Open an issue or reach out on LinkedIn.**
