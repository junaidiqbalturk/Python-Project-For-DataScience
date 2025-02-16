📌 Extracting Tesla & GameStop Stock and Revenue Data

📖 Overview

This project involves extracting stock and revenue data for Tesla (TSLA) and GameStop (GME) using Python. We utilize yfinance for stock data and web scraping (BeautifulSoup & pandas) for revenue data from Macrotrends.

🚀 Requirements

Ensure you have the required dependencies installed:

pip install yfinance pandas requests beautifulsoup4 matplotlib

📌 Questions & Solutions

✅ Question 1: Extracting Tesla Stock Data Using yfinance

Fetch Tesla (TSLA) historical and real-time stock data:

import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt

# Download Tesla stock data
tesla_stock = yf.download("TSLA", start="2023-08-01", end="2024-02-16")
print(tesla_stock.head())

📌 Real-time Stock Price:

tesla = yf.Ticker("TSLA")
print("Current Price:", tesla.history(period="1d")["Close"].iloc[-1])

📌 Save Data:

tesla_stock.to_csv("tesla_stock_data.csv")

📌 Plot Tesla Stock Price:

plt.plot(tesla_stock.index, tesla_stock["Close"], label="TSLA Closing Price", color="blue")
plt.xlabel("Date")
plt.ylabel("Price (USD)")
plt.title("Tesla Stock Price Over Time")
plt.legend()
plt.grid()
plt.show()

✅ Question 2: Extracting Tesla Revenue Data Using Web Scraping

We scrape Tesla's revenue data from Macrotrends:

import requests
import pandas as pd
from bs4 import BeautifulSoup

url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"
headers = {"User-Agent": "Mozilla/5.0"}
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

tables = pd.read_html(response.text)
for table in tables:
    if "Tesla Quarterly Revenue" in str(table):
        tesla_revenue = table
        break

tesla_revenue.columns = ["Date", "Revenue"]
tesla_revenue["Revenue"] = tesla_revenue["Revenue"].str.replace(",", "").str.replace("$", "")
tesla_revenue["Revenue"] = pd.to_numeric(tesla_revenue["Revenue"], errors="coerce")
print(tesla_revenue.head())

📌 Save Data:

tesla_revenue.to_csv("tesla_revenue_data.csv", index=False)

✅ Question 3: Extracting GameStop Stock Data Using yfinance

Fetch GameStop (GME) historical and real-time stock data:

# Download GameStop stock data
gamestop_stock = yf.download("GME", start="2023-08-01", end="2024-02-16")
print(gamestop_stock.head())

📌 Real-time Stock Price:

gamestop = yf.Ticker("GME")
print("Current Price:", gamestop.history(period="1d")["Close"].iloc[-1])

📌 Save Data:

gamestop_stock.to_csv("gamestop_stock_data.csv")

📌 Plot GameStop Stock Price:

plt.plot(gamestop_stock.index, gamestop_stock["Close"], label="GME Closing Price", color="red")
plt.xlabel("Date")
plt.ylabel("Price (USD)")
plt.title("GameStop Stock Price Over Time")
plt.legend()
plt.grid()
plt.show()

✅ Question 4: Extracting GameStop Revenue Data Using Web Scraping

We scrape GameStop's revenue data from Macrotrends:

url = "https://www.macrotrends.net/stocks/charts/GME/gamestop/revenue"
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

tables = pd.read_html(response.text)
for table in tables:
    if "GameStop Quarterly Revenue" in str(table):
        gamestop_revenue = table
        break

gamestop_revenue.columns = ["Date", "Revenue"]
gamestop_revenue["Revenue"] = gamestop_revenue["Revenue"].str.replace(",", "").str.replace("$", "")
gamestop_revenue["Revenue"] = pd.to_numeric(gamestop_revenue["Revenue"], errors="coerce")
print(gamestop_revenue.head())

📌 Save Data:

gamestop_revenue.to_csv("gamestop_revenue_data.csv", index=False)

📌 Additional Notes

yfinance is used to extract real-time and historical stock data.

BeautifulSoup and pandas are used for web scraping revenue data.

Macrotrends is the source for revenue data.

Data is saved as CSV files for further analysis.

📌 How to Run the Code

Clone the repository or download the script.

Install dependencies using pip install -r requirements.txt.

Run the Python scripts in order.

Analyze the extracted data in CSV files or visualize it using Matplotlib.

📌 License

This project is for educational purposes only. The data is extracted from publicly available sources.

🚀 Now you can analyze Tesla & GameStop stock and revenue data easily! 🚀
