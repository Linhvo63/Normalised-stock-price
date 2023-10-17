# Normalised-stock-price

import yfinance as yf

import plotly.express as px

stocks_list = ["AUTO.L", "RR.L", "SPX.L", "^FTSE"]

data = yf.download(stocks_list, period='5y')['Adj Close']

data.columns = ["AUTO.L","RR.L", "SPX.L","FTSE 100"]

def normalize_prices(df):

    df_ = df.copy()

    for stock in df_.columns:

        df_[stock] = df_[stock]/df_[stock][0]

    return df_

norm_df = normalize_prices(data)


fig = px.line(title = "Normalized stock prices")

for stock in norm_df.columns:

    fig.add_scatter(x = norm_df.index.values, y = norm_df[stock], name = stock)

fig.show()
