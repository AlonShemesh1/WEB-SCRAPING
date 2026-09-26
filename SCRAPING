import csv
from bs4 import BeautifulSoup
import requests

# Target URL
url = "https://books.toscrape.com/"

# Headers to mimic a real browser request
headers = {
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36"
}

# Send the HTTP GET request
response = requests.get(url, headers=headers)
response.encoding = "utf-8"

scraped_data = []

# Check if the request was successful
if response.status_code == 200:
    soup = BeautifulSoup(response.text, "html.parser")
    
    # Locate all book elements using CSS selectors
    books = soup.select("article.product_pod")
    
    print(f"🔍 Found {len(books)} elements on the page.")
    print("--- STARTING EXTRACTION ---")
    
    # Extract details for each book
    for book in books:
        title = book.h3.a["title"]
        price = book.select_one("p.price_color").get_text().strip()
        
        print(f"📖 Book Title: {title} | Price: {price}")
        scraped_data.append([title, price])
        
    # Save the extracted data into a CSV file
    with open("books_output.csv", "w", newline="", encoding="utf-8") as file:
        writer = csv.writer(file)
        writer.writerow(["Book Title", "Price"])
        writer.writerows(scraped_data)
        
    print(f"\n✅ SUCCESS! Saved {len(scraped_data)} books into books_output.csv.")
else:
    print(f"❌ Connection failed. Status code: {response.status_code}")
