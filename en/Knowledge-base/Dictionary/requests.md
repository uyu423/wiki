---
title: Requests
description: 
published: true
date: 2023-02-08T02:18:07.447Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:18:00.937Z
---

- [Requests***Japanese** document is available*](/ja/Knowledge-base/Dictionary/requests)
{.links-list}
- [Requests***Spanish** document is available*](/es/Knowledge-base/Dictionary/requests)
{.links-list}
- [Requests***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/requests)
{.links-list}
- [Requests***Korean** document is available*](/ko/Knowledge-base/Dictionary/requests)
{.links-list}


# Overview

Requests is an Apache2 Licensed HTTP library, written in Python, for human beings. Requests allows users to easily make HTTP requests, such as GET, POST, PUT, and DELETE, to a specified URL. It also supports authentication, cookies, and other features.

# Description

Requests is a popular Python library for making HTTP requests. It is designed to be simple and intuitive for developers to use, with a focus on making the process of making HTTP requests easier. Requests supports a wide range of HTTP requests, such as GET, POST, PUT, and DELETE. It also provides support for authentication, cookies, and other features.

Requests is built on top of the popular urllib3 library, which provides a low-level interface for making HTTP requests. Requests uses urllib3 to provide a higher-level API for making HTTP requests, making it easier to use.

Requests also provides a number of convenience features, such as the ability to specify data to be sent with a request, and the ability to specify a timeout for a request.

# History

Requests was originally created in 2011 by Kenneth Reitz. It was initially released as an open source project on GitHub, and quickly gained popularity among developers. Since its initial release, Requests has become one of the most popular Python libraries, with over 10 million downloads.

# Features

Requests provides a number of features to make it easier for developers to make HTTP requests. 

- Requests supports a wide range of HTTP requests, including GET, POST, PUT, and DELETE. 
- Requests supports authentication, allowing developers to easily authenticate with a web service. 
- Requests supports cookies, allowing developers to easily handle cookies in their requests. 
- Requests supports data, allowing developers to easily specify data to be sent with a request. 
- Requests supports timeouts, allowing developers to specify a timeout for a request. 

# Example

Here is an example of using Requests to make a GET request to a web service:

```python
import requests

response = requests.get('http://example.com/api/v1/data')

if response.status_code == 200:
    data = response.json()
    print(data)
```

# Pros and Cons

Pros:

- Easy to use: Requests provides a simple and intuitive API for making HTTP requests.
- Wide range of requests: Requests supports a wide range of HTTP requests, such as GET, POST, PUT, and DELETE.
- Authentication: Requests supports authentication, making it easier to authenticate with web services.
- Cookies: Requests supports cookies, making it easier to handle cookies in requests.
- Data: Requests supports data, making it easier to specify data to be sent with a request.
- Timeouts: Requests supports timeouts, making it easier to specify a timeout for a request.

Cons:

- Limited support for non-HTTP requests: Requests only supports HTTP requests, so it cannot be used to make non-HTTP requests.
- No support for streaming: Requests does not support streaming, so it cannot be used to stream data.

# Controversy

Requests has been the subject of some controversy due to its use of urllib3, which is a low-level library for making HTTP requests. Some developers have argued that Requests should not be used in production due to the potential security risks posed by urllib3.

# Related Technology

- urllib3: urllib3 is a low-level library for making HTTP requests. Requests is built on top of urllib3.
- Requests-toolbelt: Requests-toolbelt is a library for making HTTP requests with Requests.
- Requests-mock: Requests-mock is a library for mocking HTTP requests with Requests.

# Digression

Requests is a popular library for making HTTP requests in Python. It is designed to be easy to use, and provides a wide range of features to make it easier to make HTTP requests.

# Others

Requests is an open source project, released under the Apache2 License. It is actively maintained, and is widely used by developers.