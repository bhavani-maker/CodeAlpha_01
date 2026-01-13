import requests
from bs4 import BeautifulSoup
import pandas as pd

# Website URL
url = "https://quotes.toscrape.com"

# Request the webpage
response = requests.get(url)

# Parse HTML
soup = BeautifulSoup(response.text, "html.parser")

# Find data
quotes = soup.find_all("span", class_="text")
authors = soup.find_all("small", class_="author")

data = []

for quote, author in zip(quotes, authors):
    data.append({
        "Quote": quote.text,
        "Author": author.text
    })

# Create CSV
df = pd.DataFrame(data)
df.to_csv("quotes_dataset.csv", index=False)

print("Web scraping completed successfully!")