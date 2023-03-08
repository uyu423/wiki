---
title: Kotlin and CORS: A Guide to Cross-Origin Resource Sharing
description: 
published: true
date: 2023-02-12T06:56:11.998Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:56:05.331Z
---

- [Kotlin y CORS: una guía para compartir recursos entre orígenes***Spanish** document is available*](/es/Knowledge-base/Kotlin/kotlin-and-cors-a-guide-to-cross-origin-resource-sharing)
{.links-list}
- [Kotlin 和 CORS：跨源资源共享指南***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-cors-a-guide-to-cross-origin-resource-sharing)
{.links-list}
- [Kotlin 및 CORS: 원본 간 리소스 공유 가이드***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-cors-a-guide-to-cross-origin-resource-sharing)
{.links-list}

      
Kotlin and CORS: A Guide to Cross-Origin Resource Sharing

Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served. A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos.

The CORS mechanism works by adding HTTP headers to cross-domain HTTP requests and responses. 

## How does CORS work?

When a browser sends a request to a server, the browser includes an Origin header. This header indicates the domain of the page that is making the request. 

The server can then choose to allow or deny the request, based on the value of the Origin header. 

If the server allows the request, it will include the following headers in the response: 
- Access-Control-Allow-Origin: This header indicates the server allows the cross-origin request. 
- Access-Control-Allow-Methods: This header indicates the methods (e.g. GET, POST, etc.) that the client is allowed to use. 
- Access-Control-Allow-Headers: This header indicates the headers that the client is allowed to use. 
- Access-Control-Expose-Headers: This header indicates which headers the client is allowed to access. 

If the server does not allow the request, it will return a error. 

## Why is CORS important?

The CORS mechanism provides a way for browser-based applications to make cross-origin requests while still respecting the same-origin policy. 

The same-origin policy is a security measure that is designed to prevent cross-origin requests. However, there are many legitimate uses for cross-origin requests, such as making a request to a different domain to retrieve data or to use a third-party service. 

CORS provides a way to allow these types of cross-origin requests while still providing some protection against malicious requests. 

## What are some examples of CORS?

Here are some examples of how CORS can be used: 

- A web page that makes a cross-origin request to retrieve data from a third-party service. 
- A web page that makes a cross-origin request to load a script from a different domain. 
- A web page that makes a cross-origin request to an iframe that is embedded on the page. 

## What are some limitations of CORS?

CORS is not a perfect solution. The biggest limitation is that it is not supported by all browsers. 

Additionally, CORS can be bypassed by malicious requests. For example, a malicious request can use the XMLHttpRequest object to make a cross-origin request without the CORS headers. 

## How can I use CORS?

If you want to use CORS, you need to set up a server that supports CORS. 

 setting up a server is beyond the scope of this article, but you can find more information in the resources section below. 

Once you have a CORS-enabled server, you can make cross-origin requests using the XMLHttpRequest or Fetch APIs. 

## What is a preflight request?

A preflight request is an HTTP request that is sent before a cross-origin request. The preflight request is used to determine if the cross-origin request is safe to send. 

The preflight request is sent with the following headers: 
- Origin: The domain of the page that is making the request. 
- Access-Control-Request-Method: The method (e.g. GET, POST, etc.) that will be used for the cross-origin request. 
- Access-Control-Request-Headers: The headers that will be used for the cross-origin request. 

The server can then choose to allow or deny the request, based on the values of these headers. 

If the server allows the request, it will include the following headers in the response: 
- Access-Control-Allow-Origin: This header indicates the server allows the cross-origin request. 
- Access-Control-Allow-Methods: This header indicates the methods (e.g. GET, POST, etc.) that the client is allowed to use. 
- Access-Control-Allow-Headers: This header indicates the headers that the client is allowed to use. 
- Access-Control-Max-Age: This header indicates how long the response can be cached. 

If the server does not allow the request, it will return a error. 

## What is a preflight request?

A preflight request is an HTTP request that is sent before a cross-origin request. The preflight request is used to determine if the cross-origin request is safe to send. 

The preflight request is sent with the following headers: 
- Origin: The domain of the page that is making the request. 
- Access-Control-Request-Method: The method (e.g. GET, POST, etc.) that will be used for the cross-origin request. 
- Access-Control-Request-Headers: The headers that will be used for the cross-origin request. 

The server can then choose to allow or deny the request, based on the values of these headers. 

If the server allows the request, it will include the following headers in the response: 
- Access-Control-Allow-Origin: This header indicates the server allows the cross-origin request. 
- Access-Control-Allow-Methods: This header indicates the methods (e.g. GET, POST, etc.) that the client is allowed to use. 
- Access-Control-Allow-Headers: This header indicates the headers that the client is allowed to use. 
- Access-Control-Max-Age: This header indicates how long the response can be cached. 

If the server does not allow the request, it will return a error. 

## What are some tips for using CORS?

Here are some tips for using CORS: 

- Use the XMLHttpRequest or Fetch APIs to make cross-origin requests. 
- Set the Origin header to the domain of the page that is making the request. 
- Set the Access-Control-Request-Method header to the method (e.g. GET, POST, etc.) that will be used for the cross-origin request. 
- Set the Access-Control-Request-Headers header to the headers that will be used for the cross-origin request. 
- If the server allows the request, it will include the following headers in the response: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers, and Access-Control-Max-Age. 
- If the server does not allow the request, it will return a error. 

## Conclusion

CORS is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served. A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos.

The CORS mechanism works by adding HTTP headers to cross-domain HTTP requests and responses. 

When a browser sends a request to a server, the browser includes an Origin header. This header indicates the domain of the page that is making the request. 

The server can then choose to allow or deny the request, based on the value of the Origin header. 

If the server allows the request, it will include the following headers in the response: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers, and Access-Control-Expose-Headers. 

If the server does not allow the request, it will return a error. 

The CORS mechanism provides a way for browser-based applications to make cross-origin requests while still respecting the same-origin policy. 

The same-origin policy is a security measure that is designed to prevent cross-origin requests. However, there are many legitimate uses for cross-origin requests, such as making a request to a different domain to retrieve data or to use a third-party service. 

CORS provides a way to allow these types of cross-origin requests while still providing some protection against malicious requests. 

If you want to use CORS, you need to set up a server that supports CORS. setting up a server is beyond the scope of this article, but you can find more information in the resources section below. 

Once you have a CORS-enabled server, you can make cross-origin requests using the XMLHttpRequest or Fetch APIs. 

A preflight request is an HTTP request that is sent before a cross-origin request. The preflight request is used to determine if the cross-origin request is safe to send. 

The preflight request is sent with the following headers: Origin, Access-Control-Request-Method, and Access-Control-Request-Headers. 

The server can then choose to allow or deny the request, based on the values of these headers. 

If the server allows the request, it will include the following headers in the response: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers, and Access-Control-Max-Age. 

If the server does not allow the request, it will return a error. 

Here are some tips for using CORS: 

- Use the XMLHttpRequest or Fetch APIs to make cross-origin requests. 
- Set the Origin header to the domain of the page that is making the request. 
- Set the Access-Control-Request-Method header to the method (e.g. GET, POST, etc.) that will be used for the cross-origin request. 
- Set the Access-Control-Request-Headers header to the headers that will be used for the cross-origin request. 
- If the server allows the request, it will include the following headers in the response: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers, and Access-Control-Max-Age. 
- If the server does not allow the request, it will return a error.