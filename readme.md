# 📘 Web Scraping 
## **Q1. What is web scraping, and why is it used in Python programming?**
Web scraping is the process of automatically extracting data from websites.  
In Python, it is used because Python offers powerful libraries like **requests**, **BeautifulSoup**, **Selenium**, and **Scrapy** that make scraping easy and efficient.  
It helps collect information such as prices, news, job data, weather, and analytics.

---

## **Q2. How is web scraping different from APIs for extracting data from websites?**

| Web Scraping | API |
|--------------|-----|
| Extracts raw HTML data | Provides clean structured data (JSON/XML) |
| May break if website layout changes | Stable and reliable |
| Can violate policies if misused | Fully legal and allowed |
| Slower | Faster |
| No permission needed (but must check robots.txt) | Often needs key or approval |

**Summary:** Web scraping reads HTML. APIs provide ready-made data.

---

## **Q3. What are the ethical considerations and legal implications of web scraping?**
- Respect website **robots.txt** rules  
- Do not collect personal or copyrighted data  
- Avoid high request frequency (prevents server overload)  
- Follow website **Terms of Service**  
- Use scraping only for legal purposes like research, analytics, or learning  

Scraping becomes illegal if it:
- Breaks website security  
- Steals private or copyrighted content  
- Violates website policies  

---

## **Q4. Provide examples of real-world applications where web scraping is commonly used.**
- Price comparison tools  
- E-commerce product data extraction (Amazon, Flipkart)  
- News and article collection  
- Stock market data  
- Job listing extraction  
- Weather and travel fare monitoring  
- Social media trend monitoring  
- Academic or research datasets  

---

## **Q5. What is the `requests` library in Python, and what is its primary purpose?**
The **requests** library is used to send HTTP requests to websites.  
Its main purpose is to **retrieve webpage content**, such as HTML, JSON, images, or API responses.

---

## **Q6. How do you send an HTTP GET request using the requests library? Provide an example.**

```python
import requests

response = requests.get("https://example.com")
print(response.text)
```

---

## **Q7. Explain the difference between GET, POST, and DELETE requests in the requests library.**

| Method | Purpose |
|--------|---------|
| GET | Retrieve data from a server |
| POST | Send or submit data to a server (forms, login, upload) |
| DELETE | Remove data from a server via APIs |

---

## **Q8. How can you handle response status codes (e.g., 200, 404) using the requests library?**

```python
import requests

response = requests.get("https://example.com")

if response.status_code == 200:
    print("Success!")
elif response.status_code == 404:
    print("Page not found")
else:
    print("Error:", response.status_code)
```

Common codes:  
- **200** → Success  
- **404** → Not Found  
- **500** → Server Error  

---

## **Q9. What is the BeautifulSoup library, and how is it used in web scraping?**
BeautifulSoup is a Python library used to **parse and extract data** from HTML or XML content.  
It helps you find specific tags, extract text, and navigate through the DOM tree.

---

## **Q10. Explain the purpose of a parser in BeautifulSoup and list commonly used parsers.**
A parser converts HTML code into a searchable structure.

Commonly used BeautifulSoup parsers:
- `"html.parser"` (default)
- `"lxml"` (fast and powerful)
- `"html5lib"` (handles broken HTML)

Example:
```python
soup = BeautifulSoup(html, "html.parser")
```

---

## **Q11. How can you extract specific HTML elements (e.g., `<title>`, `<div>`) using BeautifulSoup? Provide an example.**

```python
from bs4 import BeautifulSoup

html = "<html><head><title>My Page</title></head><body><div>Content</div></body></html>"
soup = BeautifulSoup(html, "html.parser")

print(soup.title.text)        # Extract title
print(soup.find("div").text)  # Extract div
```

Output:
```
My Page
Content
```

---

## **Q12. Explain how to use BeautifulSoup to navigate and search the DOM tree for specific data.**

### 1. `find()` – returns first matching element  
```python
soup.find("p")
```

### 2. `find_all()` – returns list of matching elements  
```python
soup.find_all("a")
```

### 3. Accessing parent/child elements  
```python
div = soup.find("div")
print(div.parent)
print(div.contents)
```

### 4. Search by class or id  
```python
soup.find("div", class_="header")
soup.find("p", id="intro")
```

### 5. CSS selectors  
```python
soup.select("div.header > p")
```

BeautifulSoup allows smooth navigation through the DOM to extract structured data easily.

---