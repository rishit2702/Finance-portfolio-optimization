# Finance Portfolio Optimization

## Overview
This project implements a sophisticated machine learning-based portfolio optimization system specifically designed for the Indian stock market. It leverages advanced algorithms to analyze historical stock data, generate optimal portfolio weights, and provide comprehensive performance analytics. The system combines traditional financial metrics with modern machine learning techniques to create robust investment strategies tailored to the Indian market context.

## Features

### 1. Data Collection & Processing
#### Market Data Integration
- Automated data fetching from Yahoo Finance API
- Support for all major Indian stocks and indices (NSE/BSE)
- Real-time price updates during market hours
- Historical data with adjustments for corporate actions

#### Data Quality Management
- Automated detection and handling of missing values
- Outlier detection and treatment
- Data normalization and standardization
- Time series alignment and synchronization

### 2. Technical Analysis Engine
#### Price-Based Indicators
- Simple Moving Averages (20, 50, 200 days)
- Exponential Moving Averages
- Bollinger Bands with customizable parameters
- MACD (Moving Average Convergence Divergence)

#### Volume Analysis
- Volume Weighted Average Price (VWAP)
- On-Balance Volume (OBV)
- Volume Profile analysis
- Accumulation/Distribution indicators

#### Momentum Indicators
- Relative Strength Index (RSI)
- Stochastic Oscillator
- Money Flow Index (MFI)
- Rate of Change (ROC)

### 3. Portfolio Optimization
#### Machine Learning Models
- LightGBM-based return prediction
- Risk factor modeling using principal component analysis
- Correlation-based clustering for diversification
- Adaptive weight optimization

#### Risk Management
- Dynamic position sizing based on volatility
- Maximum position limits (30% per stock)
- Minimum position requirements (5% threshold)
- Sector exposure controls
- Stop-loss implementation with trailing mechanisms

#### Optimization Constraints
- Transaction cost consideration
- Liquidity-based position limits
- Sector-wise allocation limits
- Risk budget allocation

### 4. Performance Analytics
#### Return Metrics
- Absolute returns (daily, monthly, annual)
- Risk-adjusted returns (Sharpe, Sortino ratios)
- Alpha generation vs benchmark
- Rolling returns analysis

#### Risk Metrics
- Value at Risk (VaR) calculation
- Expected Shortfall (ES)
- Maximum drawdown analysis
- Beta calculation vs NIFTY 50

#### Portfolio Analysis
- Attribution analysis
- Factor exposure analysis
- Stress testing
- Scenario analysis

## Requirements

### Software Dependencies
```
numpy>=1.19.2
pandas>=1.2.0
yfinance>=0.1.63
scikit-learn>=0.24.0
lightgbm>=3.2.1
matplotlib>=3.3.3
seaborn>=0.11.1
scipy>=1.6.0
statsmodels>=0.12.0
```

### System Requirements
- Python 3.8 or higher
- Minimum 4GB RAM (8GB recommended)
- Stable internet connection for real-time data
- 50GB storage for historical data

## Installation

### 1. Environment Setup
```bash
# Create and activate virtual environment
python -m venv portfolio_env
source portfolio_env/bin/activate  # Linux/Mac
portfolio_env\Scripts\activate     # Windows
```

### 2. Package Installation
```bash
# Install required packages
pip install -r requirements.txt

# Install additional development dependencies
pip install -r requirements-dev.txt
```

### 3. Configuration Setup
```bash
# Copy example configuration
cp config.example.yml config.yml

# Edit configuration with your parameters
nano config.yml
```

## Usage

### 1. Basic Implementation
```python
from portfolio_optimization import MarketData, PortfolioOptimizer

# Initialize data collector with custom configuration
market_data = MarketData(
    symbols=['RELIANCE.NS', 'TCS.NS', 'HDFCBANK.NS'],
    start_date='2020-01-01',
    end_date='2025-02-09'
)

# Fetch and process market data
data = market_data.fetch()
processed_data = market_data.process()

# Create and train optimizer
optimizer = PortfolioOptimizer(
    risk_tolerance=0.5,
    max_position=0.3,
    min_position=0.05
)

# Generate optimal weights
weights = optimizer.optimize(processed_data)
```

### 2. Advanced Usage with Risk Management
```python
from portfolio_optimization import RiskManager, PerformanceAnalytics

# Initialize risk manager
risk_manager = RiskManager(
    stop_loss_threshold=0.1,
    trailing_stop=0.05,
    vol_target=0.15
)

# Apply risk overlays
managed_weights = risk_manager.apply_constraints(weights)

# Analyze performance
analytics = PerformanceAnalytics(portfolio_data)
metrics = analytics.calculate_metrics()
```

### 3. Real-time Monitoring
```python
from portfolio_optimization import PortfolioDashboard

# Initialize dashboard
dashboard = PortfolioDashboard(
    refresh_interval=60,
    metrics=['returns', 'volatility', 'sharpe_ratio']
)

# Start monitoring
dashboard.run()
```

## Configuration Options

### Market Data Settings
```python
CONFIG = {
    'start_date': '2020-01-01',
    'end_date': '2025-02-09',
    'symbols': ['RELIANCE.NS', 'TCS.NS', 'HDFCBANK.NS'],
    'market_index': '^NSEI',
    'lookback_period': 252,
    'data_frequency': 'daily'
}
```

### Optimization Parameters
```python
OPTIMIZATION_CONFIG = {
    'risk_tolerance': 0.5,
    'max_position': 0.3,
    'min_position': 0.05,
    'sector_limits': {
        'Technology': 0.4,
        'Financial': 0.4,
        'Energy': 0.3
    },
    'rebalance_frequency': 'monthly'
}
```

## Performance Metrics Tracked

### Return Metrics
- Daily/Monthly/Annual Returns
- Cumulative Returns
- Rolling Returns (various windows)
- Excess Returns vs Benchmark

### Risk Metrics
- Standard Deviation
- Downside Deviation
- Beta
- Value at Risk (95%, 99%)
- Maximum Drawdown
- Recovery Time

### Risk-Adjusted Metrics
- Sharpe Ratio
- Sortino Ratio
- Information Ratio
- Treynor Ratio
- Jensen's Alpha

## Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/EnhancedRiskMetrics`)
3. Commit your changes (`git commit -m 'Add enhanced risk metrics calculation'`)
4. Push to the branch (`git push origin feature/EnhancedRiskMetrics`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guide
- Add unit tests for new features
- Update documentation accordingly
- Maintain backward compatibility

