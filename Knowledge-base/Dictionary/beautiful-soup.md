---
title: Beautiful Soup
description: 
published: true
date: 2023-02-23T22:32:31.612Z
tags: 
editor: markdown
dateCreated: 2023-02-23T22:32:30.264Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Beautiful Soup***English** document is available*](/en/Knowledge-base/Dictionary/beautiful-soup)
{.links-list}


# 개요
Beautiful Soup은 웹사이트에서 데이터를 스크랩하는 데 사용되는 Python 라이브러리입니다. 웹 스크래핑을 더 쉽고 빠르게 할 수 있도록 설계되었습니다. Beautiful Soup은 구문 분석 트리를 탐색, 검색 및 수정하기 위한 몇 가지 간단한 방법과 Python 관용구를 제공합니다.

# 설명
Beautiful Soup은 HTML 및 XML 문서를 구문 분석하기 위한 Python 라이브러리입니다. 웹 스크래핑을 더 쉽고 빠르게 할 수 있도록 설계되었습니다. Beautiful Soup은 구문 분석 트리를 탐색, 검색 및 수정하기 위한 몇 가지 간단한 방법과 Python 관용구를 제공합니다.

Beautiful Soup은 Python HTML 파서 라이브러리인 lxml 위에 구축되었습니다. 구문 분석된 HTML 및 XML 문서에 대한 구문 분석 트리를 만들고 개발자가 트리 내에 저장된 데이터에 액세스할 수 있는 방법을 제공합니다.

Beautiful Soup은 개발자가 HTML 및 XML 문서에서 데이터를 빠르게 추출할 수 있게 해주기 때문에 웹 스크래핑에 유용합니다. 제품 가격, 제품 리뷰 등과 같은 웹 사이트에서 데이터를 추출하는 데 사용할 수 있습니다.

Beautiful Soup은 파스 트리를 수정하는 메서드도 제공하여 개발자가 트리에 저장된 데이터를 수정할 수 있도록 합니다. 불필요한 태그나 속성을 제거하는 등 데이터를 정리하는 데 사용할 수 있습니다.

# 특징
Beautiful Soup은 구문 분석 트리를 탐색, 검색 및 수정하기 위한 몇 가지 간단한 방법과 Python 관용구를 제공합니다.

라이브러리는 구문 분석 트리를 순회하고 특정 요소에 액세스하는 방법을 제공합니다. 또한 class 및 id와 같은 특성을 기반으로 요소를 검색하는 메서드를 제공합니다.

Beautiful Soup은 파스 트리를 수정하는 메서드도 제공하여 개발자가 트리에 저장된 데이터를 수정할 수 있도록 합니다. 불필요한 태그나 속성을 제거하는 등 데이터를 정리하는 데 사용할 수 있습니다.

# 예
다음 예는 Beautiful Soup을 사용하여 웹 사이트에서 제품 가격을 스크랩하는 방법을 보여줍니다.

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

# 장점과 단점
아름다운 수프에는 몇 가지 장점과 단점이 있습니다.

**장점**

- 사용하기 쉬움: Beautiful Soup은 웹 스크래핑을 더 쉽고 빠르게 할 수 있도록 설계되었습니다.
- 유연성: Beautiful Soup은 구문 분석 트리를 탐색, 검색 및 수정하기 위한 몇 가지 간단한 메서드와 Python 관용구를 제공합니다.
- 확장 가능: Beautiful Soup은 사용자 지정 파서를 사용하여 확장할 수 있습니다.

**단점**
- 느림: Beautiful Soup은 가장 빠른 웹 스크래핑 라이브러리가 아닙니다.
- 제한된 지원: 뷰티플수프는 모든 HTML 및 XML 기능을 지원하지 않습니다.

# 관련 기술
Beautiful Soup은 Scrapy 및 Selenium과 같은 다른 웹 스크래핑 라이브러리와 관련이 있습니다. Scrapy는 웹 크롤러를 만들고 웹 사이트에서 데이터를 스크랩하기 위한 Python 프레임워크입니다. Selenium은 웹 브라우저를 제어하고 웹 사이트에서 데이터를 스크랩하는 데 사용할 수 있는 브라우저 자동화 라이브러리입니다.