# 🐍 Python Web Scraping Programs (Q1–Q10)

This document contains solutions to web scraping and HTTP request tasks using **requests** and **BeautifulSoup** libraries in Python.

---

# ✅ **Q1. Fetch HTML content & print status code**

```python
import requests

url = "https://example.com"
response = requests.get(url)

print("Status Code:", response.status_code)
print("HTML Content:\n", response.text)
```

---

# ✅ **Q2. Send GET request to free API & extract JSON**

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"
response = requests.get(url)

data = response.json()

first_post = data[0]

print("Title:", first_post['title'])
print("Body:", first_post['body'])
```

---

# ✅ **Q3. Send GET request with query parameters**

```python
import requests

url = "https://httpbin.org/get"
params = {"search": "python"}

response = requests.get(url, params=params)

print("Final URL:", response.url)
print("Response JSON:", response.json())
```

---

# ✅ **Q4. Parse HTML and extract `<h1>` and `<p>` tags using BeautifulSoup**

```python
from bs4 import BeautifulSoup

html = """
<html>
<head><title>Sample Page</title></head>
<body>
<h1>Welcome to Web Scraping</h1>
<p>This is a paragraph.</p>
<p>Another paragraph.</p>
</body>
</html>
"""

soup = BeautifulSoup(html, "html.parser")

print("All <h1> Tags:")
for h1 in soup.find_all("h1"):
    print(h1.text)

print("\nAll <p> Tags:")
for p in soup.find_all("p"):
    print(p.text)
```

---

# ✅ **Q5. Extract all hyperlinks (`<a>`) and print URLs + text**

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

print("Hyperlinks:")
for link in soup.find_all("a"):
    href = link.get("href")
    text = link.text.strip()
    print(f"Text: {text},  URL: {href}")
```

---

# ✅ **Q6. Scrape an HTML table & print headers and rows**

```python
import requests
from bs4 import BeautifulSoup

url = "https://www.w3schools.com/html/html_tables.asp"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

table = soup.find("table")

# Extract table headers
headers = [th.text.strip() for th in table.find_all("th")]
print("Headers:", headers)

# Extract rows
rows = []
for tr in table.find_all("tr")[1:]:
    row = [td.text.strip() for td in tr.find_all("td")]
    if row:
        rows.append(row)

print("\nRows:")
for r in rows:
    print(r)
```

---

# ✅ **Q7. Extract all images (`<img>`) – print src and alt**

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

print("Images Found:")
for img in soup.find_all("img"):
    src = img.get("src")
    alt = img.get("alt")
    print(f"Image Src: {src}, Alt: {alt}")
```

---

# ✅ **Q8. Extract data from a specific `<div class="content">` using CSS selectors**

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

content_section = soup.select("div.content")

for section in content_section:
    print("Content Section Text:", section.text.strip())

    nested_items = section.select("p, a, span")  # extracting inside elements
    for item in nested_items:
        print("Nested Element:", item.text.strip())
```

---

# ✅ **Q9. Scrape blog titles + URLs and save into CSV**

```python
import requests
from bs4 import BeautifulSoup
import csv

url = "https://blog.python.org/"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

posts = soup.find_all("h3", class_="post-title")

data = []

for post in posts:
    title = post.text.strip()
    link = post.find("a").get("href")
    data.append([title, link])

# Save into CSV
with open("blog_posts.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerow(["Title", "URL"])
    writer.writerows(data)

print("Data saved into blog_posts.csv")
```

---

# ✅ **Q10. Scrape product names & prices from a product listing**

❗ *Note: Example used on a demo site (books.toscrape.com).*

```python
import requests
from bs4 import BeautifulSoup

url = "https://books.toscrape.com/"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

products = soup.find_all("article", class_="product_pod")

for product in products:
    name = product.h3.a["title"]
    price = product.find("p", class_="price_color").text
    print(f"Product: {name} | Price: {price}")
```

---
