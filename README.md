Question 1: Use yfinance to Extract Stock Data
Using the Ticker function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is TSLA.

tesla = yf.Ticker('TSLA')
Using the ticker object and the function history extract stock information and save it in a dataframe named tesla_data. Set the period parameter to max so we get information for the maximum amount of time.

tesla_data = tesla.history(periond="max")
Reset the index using the reset_index(inplace=True) function on the tesla_data DataFrame and display the first five rows of the tesla_data dataframe using the head function. Take a screenshot of the results and code from the beginning of Question 1 to the results below.

tesla_data.reset_index(inplace=True)
tesla_data.head(5)
Date	Open	High	Low	Close	Volume	Dividends	Stock Splits
0	2023-03-22	199.300003	200.660004	190.949997	191.149994	150376400	0	0
1	2023-03-23	195.259995	199.309998	188.649994	192.220001	144193900	0	0
2	2023-03-24	191.649994	192.360001	187.149994	190.410004	116531600	0	0
3	2023-03-27	194.419998	197.389999	189.940002	191.809998	120851600	0	0
4	2023-03-28	192.000000	192.350006	185.429993	189.190002	98654600	0	0
Question 2: Use Webscraping to Extract Tesla Revenue Data
Use the requests library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm Save the text of the response as a variable named html_data.

url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"
html_data = requests.get(url).text
Parse the html data using beautiful_soup.

soup = BeautifulSoup(html_data, "html.parser")
soup.find_all('title')
[<title>Tesla Revenue 2010-2023 | TSLA | MacroTrends</title>]
Using BeautifulSoup or the read_html function extract the table with Tesla Quarterly Revenue and store it into a dataframe named tesla_revenue. The dataframe should have columns Date and Revenue.

Click here if you need help locating the table

Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab

soup.find_all("tbody")[1]

If you want to use the read_html function the table is located at index 1


tesla_revenue = pd.DataFrame(columns = ["Date","Revenue"])

for table in soup.find_all('table'):
    if table.find('th').getText().startswith("Tesla Quarterly Revenue"):
        for row in table.find("tbody").find_all("tr"):
            col = row.find_all("td")
            if len(col) != 2: continue
            Date = col[0].text
            Revenue = col[1].text.replace("$","").replace(",","")
               
            tesla_revenue = tesla_revenue.append({"Date":Date, "Revenue":Revenue}, ignore_index=True)
Execute the following line to remove the comma and dollar sign from the Revenue column.

Execute the following lines to remove an null or empty strings in the Revenue column.

tesla_revenue.dropna(inplace=True)

tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
Display the last 5 row of the tesla_revenue dataframe using the tail function. Take a screenshot of the results.

tesla_revenue.tail(5)
Date	Revenue
50	2010-09-30	31
51	2010-06-30	28
52	2010-03-31	21
54	2009-09-30	46
55	2009-06-30	27
Question 3: Use yfinance to Extract Stock Data
Using the Ticker function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is GME.

gme = yf.Ticker('GME')
Using the ticker object and the function history extract stock information and save it in a dataframe named gme_data. Set the period parameter to max so we get information for the maximum amount of time.

gme_data = gme.history(period = "max")
Reset the index using the reset_index(inplace=True) function on the gme_data DataFrame and display the first five rows of the gme_data dataframe using the head function. Take a screenshot of the results and code from the beginning of Question 3 to the results below.

gme_data.reset_index(inplace=True)
gme_data.head(5)
Date	Open	High	Low	Close	Volume	Dividends	Stock Splits
0	2002-02-13	1.620128	1.693350	1.603296	1.691666	76216000	0.0	0.0
1	2002-02-14	1.712707	1.716073	1.670626	1.683250	11021600	0.0	0.0
2	2002-02-15	1.683250	1.687458	1.658002	1.674834	8389600	0.0	0.0
3	2002-02-19	1.666418	1.666418	1.578047	1.607504	7410400	0.0	0.0
4	2002-02-20	1.615920	1.662210	1.603296	1.662210	6892800	0.0	0.0
Question 4: Use Webscraping to Extract GME Revenue Data
Use the requests library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html. Save the text of the response as a variable named html_data.

url = "https://www.macrotrends.net/stocks/charts/GME/gamestop/revenue"
html_data = requests.get(url).text
Parse the html data using beautiful_soup.

soup = BeautifulSoup(html_data, "html.parser")
soup.find_all('title')
[<title>GameStop Revenue 2010-2023 | GME | MacroTrends</title>]
Using BeautifulSoup or the read_html function extract the table with GameStop Quarterly Revenue and store it into a dataframe named gme_revenue. The dataframe should have columns Date and Revenue. Make sure the comma and dollar sign is removed from the Revenue column using a method similar to what you did in Question 2.

Click here if you need help locating the table

Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab

soup.find_all("tbody")[1]

If you want to use the read_html function the table is located at index 1


gme_revenue = pd.DataFrame(columns = ["Date","Revenue"])

for table in soup.find_all('table'):
    if table.find('th').getText().startswith("GameStop Quarterly Revenue"):
        for row in table.find("tbody").find_all("tr"):
            col = row.find_all("td")
            if len(col) != 2: continue
            Date = col[0].text
            Revenue = col[1].text.replace("$","").replace(",","")
               
            gme_revenue = gme_revenue.append({"Date":Date, "Revenue":Revenue}, ignore_index=True)
Display the last five rows of the gme_revenue dataframe using the tail function. Take a screenshot of the results.

gme_revenue.tail(5)
Date	Revenue
52	2010-01-31	3524
53	2009-10-31	1835
54	2009-07-31	1739
55	2009-04-30	1981
56	2009-01-31	3492
Question 5: Plot Tesla Stock Graph
Use the make_graph function to graph the Tesla Stock Data, also provide a title for the graph. The structure to call the make_graph function is make_graph(tesla_data, tesla_revenue, 'Tesla'). Note the graph will only show data upto June 2021.

make_graph(tesla_data, tesla_revenue, 'Tesla')
Question 6: Plot GameStop Stock Graph
Use the make_graph function to graph the GameStop Stock Data, also provide a title for the graph. The structure to call the make_graph function is make_graph(gme_data, gme_revenue, 'GameStop'). Note the graph will only show data upto June 2021.

make_graph(gme_data, gme_revenue, 'GameStop')
