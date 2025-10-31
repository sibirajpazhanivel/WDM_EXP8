### EX8 Web Scraping On E-commerce platform using BeautifulSoup
##### DATE: 17-10-2025
##### NAME : SIBIRAJ P
##### REGISTER NUMBER : 212222220046
### AIM: 
To perform Web Scraping using (beautifulsoup) Python.
### Description: 
<div align = "justify">
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique 
to extract unstructured data and store that data either in a local file or in a database. 
There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. 
One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
<p>The basic steps involved in web scraping are:
<p>1) Loading the document (HTML content)
<p>2) Parsing the document
<p>3) Extraction
<p>4) Transformation

### Procedure:

1) Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
2) Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
3) Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
4) Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
5) Return sorted product data as a list of dictionaries.
6) Call get_amazon_products(search_query) to get product data based on the user's search query.
7) Check if products are found; if not, display "No products found."
8) Visualize Product Data using a Bar Chart

### Program:
```PYTHON
import requests
from bs4 import BeautifulSoup
import time
search_query = input("Enter the product to search on Snapdeal: ").strip()
num_pages = 2  
base_url = "https://www.snapdeal.com/search"
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"}

product_list = []

for page in range(1, num_pages + 1):
    print(f"\nScraping page {page} for '{search_query}'...")
    params = {"keyword": search_query, "page": page}
    response = requests.get(base_url, params=params, headers=headers)
    soup = BeautifulSoup(response.text, "html.parser")

    products = soup.find_all("div", class_="product-tuple-listing")

    for product in products:
        title = product.find("p", class_="product-title").text.strip() if product.find("p", class_="product-title") else "N/A"
        price = product.find("span", class_="product-price").text.strip() if product.find("span", class_="product-price") else "N/A"
        discount = product.find("div", class_="product-discount").text.strip() if product.find("div", class_="product-discount") else "N/A"
        rating_tag = product.find("div", class_="filled-stars")
        if rating_tag:
            rating_style = rating_tag.get("style", "")
            try:
                percent = float(rating_style.replace("width:", "").replace("%", "").replace(";", "").strip())
                rating_value = round(percent / 20, 1)  
            except ValueError:
                rating_value = "N/A"
        else:
            rating_value = "N/A"

        product_list.append({
            "Title": title,
            "Price": price,
            "Discount": discount,
            "Rating": rating_value
        })
    
    time.sleep(1)
if not product_list:
    print("\nNo products found. Try another search term.")
else:
    print(f"\nFound {len(product_list)} products for '{search_query}'\n")
    
    for i, item in enumerate(product_list, 1):
        print(f"{i}. Title: {item['Title']}")
        print(f"   Price: {item['Price']}")
        print(f"   Discount: {item['Discount']}")
        print(f"   Rating: {item['Rating']}")
        print("-" * 60)
```

### Output:

<img width="1346" height="765" alt="image" src="https://github.com/user-attachments/assets/bb34eabe-1f4c-40f4-9387-2d630c3d49aa" />

<img width="1320" height="772" alt="image" src="https://github.com/user-attachments/assets/75e462d8-d1fd-4317-aa2a-b523681ccfa1" />

<img width="1329" height="756" alt="image" src="https://github.com/user-attachments/assets/211349bd-c946-4f87-9da6-67975aeba6b3" />


<img width="1318" height="767" alt="image" src="https://github.com/user-attachments/assets/5fd81fe9-62a3-4770-bb6b-93a75ff36975" />

<img width="1319" height="765" alt="image" src="https://github.com/user-attachments/assets/d0aeb221-e452-4e52-b2c6-7896a9f65aa3" />


<img width="1354" height="594" alt="image" src="https://github.com/user-attachments/assets/0a91c100-52b4-447e-a212-571d54b366fc" />



### Result:
Web Scraping using (beautifulsoup) Python is implemented successfully.
