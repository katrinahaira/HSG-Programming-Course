# Objective of the code
# Of current S&P 500 stocks, we analyze which one performed best in April 2020, and some of their data, including min, max, mean price, standard deviation of closing prices, and percentage change in price. 
# We chose April 2020 as our target time period, because it is an interesting one to analyze since it was right at the beginning of the pandemic. 
# Some of the current stocks were not in the list back in April 2020, which is the reason for the errors regarding these companies when running the code.  

# We use import yfinance as yf to use the yfinance library, which allows us to access financial data from Yahoo Finance. This is essential for our analysis because it enables us to download historical data and calculate performance metrics. 

import yfinance as yf

# We use import matplotlib.pyplot as plt to take advantage of the matplotlib.pyplot library for creating visualizations.

import matplotlib.pyplot as plt

# We create a list of all current companies so that we can easily access and analyze the stock performance for each of these companies. This list allows us to download data and calculate the performance for all the companies we're interested in, helping us compare their performances and identify which one did the best during the specified period.

tickers = ['A',	'AAL',	'AAPL',	'ABBV',	'ABNB',	'ABT',	'ACGL',	'ACN',	'ADBE',	'ADI',	'ADM',	'ADP',	'ADSK',	'AEE',	'AEP',	'AES',	'AFL',	'AIG',	'AIZ',	'AJG',	'AKAM',	'ALB',	'ALGN',	'ALL',	'ALLE',	'AMAT',	'AMCR',	'AMD',	'AME',	'AMGN',	'AMP',	'AMT',	'AMZN',	'ANET',	'ANSS',	'AON',	'AOS',	'APA',	'APD',	'APH',	'APTV',	'ARE',	'ATO',	'AVB',	'AVGO',	'AVY',	'AWK',	'AXON',	'AXP',	'AZO',	'BA',	'BAC',	'BALL',	'BAX',	'BBWI',	'BBY',	'BDX',	'BEN',	'BF.B',	'BG',	'BIIB',	'BIO',	'BK',	'BKNG',	'BKR',	'BLDR',	'BLK',	'BMY',	'BR',	'BRK.B',	'BRO',	'BSX',	'BWA',	'BX',	'BXP',	'C',	'CAG',	'CAH',	'CARR',	'CAT',	'CB',	'CBOE',	'CBRE',	'CCI',	'CCL',	'CDNS',	'CDW',	'CE',	'CEG',	'CF',	'CFG',	'CHD',	'CHRW',	'CHTR',	'CI',	'CINF',	'CL',	'CLX',	'CMA',	'CMCSA',	'CME',	'CMG',	'CMI',	'CMS',	'CNC',	'CNP',	'COF',	'COO',	'COP',	'COR',	'COST',	'CPB',	'CPRT',	'CPT',	'CRL',	'CRM',	'CSCO',	'CSGP',	'CSX',	'CTAS',	'CTLT',	'CTRA',	'CTSH',	'CTVA',	'CVS',	'CVX',	'CZR',	'D',	'DAL',	'DAY',	'DD',	'DE',	'DECK',	'DFS',	'DG',	'DGX',	'DHI',	'DHR',	'DIS',	'DLR',	'DLTR',	'DOC',	'DOV',	'DOW',	'DPZ',	'DRI',	'DTE',	'DUK',	'DVA',	'DVN',	'DXCM',	'EA',	'EBAY',	'ECL',	'ED',	'EFX',	'EG',	'EIX',	'EL',	'ELV',	'EMN',	'EMR',	'ENPH',	'EOG',	'EPAM',	'EQIX',	'EQR',	'EQT',	'ES',	'ESS',	'ETN',	'ETR',	'ETSY',	'EVRG',	'EW',	'EXC',	'EXPD',	'EXPE',	'EXR',	'F',	'FANG',	'FAST',	'FCX',	'FDS',	'FDX',	'FE',	'FFIV',	'FI',	'FICO',	'FIS',	'FITB',	'FLT',	'FMC',	'FOX',	'FOXA',	'FRT',	'FSLR',	'FTNT',	'FTV',	'GD',	'GE',	'GEHC',	'GEN',	'GILD',	'GIS',	'GL',	'GLW',	'GM',	'GNRC',	'GOOG',	'GOOGL',	'GPC',	'GPN',	'GRMN',	'GS',	'GWW',	'HAL',	'HAS',	'HBAN',	'HCA',	'HD',	'HES',	'HIG',	'HII',	'HLT',	'HOLX',	'HON',	'HPE',	'HPQ',	'HRL',	'HSIC',	'HST',	'HSY',	'HUBB',	'HUM',	'HWM',	'IBM',	'ICE',	'IDXX',	'IEX',	'IFF',	'ILMN',	'INCY',	'INTC',	'INTU',	'INVH',	'IP',	'IPG',	'IQV',	'IR',	'IRM',	'ISRG',	'IT',	'ITW',	'IVZ',	'J',	'JBHT',	'JBL',	'JCI',	'JKHY',	'JNJ',	'JNPR',	'JPM',	'K',	'KDP',	'KEY',	'KEYS',	'KHC',	'KIM',	'KLAC',	'KMB',	'KMI',	'KMX',	'KO',	'KR',	'KVUE',	'L',	'LDOS',	'LEN',	'LH',	'LHX',	'LIN',	'LKQ',	'LLY',	'LMT',	'LNT',	'LOW',	'LRCX',	'LULU',	'LUV',	'LVS',	'LW',	'LYB',	'LYV',	'MA',	'MAA',	'MAR',	'MAS',	'MCD',	'MCHP',	'MCK',	'MCO',	'MDLZ',	'MDT',	'MET',	'META',	'MGM',	'MHK',	'MKC',	'MKTX',	'MLM',	'MMC',	'MMM',	'MNST',	'MO',	'MOH',	'MOS',	'MPC',	'MPWR',	'MRK',	'MRNA',	'MRO',	'MS',	'MSCI',	'MSFT',	'MSI',	'MTB',	'MTCH',	'MTD',	'MU',	'NCLH',	'NDAQ',	'NDSN',	'NEE',	'NEM',	'NFLX',	'NI',	'NKE',	'NOC',	'NOW',	'NRG',	'NSC',	'NTAP',	'NTRS',	'NUE',	'NVDA',	'NVR',	'NWS',	'NWSA',	'NXPI',	'O',	'ODFL',	'OKE',	'OMC',	'ON',	'ORCL',	'ORLY',	'OTIS',	'OXY',	'PANW',	'PARA',	'PAYC',	'PAYX',	'PCAR',	'PCG',	'PEG',	'PEP',	'PFE',	'PFG',	'PG',	'PGR',	'PH',	'PHM',	'PKG',	'PLD',	'PM',	'PNC',	'PNR',	'PNW',	'PODD',	'POOL',	'PPG',	'PPL',	'PRU',	'PSA',	'PSX',	'PTC',	'PWR',	'PXD',	'PYPL',	'QCOM',	'QRVO',	'RCL',	'REG',	'REGN',	'RF',	'RHI',	'RJF',	'RL',	'RMD',	'ROK',	'ROL',	'ROP',	'ROST',	'RSG',	'RTX',	'RVTY',	'SBAC',	'SBUX',	'SCHW',	'SHW',	'SJM',	'SLB',	'SMCI',	'SNA',	'SNPS',	'SO',	'SPG',	'SPGI',	'SRE',	'STE',	'STLD',	'STT',	'STX',	'STZ',	'SWK',	'SWKS',	'SYF',	'SYK',	'SYY',	'T',	'TAP',	'TDG',	'TDY',	'TECH',	'TEL',	'TER',	'TFC',	'TFX',	'TGT',	'TJX',	'TMO',	'TMUS',	'TPR',	'TRGP',	'TRMB',	'TROW',	'TRV',	'TSCO',	'TSLA',	'TSN',	'TT',	'TTWO',	'TXN',	'TXT',	'TYL',	'UAL',	'UBER',	'UDR',	'UHS',	'ULTA',	'UNH',	'UNP',	'UPS',	'URI',	'USB',	'V',	'VFC',	'VICI',	'VLO',	'VLTO',	'VMC',	'VRSK',	'VRSN',	'VRTX',	'VTR',	'VTRS',	'VZ',	'WAB',	'WAT',	'WBA',	'WBD',	'WDC',	'WEC',	'WELL',	'WFC',	'WM',	'WMB',	'WMT',	'WRB',	'WRK',	'WST',	'WTW',	'WY',	'WYNN',	'XEL',	'XOM',	'XRAY',	'XYL',	'YUM',	'ZBH',	'ZBRA',	'ZTS']  

# Defining the time period (April 2020) – we are interested in this specific time period and, therefore, it is important to clearly define the time period

start_date = '2020-04-01'
end_date = '2020-04-30'

# We use the function fetch_performance(ticker) to easily get stock price data and calculate how much a stock's price has changed over a specific period. The function downloads the stock's price data, checks if the data is available, and then calculates the performance by comparing the closing prices on the first and last days of the period. It returns the performance as a percentage change and the data itself.

def fetch_performance(ticker):
    data = yf.download(ticker, start=start_date, end=end_date)
    if not data.empty:
        first_close = data.iloc[0]['Close']
        last_close = data.iloc[-1]['Close']
        return last_close / first_close - 1, data
    else:
        return None, None


# We initialize an empty dictionary performance_dict to store the performance data (percentage change) and associated historical data for each ticker.

performance_dict = {}


# We then loop through each ticker, fetch the performance for each ticker using fetch_performance, and store the results in the dictionary.

for ticker in tickers:
    change, data = fetch_performance(ticker)
    if change is not None:
        performance_dict[ticker] = (change, data)


# To indentify the best performing stock, we identify the ticker with the maximum percentage change. This is done using the max function, which returns the ticker with the highest performance.

best_stock = max(performance_dict, key=lambda x: performance_dict[x][0])
best_data = performance_dict[best_stock][1]


#  We then calculate key statistics for the best performing stock, including the minimum, maximum, mean closing prices, and the standard deviation of closing prices.

min_price = best_data['Close'].min()
max_price = best_data['Close'].max()
mean_price = best_data['Close'].mean()
std_dev = best_data['Close'].std()

 
# Plotting the closing prices for the best performing stock
plt.figure(figsize=(10, 5))  # Set the size of the plot
 
# Plot the 'Close' column from best_data with circles at data points and a line connecting them
plt.plot(best_data['Close'], marker='o', linestyle='-')
 
# Set the title of the plot with the stock name and the date range
plt.title(f'{best_stock}: April 2020 Closing Prices')
 
# Label the x-axis as 'Date'
plt.xlabel('Date')
 
# Label the y-axis as 'Closing Price (USD)'
plt.ylabel('Closing Price (USD)')
 
# Add a grid to the plot for better readability
plt.grid(True)
 
# Rotate the x-axis labels by 45 degrees for better readability
plt.xticks(rotation=45)
 
# Adjust the layout to make room for the rotated x-axis labels
plt.tight_layout()
 
# Display the plot
plt.show()
 
# Printing the statistics for the best performing stock
print(f"Statistics for {best_stock} from April 1, 2020 to April 30, 2020:")
 
# Print the minimum closing price with two decimal places
print(f"Minimum Closing Price: ${min_price:.2f}")
 
# Print the maximum closing price with two decimal places
print(f"Maximum Closing Price: ${max_price:.2f}")
 
# Print the mean (average) closing price with two decimal places
print(f"Mean Closing Price: ${mean_price:.2f}")
 
# Print the standard deviation of the closing prices with two decimal places
print(f"Standard Deviation of Closing Prices: ${std_dev:.2f}")
 
# Print the percentage change in the stock's performance with two decimal places
print(f"Percentage Change (Performance): {performance_dict[best_stock][0] * 100:.2f}%")


# The code and analysis help us figure out which stocks did well during an important time. By using Python and its useful tools, we can get valuable information and make easy-to-understand charts. This way, we can see which stock performed the best and have a good method for analyzing stock performance during unpredictable times.
