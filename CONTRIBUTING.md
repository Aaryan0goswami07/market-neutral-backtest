# Contributing to Market Neutral Backtest Framework

First off, thank you for considering contributing to this project! 🎉

## How Can I Contribute?

### Reporting Bugs

If you find a bug, please open an issue with:

- **Clear title** describing the problem
- **Steps to reproduce** the behavior
- **Expected behavior** vs actual behavior
- **Screenshots** if applicable
- **Environment details** (Python version, OS, etc.)

### Suggesting Enhancements

Enhancement suggestions are welcome! Please open an issue with:

- **Clear description** of the enhancement
- **Use case** - why would this be useful?
- **Possible implementation** (if you have ideas)

### Pull Requests

1. **Fork the repo** and create your branch from `main`
2. **Make your changes** and add tests if applicable
3. **Ensure tests pass** (`pytest tests/`)
4. **Update documentation** if needed
5. **Write clear commit messages**
6. **Submit a pull request**

## Development Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/market-neutral-backtest.git
cd market-neutral-backtest

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install pytest pytest-cov black flake8

# Run tests
pytest tests/
```

## Code Style

- Follow **PEP 8** style guide
- Use **type hints** where appropriate
- Write **docstrings** for functions and classes
- Keep functions **focused** and **testable**

```python
def calculate_zscore(ratio: pd.Series, window: int = 60) -> pd.Series:
    """
    Calculate Z-score for price ratio.
    
    Parameters
    ----------
    ratio : pd.Series
        Price ratio between two assets
    window : int, default 60
        Rolling window for mean/std calculation
    
    Returns
    -------
    pd.Series
        Z-score time series
    """
    rolling_mean = ratio.rolling(window=window).mean()
    rolling_std = ratio.rolling(window=window).std()
    return (ratio - rolling_mean) / rolling_std
```

## Testing

- Write tests for new features
- Aim for >80% code coverage
- Test edge cases

```python
def test_zscore_calculation():
    ratio = pd.Series([1.0, 1.1, 1.2, 0.9, 1.0])
    zscore = calculate_zscore(ratio, window=3)
    assert not zscore.isna().all()
```

## Areas We'd Love Help With

- [ ] Regime detection algorithms
- [ ] Machine learning signal enhancement
- [ ] Additional asset classes (futures, options)
- [ ] Performance optimizations
- [ ] Documentation improvements
- [ ] Test coverage expansion

## Questions?

Feel free to open an issue or reach out on LinkedIn!

Thank you for contributing! 🚀
