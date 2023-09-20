![image.jpg](h)

## Project Overview:
Welcome to my web scraping project that extracts data from the [List of Largest Companies in the United States by Revenue](https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue). The project utilizes Python, the Beautiful Soup library for web scraping, and the Pandas library for data manipulation. The scraped data is then saved to a CSV file.

The primary goal of this project is to demonstrate how web scraping can be used to gather valuable information from websites and present it in a structured format.

##Web scrapping using beautifulsoup


***Import  libraries***
```python
from bs4 import BeautifulSoup
import requests
***URL of the website***
```python
url = "https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue"

***Sending a Get request and parsing the output in html format***
```python
page = requests.get (url)
soup = BeautifulSoup(page.text, 'html')

***Locating  the Table***
```python
table = soup.find('table', class_ = 'wikitable sortable') 
table
***Extract Data from the Table***
```python
row = soup.find_all('table')[1]
row


***Extract Headers from Table***
```python
world_titles = table.find_all('th')

world_table_titles = [title.text.strip() for title in world_titles]
print (world_table_titles)


***Create a Pandas DataFrame***
```python
df = pd.DataFrame (columns = world_table_titles)
***Extract Data from Rows***
```python
column=table.find_all('tr')

for row in column[1:]:
    row_data=row.find_all("td")
    indiviual=[data.text.strip() for data in row_data]


    length=len(df)
    df.loc[length]=indiviual

***Displaying Dataframe***
```python
df

***Saving data to csv***
```python
df.to_csv("top_companies.csv",index=False)




