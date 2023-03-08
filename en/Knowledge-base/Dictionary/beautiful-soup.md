---
title: Beautiful Soup
description: 
published: true
date: 2023-02-23T22:32:37.124Z
tags: 
editor: markdown
dateCreated: 2023-02-23T22:32:30.267Z
---

- [Beautiful Soup***Korean** document is available*](/ko/Knowledge-base/Dictionary/beautiful-soup)
{.links-list}


# Overview
Beautiful Soup is a Python library used to scrape data from websites. It is designed to make web scraping easier and faster. Beautiful Soup provides a few simple methods and Pythonic idioms for navigating, searching, and modifying a parse tree.

# Description
Beautiful Soup is a Python library for parsing HTML and XML documents. It is designed to make web scraping easier and faster. Beautiful Soup provides a few simple methods and Pythonic idioms for navigating, searching, and modifying a parse tree.

Beautiful Soup is built on top of the Python HTML parser library, lxml. It creates a parse tree for parsed HTML and XML documents and provides ways for developers to access the data stored within the tree.

Beautiful Soup is useful for web scraping because it allows developers to quickly extract data from HTML and XML documents. It can be used to extract data from websites, such as product prices, product reviews, and more.

Beautiful Soup also provides methods to modify the parse tree, allowing developers to modify the data stored in the tree. This can be used to clean up data, such as removing unnecessary tags or attributes.

# Features
Beautiful Soup provides a few simple methods and Pythonic idioms for navigating, searching, and modifying a parse tree.

The library provides methods to traverse the parse tree and access specific elements. It also provides methods to search for elements based on attributes, such as class and id.

Beautiful Soup also provides methods to modify the parse tree, allowing developers to modify the data stored in the tree. This can be used to clean up data, such as removing unnecessary tags or attributes.

# Example
The following example shows how to use Beautiful Soup to scrape product prices from a website:

```python
from bs4 import BeautifulSoup
import requests

url = "https://example.com/products"

# Make a GET request to fetch the raw HTML content
html_content = requests.get(url).text

# Parse the html content
soup = BeautifulSoup(html_content, "lxml")

# Find all the products
products = soup.find_all("div", attrs={"class": "product"})

# Iterate over each product and get the product price
for product in products:
    product_price = product.find("span", attrs={"class": "price"}).text
    print("Product Price:", product_price)
```

# Pros and Cons
Beautiful Soup has several advantages and disadvantages.

**Pros**

- Easy to use: Beautiful Soup is designed to make web scraping easier and faster.
- Flexible: Beautiful Soup provides a few simple methods and Pythonic idioms for navigating, searching, and modifying a parse tree.
- Extensible: Beautiful Soup can be extended with custom parsers.

**Cons**
- Slow: Beautiful Soup is not the fastest web scraping library.
- Limited support: Beautiful Soup does not support all HTML and XML features.

# Related Technology
Beautiful Soup is related to other web scraping libraries, such as Scrapy and Selenium. Scrapy is a Python framework for creating web crawlers and scraping data from websites. Selenium is a browser automation library that can be used to control a web browser and scrape data from websites.