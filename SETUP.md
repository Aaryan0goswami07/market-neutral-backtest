# Setup Instructions

## Quick Setup (5 minutes)

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/market-neutral-backtest.git
cd market-neutral-backtest
```

### Step 2: Create Virtual Environment (Recommended)

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**Mac/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Run the Application

```bash
streamlit run app.py
```

The app will open automatically in your browser at `http://localhost:8501`

## Troubleshooting

### Issue: `streamlit: command not found`

**Solution:**
```bash
python -m streamlit run app.py
```

### Issue: Module import errors

**Solution:**
```bash
pip install --upgrade -r requirements.txt
```

### Issue: yfinance data fetch errors

**Solution:**
- Check your internet connection
- Try a different ticker pair
- yfinance occasionally has rate limits; wait a few minutes and retry

### Issue: Port 8501 already in use

**Solution:**
```bash
streamlit run app.py --server.port 8502
```

## Development Setup

For development work:

```bash
# Install development dependencies
pip install pytest pytest-cov black flake8

# Run tests
pytest tests/

# Check code style
black backtest/
flake8 backtest/

# Run with debug mode
streamlit run app.py --logger.level=debug
```

## Configuration

### Custom Settings

Create a `.streamlit/config.toml` file:

```toml
[theme]
primaryColor = "#00d4ff"
backgroundColor = "#0e1117"
secondaryBackgroundColor = "#262730"
textColor = "#fafafa"

[server]
port = 8501
enableCORS = false
```

### Environment Variables

Create a `.env` file (optional):

```
DATA_SOURCE=yfinance
CACHE_TTL=3600
DEFAULT_BENCHMARK=SPY
```

## Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=backtest tests/

# Run specific test file
pytest tests/test_backtest.py

# Verbose output
pytest -v
```

## Building Documentation

```bash
# Install docs dependencies
pip install sphinx sphinx-rtd-theme

# Build docs
cd docs
make html

# View docs
open _build/html/index.html
```

## Deployment

### Streamlit Cloud

1. Push code to GitHub
2. Go to [share.streamlit.io](https://share.streamlit.io)
3. Connect your repo
4. Deploy!

### Local Production

```bash
# Install production server
pip install gunicorn

# Run with gunicorn (example)
gunicorn app:app --workers 4 --bind 0.0.0.0:8000
```

## Need Help?

- Check [README.md](README.md) for usage examples
- See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines
- Open an issue on GitHub
- Reach out on LinkedIn

---

**You're all set! Start backtesting! 🚀**
