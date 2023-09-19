# Projeto de Análise de Dados de Ações

Este repositório contém o código e os resultados de uma análise de dados de ações usando Python, incluindo a extração de dados de ações da Tesla e GameStop, bem como a criação de gráficos relevantes. Os detalhes da análise são fornecidos nas seções a seguir.

## Question 1: Extrair Dados de Ações da Tesla

```python
# Use yfinance para Extrair Dados de Ações da Tesla
tesla = yf.Ticker('TSLA')
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)
tesla_data.head(5)
Tesla Stock Data

Question 2: Extrair Dados de Receita da Tesla (Web Scraping)

# Use Web Scraping para Extrair Dados de Receita da Tesla
url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, "html.parser")

# Código para extrair a tabela de receita
tesla_revenue = pd.DataFrame(columns=["Date", "Revenue"])
# ...
tesla_revenue.tail(5)
Tesla Revenue Data

Question 3: Extrair Dados de Ações da GameStop

# Use yfinance para Extrair Dados de Ações da GameStop
gme = yf.Ticker('GME')
gme_data = gme.history(period="max")
gme_data.reset_index(inplace=True)
gme_data.head(5)
GameStop Stock Data

Question 4: Extrair Dados de Receita da GameStop (Web Scraping)


# Use Web Scraping para Extrair Dados de Receita da GameStop
url = "https://www.macrotrends.net/stocks/charts/GME/gamestop/revenue"
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, "html.parser")

# Código para extrair a tabela de receita
gme_revenue = pd.DataFrame(columns=["Date", "Revenue"])
# ...
gme_revenue.tail(5)
GameStop Revenue Data

Question 5: Gráfico de Ações da Tesla


# Gráfico de Ações da Tesla
make_graph(tesla_data, tesla_revenue, 'Tesla')
Question 6: Gráfico de Ações da GameStop
python
Copy code
# Gráfico de Ações da GameStop
make_graph(gme_data, gme_revenue, 'GameStop')






