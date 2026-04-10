# Data Availability and Replication Instructions

Due to strict licensing agreements and copyright restrictions, the raw proprietary financial data utilized in this thesis cannot be shared publicly in this repository. 

To fully replicate the empirical analysis and execute the `Thesis_Implementation.ipynb` notebook, researchers must independently acquire and place the following datasets in this `data/` directory:

### 1. Asset Returns Data (FactSet)
Monthly Total Return and Price Return series for the five analyzed asset classes were originally extracted from **FactSet**. For researchers with active FactSet access, the exact indices and tickers used in this study are listed below:

| Asset Class | Index Description | FactSet Ticker |
| :--- | :--- | :--- |
| **US Equity** | S&P 500 Total Return Index | `SP50` |
| **Fixed Income** | ICE BofA US Treasury 7-10 Year Total Return Index | `MLG4O2` |
| **Commodities** | S&P Goldman Sachs Commodity Index (GSCI) Total Return | `SPGSCI` |
| **Gold** | LBMA Gold Price (Spot) | `GOLD-FDS` |
| **Real Estate** | FTSE NAREIT All Equity REITs Total Return Index | `FNER` |

*Note: Researchers without FactSet access can reconstruct proxy series using standard OHLCV data from alternative financial data providers (e.g., Bloomberg, Refinitiv, or Yahoo Finance).*

### 2. Macroeconomic Predictors (Goyal-Welch-Zafirov)
The 37 macroeconomic variables (GWZ 2023) are maintained and updated by Amit Goyal and Ivo Welch.
* **Source:** Welch, Ivo, and Amit Goyal. "A Comprehensive Look at The Empirical Performance of Equity Premium Prediction."
* **Direct Access (Updated Spreadsheet):** [GWZ Data on Google Sheets](https://docs.google.com/spreadsheets/d/10_nkOkJPvq4eZgNl-1ys63PzhbnM3S2y/edit?pli=1&gid=1060486139#gid=1060486139)

### 3. Fama-French Risk Factors
The Fama-French 3-Factor model datasets (Mkt-RF, SMB, HML, and the Risk-Free rate) are publicly available via the Dartmouth Data Library.
* **Source:** Kenneth R. French Data Library.
* **Download Page:** [French Data Library - Current Research Returns](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)
* **Specific File Needed:** `F-F_Research_Data_Factors.csv` (Monthly version).

**Note on Code Execution:** Before running the pipeline in `Thesis_Implementation.ipynb`, ensure all CSV files are correctly named and formatted as expected by the "Data Import" block. Specifically, the notebook expects the predictors and factors to be aligned chronologically with the month-end convention.
