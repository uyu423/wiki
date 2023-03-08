---
title: 파이썬으로 웹 스크레이퍼 만들기
description: 
published: true
date: 2023-02-23T19:32:23.106Z
tags: 
editor: markdown
dateCreated: 2023-02-23T19:32:16.280Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building a Web Scraper with Python***English** document is available*](/en/Knowledge-base/Common/building-a-web-scraper-with-python)
{.links-list}

      
웹 스크래핑은 웹사이트에서 데이터를 추출하는 프로세스입니다. 수동으로 수행할 수 있지만 일반적으로 스크립트나 프로그램을 사용하여 자동화됩니다. Python은 사용하기 쉽고 라이브러리가 많기 때문에 웹 스크래핑에 적합한 언어입니다.

이 글에서는 Python을 사용하여 웹 스크래퍼를 빌드하는 방법에 대해 알아봅니다. BeautifulSoup 라이브러리를 사용하여 HTML을 구문 분석하고 Requests 라이브러리를 사용하여 HTTP 요청을 만듭니다. 또한 Pandas 라이브러리를 사용하여 데이터를 DataFrame에 저장합니다.

먼저 BeautifulSoup, Requests 및 Pandas 라이브러리를 설치해야 합니다. pip를 사용하여 이 작업을 수행할 수 있습니다.

```
pip install beautifulsoup4
pip install requests
pip install pandas
```

다음으로 라이브러리를 스크립트로 가져와야 합니다.

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

이제 스크랩하려는 웹사이트의 URL을 지정해야 합니다. 이 예에서는 http://www.example.com 웹 사이트를 스크랩합니다.

```python
url = "http://www.example.com"
```

다음으로 요청 라이브러리를 사용하여 웹 사이트에 HTTP GET 요청을 수행합니다.

```python
r = requests.get(url)
```

이제 BeautifulSoup 라이브러리를 사용하여 웹사이트의 HTML을 구문 분석합니다.

```python
soup = BeautifulSoup(r.content, "html.parser")
```

마지막으로 웹사이트에서 원하는 데이터를 추출하여 DataFrame에 저장합니다.

```python
data = []

for row in soup.find_all("tr"):
    data.append([td.text for td in row.find_all("td")])

df = pd.DataFrame(data, columns=["Column 1", "Column 2", "Column 3"])
```

그리고 그게 다야! Python을 사용하여 웹 스크레이퍼를 성공적으로 구축했습니다.