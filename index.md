# Data Acquisition: Scraping and Analyzing S&P 500 Stock Performance

**Question:** How have S&P 500 companies performed over the past year, and which sectors led or lagged performance?

## Why this project
Stock performance is a compact, real-world example that combines web scraping, API usage, cleaning, and exploratory data analysis. The S&P 500 provides a consistent universe of firms (≈500 companies), which makes it ideal for teaching reproducible data collection and analysis while producing clear, interpretable visualizations.

## Data sources and ethics
I collected a list of S&P 500 constituents from **Wikipedia** (public, table-formatted) and used **Yahoo Finance** (via the `yfinance` Python library) to pull one-year historical price data. Both sources are publicly accessible, and I respected scraping etiquette by supplying a descriptive `User-Agent` header and limiting request frequency in my scripts. No private API keys were used.

## What I built
The final dataset links each S&P 500 ticker to:
- company name and sector (from Wikipedia)
- 1-year percent price change
- annualized volatility (std of daily returns, annualized)
- average annualized return (from daily returns)
- max drawdown over the year

Total sample: **~500 companies**, with multiple numeric and categorical variables suitable for EDA and basic ranking analysis.

## How others can get started
1. Use `pandas.read_html()` (with `requests.get()` and a sensible `User-Agent`) to pull the Wikipedia table of S&P 500 companies.  
2. Convert tickers that use dots (e.g., `BRK.B`) to Yahoo’s format (`BRK-B`).  
3. Use `yfinance.download()` to pull 1-year daily data for all tickers.  
4. Flatten the multi-index columns created by `yfinance` (e.g., produce `AAPL_Close`) or iterate per ticker.  
5. Compute metrics: percent change = (last close − first close) / first close; daily pct changes → volatility and average returns; max drawdown via `cummax()`.  
6. Merge metrics with the Wikipedia metadata and export as CSV for reproducibility.

(See the linked code repo for runnable Jupyter notebooks and the exact code used.)

## EDA highlights
- **Top performers:** The top decile of the S&P 500 contained names from technology and data-driven firms (example: *Robinhood, Palantir, Western Digital*).  
- **Sector averages:** On average, **Information Technology** and **Consumer Discretionary** produced the highest mean 1-year returns; defensive sectors such as **Utilities** lagged.  
- **Risk vs return:** Many of the largest 1-year winners also show high annualized volatility and large max drawdowns — indicating higher risk profiles.  
- **Distributions:** The 1-year returns distribution is right-skewed with heavy tails; volatility has a positive lower bound and a long upper tail.

(Include images: Top performers bar chart; Average 1Y return by sector bar chart; Histogram of metrics; Risk vs Return scatter.)

## Key findings (brief)
- Technology-oriented sectors dominated year-over-year returns, but at the cost of higher volatility.  
- Several mid-cap names produced outsized returns, which suggests concentrated winners rather than broad-based market gains.  
- Sector-level boxplots show large dispersion within sectors — sector average masks important company-level heterogeneity.

## Resources & links
- S&P 500 list (Wikipedia) — *List of S&P 500 companies*  
- Yahoo Finance docs / `yfinance` — *Python wrapper and documentation*  
- Code & data: **[Data & scripts repository]**(https://github.com/mitchster21/Data_Acquisition_Blog_SP500)

---

## Reproducibility
All code (scraping, cleaning, and EDA) is available in the linked GitHub repo as a Jupyter notebook. The notebook saves the final merged CSV so readers can reproduce the figures without long downloads.

---

**Author:** Mitchell Heaton — contact via GitHub
