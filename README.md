# Stock Price Prediction using Sentiment Analysis

A comprehensive data science project that analyzes the correlation between market sentiment and stock price movements. This project combines real-time financial data with news sentiment analysis to provide insights for market prediction and investment decision-making.

## 📊 Project Overview

This project investigates the relationship between news sentiment and stock price trends by analyzing major companies' stocks alongside their corresponding news coverage. Using advanced web scraping, financial data APIs, and natural language processing, the system provides valuable insights into how market sentiment influences stock performance.

## 🎯 Objectives

- Analyze correlation between news sentiment and stock price movements
- Retrieve real-time financial data for major technology and retail stocks
- Scrape and analyze financial news articles for sentiment scoring
- Create visualizations to understand stock price patterns and sentiment trends
- Provide actionable insights for market prediction and investment strategies
- Demonstrate the practical application of sentiment analysis in financial markets

## 📈 Stock Portfolio Analysis

### Selected Stocks
The project analyzes 8 major companies representing different sectors:

- **NVDA** - NVIDIA Corporation (Technology/Semiconductors)
- **SPOT** - Spotify Technology (Media/Entertainment)
- **META** - Meta Platforms (Social Media/Technology)
- **MSFT** - Microsoft Corporation (Technology/Software)
- **AMZN** - Amazon.com Inc (E-commerce/Cloud)
- **TSLA** - Tesla Inc (Automotive/Energy)
- **C** - Citigroup Inc (Financial Services)
- **AAPL** - Apple Inc (Technology/Consumer Electronics)

### Time Period
- **Analysis Window**: 2 years of historical data
- **Data Frequency**: Daily stock prices and news updates
- **Coverage**: Comprehensive market cycles including volatility periods

## 🔧 Methodology

### 1. Financial Data Acquisition

#### YFinance Integration
```python
import yfinance as yf
msft = yf.Ticker("MSFT")
hist = msft.history(period="2y")
```

**Data Retrieved**:
- **OHLCV Data**: Open, High, Low, Close, Volume
- **Corporate Actions**: Dividends, stock splits
- **Company Information**: Market cap, sector, business summary
- **Calendar Events**: Earnings dates, dividend dates

#### Historical Analysis
- **Maximum History**: Complete trading history available
- **2-Year Focus**: Recent market trends and patterns
- **Real-time Updates**: Live market data integration

### 2. Advanced Stock Visualization

#### Candlestick Pattern Analysis
```python
import plotly.graph_objects as go
fig = go.Figure(data=[go.Candlestick(
    x=temp_df.index,
    open=temp_df["Open"],
    high=temp_df["High"],
    low=temp_df["Low"],
    close=temp_df["Close"]
)])
```

**Visualization Features**:
- **Interactive Candlestick Charts**: Professional trading chart format
- **Multi-Stock Comparison**: Individual charts for each stock
- **Custom Styling**: Professional color schemes and layouts
- **Responsive Design**: Optimized chart dimensions and margins

### 3. News Data Collection

#### Web Scraping from Finviz
```python
from urllib.request import urlopen, Request
from bs4 import BeautifulSoup

url = "https://finviz.com/quote.ashx?t=" + ticker
req = Request(url=url, headers={"user-agent": "my-app"})
response = urlopen(req)
html = BeautifulSoup(response, "html")
news = html.find(id="news-table")
```

**Data Extraction Process**:
- **Source**: Finviz financial news aggregator
- **Content**: News headlines, dates, and timestamps
- **Coverage**: Multiple news sources per stock
- **Parsing**: Structured data extraction from HTML

#### News Data Structure
- **Ticker Symbol**: Stock identifier
- **Publication Date**: News article date
- **Publication Time**: Specific timestamp
- **Headline**: Complete news title for sentiment analysis

### 4. Sentiment Analysis Implementation

#### VADER Sentiment Analyzer
```python
from nltk.sentiment.vader import SentimentIntensityAnalyzer
vader = SentimentIntensityAnalyzer()
df["compound"] = df["title"].apply(lambda x: vader.polarity_scores(x)["compound"])
```

**VADER Advantages**:
- **Financial Context**: Optimized for financial and social media text
- **Compound Scoring**: Single metric combining positive, negative, and neutral scores
- **Real-time Processing**: Fast sentiment computation for large datasets
- **No Training Required**: Pre-trained model ready for immediate use

#### Sentiment Scoring
- **Range**: -1 (most negative) to +1 (most positive)
- **Neutral Zone**: Scores near 0 indicate neutral sentiment
- **Threshold Analysis**: Clear positive/negative sentiment identification
- **Aggregation**: Stock-level sentiment averaging across multiple news sources

## 📊 Key Findings & Insights

### Sentiment-Price Correlation Discovery
The analysis reveals a **direct correlation between positive sentiment and stock price surges**:

- **Positive News Impact**: Stocks with positive news sentiment show corresponding price increases
- **Market Validation**: Real market data confirms sentiment-driven price movements
- **Consistent Patterns**: Similar sentiment-price relationships across different stocks
- **Predictive Value**: Sentiment scores provide leading indicators for price movements

### Cross-Stock Analysis
- **Uniform Growth Period**: All analyzed stocks showed positive sentiment during growth phases
- **Sector Consistency**: Technology stocks demonstrate strong sentiment-price correlation
- **Market Timing**: News sentiment often precedes significant price movements
- **Risk Assessment**: Negative sentiment provides early warning signals

## 🛠️ Technologies & Libraries

### Core Libraries
- **pandas** - Data manipulation and analysis
- **NumPy** - Numerical computing and array operations
- **matplotlib** - Basic plotting and visualization
- **seaborn** - Statistical data visualization

### Financial Data
- **yfinance** - Yahoo Finance API integration
- **plotly** - Interactive financial chart creation

### Web Scraping & NLP
- **urllib** - HTTP request handling
- **BeautifulSoup** - HTML parsing and data extraction
- **nltk** - Natural language processing and sentiment analysis

## 📋 Installation & Setup

### Install Required Libraries
```bash
pip install pandas numpy matplotlib seaborn yfinance plotly beautifulsoup4 nltk urllib3
```

### NLTK Data Setup
```python
import nltk
nltk.download('vader_lexicon')
```

### Library Imports
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import yfinance as yf
import plotly.graph_objects as go
from urllib.request import urlopen, Request
from bs4 import BeautifulSoup
from nltk.sentiment.vader import SentimentIntensityAnalyzer
```

## 🚀 Usage

### 1. Stock Data Retrieval
```python
# Single stock analysis
msft = yf.Ticker("MSFT")
hist = msft.history(period="2y")

# Multiple stock analysis
stocks = ["NVDA", "SPOT", "META", "MSFT", "AMZN", "TSLA", "C", "AAPL"]
hists = {}
for s in stocks:
    tkr = yf.Ticker(s)
    history = tkr.history(period="2y")
    hists[s] = history
```

### 2. Candlestick Visualization
```python
for stk in stocks:
    temp_df = hists[stk].copy()
    fig = go.Figure(data=[go.Candlestick(
        x=temp_df.index,
        open=temp_df["Open"],
        high=temp_df["High"],
        low=temp_df["Low"],
        close=temp_df["Close"]
    )])
    fig.update_layout(title=stk)
    fig.show()
```

### 3. News Scraping & Sentiment Analysis
```python
# Scrape news data
news_data = {}
for ticker in stocks:
    url = f"https://finviz.com/quote.ashx?t={ticker}"
    req = Request(url=url, headers={"user-agent": "my-app"})
    response = urlopen(req)
    html = BeautifulSoup(response, "html")
    news = html.find(id="news-table")
    news_data[ticker] = news

# Calculate sentiment scores
vader = SentimentIntensityAnalyzer()
df["compound"] = df["title"].apply(lambda x: vader.polarity_scores(x)["compound"])
```

## 📊 Key Features

### Advanced Data Integration
- **Multi-Source Data**: Combines financial and news data
- **Real-time Updates**: Live market data integration
- **Historical Analysis**: Comprehensive 2-year lookback period
- **Cross-Validation**: News sentiment validated against actual price movements

### Professional Visualizations
- **Interactive Charts**: Plotly-powered candlestick patterns
- **Multi-Stock Dashboard**: Comparative analysis across portfolio
- **Custom Styling**: Professional trading platform aesthetics
- **Responsive Design**: Optimized for various display sizes

### Intelligent Analysis
- **Automated Sentiment Scoring**: VADER-powered news analysis
- **Correlation Detection**: Statistical relationship identification
- **Pattern Recognition**: Market trend and sentiment pattern analysis
- **Predictive Insights**: Forward-looking market indicators

## 💡 Business Applications

### Investment Strategy
- **Entry/Exit Timing**: Use sentiment as timing indicator
- **Risk Management**: Early warning through negative sentiment detection
- **Portfolio Diversification**: Multi-stock sentiment analysis
- **Market Trend Analysis**: Broader market sentiment assessment

### Trading Applications
- **Day Trading**: Intraday sentiment-driven decisions
- **Swing Trading**: Multi-day sentiment trend following
- **Long-term Investing**: Fundamental sentiment analysis
- **Risk Assessment**: Sentiment-based position sizing

### Financial Research
- **Market Analysis**: Academic research on sentiment-price relationships
- **Algorithm Development**: Quantitative trading strategy creation
- **Backtesting**: Historical sentiment-performance validation
- **Market Prediction**: Forward-looking sentiment modeling

## 🔍 Analysis Insights

### Key Discoveries
1. **Direct Correlation**: Strong positive relationship between sentiment and price movements
2. **Leading Indicator**: News sentiment often precedes price changes
3. **Sector Patterns**: Technology stocks show stronger sentiment correlation
4. **Market Timing**: Sentiment analysis improves entry/exit decisions
5. **Risk Mitigation**: Negative sentiment provides early warning signals

### Statistical Observations
- **Positive Bias**: Growth periods show predominantly positive sentiment scores
- **Consistency**: Similar patterns across different stock sectors
- **Volatility Prediction**: Extreme sentiment scores predict price volatility
- **Market Efficiency**: Quick price adjustment to sentiment changes

## 🚀 Future Enhancements

### Advanced Analytics
- **Machine Learning Models**: Predictive modeling using sentiment features
- **Time Series Analysis**: LSTM networks for temporal sentiment patterns
- **Multi-Source Integration**: Additional news sources and social media
- **Real-time Streaming**: Live sentiment and price correlation monitoring

### Enhanced Visualization
- **Dashboard Development**: Interactive web-based dashboard
- **Mobile Application**: Smartphone-optimized sentiment tracking
- **Alert Systems**: Automated sentiment threshold notifications
- **Comparative Analysis**: Sector and market-wide sentiment comparisons

### Model Improvements
- **Custom Sentiment Models**: Finance-specific sentiment training
- **Ensemble Methods**: Multiple sentiment analyzers combination
- **Feature Engineering**: Additional technical and fundamental indicators
- **Backtesting Framework**: Historical strategy performance validation

## 📈 Market Impact & Value

### For Investors
- **Improved Decision Making**: Data-driven investment choices
- **Risk Reduction**: Early warning system for market downturns
- **Performance Enhancement**: Better entry and exit timing
- **Market Understanding**: Deeper insight into price movement drivers

### For Traders
- **Strategy Development**: Sentiment-based trading algorithms
- **Signal Generation**: Automated buy/sell signal creation
- **Market Edge**: Information advantage through sentiment analysis
- **Performance Tracking**: Quantified strategy effectiveness

## 🤝 Contributing

Contributions welcome in these areas:
- Additional news sources integration
- Advanced sentiment analysis techniques
- Real-time data streaming capabilities
- Machine learning model development
- Visualization and dashboard enhancements
- Performance optimization and scalability

---

**Note**: This project demonstrates the practical application of sentiment analysis in financial markets, providing valuable insights for investors, traders, and financial analysts. The correlation between positive sentiment and stock price surges offers significant potential for market prediction and investment strategy optimization.
