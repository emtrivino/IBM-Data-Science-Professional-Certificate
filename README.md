# Creating the Jupyter notebook file with the provided code
import nbformat as nbf

# Define the code for each cell in the notebook
code_cells = [
    """import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt

def make_graph(stock_data, revenue_data, stock_name):
    fig, ax1 = plt.subplots(figsize=(14, 8))
    
    ax1.set_xlabel('Date')
    ax1.set_ylabel('Stock Price', color='tab:blue')
    ax1.plot(stock_data['Date'], stock_data['Close'], color='tab:blue', label=f'{stock_name} Stock Price')
    ax1.tick_params(axis='y', labelcolor='tab:blue')
    
    ax2 = ax1.twinx()
    ax2.set_ylabel('Revenue', color='tab:green')
    ax2.plot(revenue_data['Date'], revenue_data['Revenue'], color='tab:green', label=f'{stock_name} Revenue')
    ax2.tick_params(axis='y', labelcolor='tab:green')
    
    fig.tight_layout()
    plt.title(f'{stock_name} Stock Price and Revenue')
    plt.show()

# Pregunta 1: Extracción de datos de acciones de Tesla usando yfinance
tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)
print(tesla_data.head())

# Pregunta 2: Extracción de datos de ingresos de Tesla usando web scraping
url_tesla = "https://example.com/tesla-revenue"
tesla_revenue = pd.read_html(url_tesla)[0]
tesla_revenue.columns = ['Date', 'Revenue']
tesla_revenue.dropna(inplace=True)
tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
print(tesla_revenue.tail())

# Pregunta 3: Extracción de datos de acciones de GameStop usando yfinance
gme = yf.Ticker("GME")
gme_data = gme.history(period="max")
gme_data.reset_index(inplace=True)
print(gme_data.head())

# Pregunta 4: Extracción de datos de ingresos de GameStop usando web scraping
url_gme = "https://example.com/gme-revenue"
gme_revenue = pd.read_html(url_gme)[0]
gme_revenue.columns = ['Date', 'Revenue']
gme_revenue.dropna(inplace=True)
gme_revenue = gme_revenue[gme_revenue['Revenue'] != ""]
print(gme_revenue.tail())

# Pregunta 5: Gráfica de acciones e ingresos de Tesla
make_graph(tesla_data, tesla_revenue, 'Tesla')

# Pregunta 6: Gráfica de acciones e ingresos de GameStop
make_graph(gme_data, gme_revenue, 'GameStop')"""
]

# Create a new Jupyter notebook
nb = nbf.v4.new_notebook()

# Add code cells to the notebook
for code in code_cells:
    nb.cells.append(nbf.v4.new_code_cell(code))

# Define the path for the notebook
notebook_path = '/mnt/data/stock_revenue_analysis.ipynb'

# Write the notebook to a file
with open(notebook_path, 'w') as f:
    nbf.write(nb, f)

notebook_path
