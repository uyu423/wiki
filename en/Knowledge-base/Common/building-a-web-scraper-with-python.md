---
title: Building a Web Scraper with Python
description: 
published: true
date: 2023-02-23T19:32:17.620Z
tags: 
editor: markdown
dateCreated: 2023-02-23T19:32:16.281Z
---

- [파이썬으로 웹 스크레이퍼 만들기***Korean** document is available*](/ko/Knowledge-base/Common/building-a-web-scraper-with-python)
{.links-list}

      
Web scraping is a process of extracting data from websites. It can be done manually but it is usually automated using a script or a program. Python is a great language for web scraping because of its ease of use and its many libraries.

In this article, we will learn how to build a web scraper using Python. We will use the BeautifulSoup library to parse HTML and the Requests library to make HTTP requests. We will also use the Pandas library to store the data in a DataFrame.

First, we need to install the BeautifulSoup, Requests, and Pandas libraries. We can do this using pip:

```
pip install beautifulsoup4
pip install requests
pip install pandas
```

Next, we need to import the libraries into our script:

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

Now, we need to specify the URL of the website that we want to scrape. In this example, we will scrape the website http://www.example.com:

```python
url = "http://www.example.com"
```

Next, we will make an HTTP GET request to the website using the requests library:

```python
r = requests.get(url)
```

Now, we will parse the HTML of the website using the BeautifulSoup library:

```python
soup = BeautifulSoup(r.content, "html.parser")
```

Finally, we will extract the data that we want from the website and store it in a DataFrame:

```python
data = []

for row in soup.find_all("tr"):
    data.append([td.text for td in row.find_all("td")])

df = pd.DataFrame(data, columns=["Column 1", "Column 2", "Column 3"])
```

And that's it! We have successfully built a web scraper using Python.