# Accounting Data from Yahoo Finance
Calculating various ratios using yahoo finance data

## **yfinance** libaray

Although there are various professional databases including Compustate offered by S&P for accounting and finance professionals to use, but sometimes one can find they are expensive and a bit too heavy to use.

In this case, you can easily use free libaray, **yfinance** to extract accounting data from publicly available *Yahoo Finance* website.

By extracting financial statements from Yahoo Finance, you can calculate various accounting ratios from simple PER, PBR to more complex statistics such as Ohlson O-score (1980) or Beneish M-score (1999).

In this article, I would like to share a simple way to do this and a few examples.

## Financial Statements from **Yahoo Finance**

```python
#yahoo finance library
import yfinance as yf

#input: ticker string
#output: financial statements

def get_financial_data(ticker):
    stock = yf.Ticker(ticker)
    financials = stock.financials.T
    balance_sheet = stock.balance_sheet.T
    cashflow = stock.cashflow.T
    return financials, balance_sheet, cashflow
```

This is it.\
Using the function, `get_financial_data`, various financial statements can be extracted from Yahoo Finance. 

1. financials: income statement
2. balance_sheet: balance sheet
3. cashflow: statement of cash flow

Let's see how they are displayed.

```python
ic_AAPL, bs_AAPL, cf_AAPL = get_financial_data("AAPL")
```

#### Balance Sheet

![schematics](Images/bs_eg.png)

#### Income Statement

![schematics](Images/ic_eg.png)

#### Statement of Cash Flow

![schematics](Images/cf_eg.png)

#### (Ex) when only a certain account is required

```python
#example: EBITDA
bs_AAPL.get("EBITDA")
```

![schematics](Images/bs_ebitda_eg.png)


## Example: More complex cases

Ok. Now we now how to extract both 1. a whole financial statement and 2. a certain account.

We can use this to calculate more complex statistics. 

I took two examples - Ohlson O score and Beneish M score - to show you this.



