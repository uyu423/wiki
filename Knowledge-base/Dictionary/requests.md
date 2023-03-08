---
title: Requests
description: 
published: true
date: 2023-02-08T02:18:02.855Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:18:00.927Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Requests***English** document is available*](/en/Knowledge-base/Dictionary/requests)
{.links-list}


# 개요

Requests는 인간을 위해 Python으로 작성된 Apache2 라이센스 HTTP 라이브러리입니다. 요청을 사용하면 사용자가 지정된 URL에 GET, POST, PUT 및 DELETE와 같은 HTTP 요청을 쉽게 할 수 있습니다. 또한 인증, 쿠키 및 기타 기능을 지원합니다.

# 설명

요청은 HTTP 요청을 만드는 데 널리 사용되는 Python 라이브러리입니다. HTTP 요청을 더 쉽게 만드는 프로세스를 만드는 데 중점을 두고 개발자가 사용하기 간단하고 직관적으로 설계되었습니다. 요청은 GET, POST, PUT 및 DELETE와 같은 광범위한 HTTP 요청을 지원합니다. 또한 인증, 쿠키 및 기타 기능에 대한 지원을 제공합니다.

요청은 HTTP 요청을 만들기 위한 저수준 인터페이스를 제공하는 인기 있는 urllib3 라이브러리 위에 구축됩니다. Requests는 urllib3를 사용하여 HTTP 요청을 만들기 위한 상위 수준 API를 제공하므로 사용하기가 더 쉽습니다.

요청은 또한 요청과 함께 보낼 데이터를 지정하는 기능 및 요청에 대한 제한 시간을 지정하는 기능과 같은 여러 편의 기능을 제공합니다.

# 역사

요청은 원래 Kenneth Reitz가 2011년에 만들었습니다. 처음에는 GitHub에서 오픈 소스 프로젝트로 출시되었으며 개발자들 사이에서 빠르게 인기를 얻었습니다. 최초 릴리스 이후 Requests는 천만 회 이상 다운로드된 가장 인기 있는 Python 라이브러리 중 하나가 되었습니다.

# 특징

요청은 개발자가 HTTP 요청을 보다 쉽게 수행할 수 있도록 여러 기능을 제공합니다.

- 요청은 GET, POST, PUT 및 DELETE를 포함한 광범위한 HTTP 요청을 지원합니다.
- 요청은 인증을 지원하므로 개발자가 웹 서비스로 쉽게 인증할 수 있습니다.
- 요청은 쿠키를 지원하므로 개발자가 요청에서 쿠키를 쉽게 처리할 수 있습니다.
- 요청은 데이터를 지원하므로 개발자가 요청과 함께 보낼 데이터를 쉽게 지정할 수 있습니다.
- 요청은 제한 시간을 지원하므로 개발자가 요청에 대한 제한 시간을 지정할 수 있습니다.

# 예

다음은 요청을 사용하여 웹 서비스에 GET 요청을 하는 예입니다.

```python
import requests

response = requests.get('http://example.com/api/v1/data')

if response.status_code == 200:
    data = response.json()
    print(data)
```

# 장점과 단점

장점:

- 사용하기 쉬움: Requests는 HTTP 요청을 만들기 위한 간단하고 직관적인 API를 제공합니다.
- 광범위한 요청: 요청은 GET, POST, PUT 및 DELETE와 같은 광범위한 HTTP 요청을 지원합니다.
- 인증: Requests는 인증을 지원하여 웹 서비스로 더 쉽게 인증할 수 있습니다.
- 쿠키: 요청은 쿠키를 지원하므로 요청에서 쿠키를 더 쉽게 처리할 수 있습니다.
- 데이터: 요청은 데이터를 지원하므로 요청과 함께 보낼 데이터를 더 쉽게 지정할 수 있습니다.
- 시간 초과: 요청은 시간 초과를 지원하므로 요청에 대한 시간 초과를 더 쉽게 지정할 수 있습니다.

단점:

- 비 HTTP 요청에 대한 제한된 지원: 요청은 HTTP 요청만 지원하므로 비 HTTP 요청을 만드는 데 사용할 수 없습니다.
- 스트리밍 지원 안 함: 요청은 스트리밍을 지원하지 않으므로 스트리밍 데이터에 사용할 수 없습니다.

# 논란

Requests는 HTTP 요청을 만들기 위한 저수준 라이브러리인 urllib3을 사용하기 때문에 일부 논란의 대상이 되었습니다. 일부 개발자는 urllib3에 의해 제기된 잠재적인 보안 위험으로 인해 프로덕션에서 요청을 사용해서는 안 된다고 주장했습니다.

# 관련 기술

- urllib3: urllib3은 HTTP 요청을 만들기 위한 저수준 라이브러리입니다. 요청은 urllib3 위에 구축됩니다.
- Requests-toolbelt: Requests-toolbelt는 요청으로 HTTP 요청을 만들기 위한 라이브러리입니다.
- Requests-mock: Requests-mock은 요청으로 HTTP 요청을 조롱하기 위한 라이브러리입니다.

# 여담

요청은 Python에서 HTTP 요청을 만드는 데 널리 사용되는 라이브러리입니다. 사용하기 쉽게 설계되었으며 HTTP 요청을 보다 쉽게 할 수 있도록 다양한 기능을 제공합니다.

# 기타

Requests는 Apache2 라이선스에 따라 출시된 오픈 소스 프로젝트입니다. 적극적으로 유지 관리되며 개발자가 널리 사용합니다.