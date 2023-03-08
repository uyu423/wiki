---
title: Enabling Cross-Origin Resource Sharing (CORS) for Secure API Access
description: 
published: true
date: 2023-02-05T01:17:36.437Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:17:31.137Z
---

- [Habilitación del uso compartido de recursos entre orígenes (CORS) para el acceso seguro a la API***Spanish** document is available*](/es/Knowledge-base/Backend/enabling-cross-origin-resource-sharing-cors-for-secure-api-access)
{.links-list}
- [为安全 API 访问启用跨源资源共享 (CORS)***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/enabling-cross-origin-resource-sharing-cors-for-secure-api-access)
{.links-list}
- [보안 API 액세스를 위한 CORS(Cross-Origin Resource Sharing) 활성화***Korean** document is available*](/ko/Knowledge-base/Backend/enabling-cross-origin-resource-sharing-cors-for-secure-api-access)
{.links-list}


# Enabling Cross-Origin Resource Sharing (CORS) for Secure API Access

## Introduction

In a nutshell, Cross-Origin Resource Sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served. A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos.

In order for browsers to make cross-origin requests, a web application must first enable CORS. Enabling CORS is not required for same-origin requests, i.e. requests that are made to the same domain, protocol, and port number as the page itself.

## How CORS Works

When a browser makes a cross-origin request, the browser sends a request to the server with an `Origin` header. The `Origin` header indicates the origin of the request, i.e. the domain, protocol, and port number where the request originated.

The server can then choose to allow or block the request based on the `Origin` header. If the server allows the request, it will set an `Access-Control-Allow-Origin` header in the response. The value of the `Access-Control-Allow-Origin` header can be a specific origin (e.g. `https://example.com`), a wildcard (`*`), or `null`.

If the `Access-Control-Allow-Origin` header is not present in the response, or if its value is not a valid origin, then the browser will block the response.

## Why CORS is Important

Without CORS, cross-origin requests will be blocked by the browser. This is important because it prevents malicious scripts from making unauthorized requests to your API.

## Enabling CORS

### Setting the `Access-Control-Allow-Origin` Header

The `Access-Control-Allow-Origin` header tells the browser whether or not it should allow cross-origin requests from the origin where the request originated.

You can set the `Access-Control-Allow-Origin` header in the HTTP response from your server. The value of the header can be a specific origin (e.g. `https://example.com`), a wildcard (`*`), or `null`.

If you want to allow cross-origin requests from any origin, you can set the `Access-Control-Allow-Origin` header to `*`.

```
Access-Control-Allow-Origin: *
```

If you want to allow cross-origin requests from a specific origin, you can set the `Access-Control-Allow-Origin` header to the origin of the request.

```
Access-Control-Allow-Origin: https://example.com
```

If you want to allow cross-origin requests from multiple origins, you can set the `Access-Control-Allow-Origin` header to a comma-separated list of origins.

```
Access-Control-Allow-Origin: https://example.com,https://example.org
```

If you want to allow cross-origin requests from all origins except a specific origin, you can set the `Access-Control-Allow-Origin` header to `*` and the `Access-Control-Expose-Headers` header to `Origin`.

```
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: Origin
```

### Setting the `Access-Control-Allow-Credentials` Header

The `Access-Control-Allow-Credentials` header tells the browser whether or not it should send cookies with cross-origin requests.

If you want to allow cookies to be sent with cross-origin requests, you can set the `Access-Control-Allow-Credentials` header to `true`.

```
Access-Control-Allow-Credentials: true
```

If you want to allow cookies to be sent with cross-origin requests from a specific origin, you can set the `Access-Control-Allow-Origin` header to the origin of the request and the `Access-Control-Allow-Credentials` header to `true`.

```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Credentials: true
```

### Setting the `Access-Control-Expose-Headers` Header

The `Access-Control-Expose-Headers` header tells the browser which headers it should allow to be exposed to the client.

If you want to allow cross-origin requests to expose all headers, you can set the `Access-Control-Expose-Headers` header to `*`.

```
Access-Control-Expose-Headers: *
```

If you want to allow cross-origin requests to expose a specific header, you can set the `Access-Control-Expose-Headers` header to the header you want to allow.

```
Access-Control-Expose-Headers: Content-Type
```

If you want to allow cross-origin requests to expose multiple headers, you can set the `Access-Control-Expose-Headers` header to a comma-separated list of headers.

```
Access-Control-Expose-Headers: Content-Type,X-Custom-Header
```

## Preflighted Requests

Some cross-origin requests are preflighted. A preflighted request is a request that is made with an `OPTIONS` HTTP method and that has an `Origin` header.

The browser sends a preflight request to the server to check if the server allows the cross-origin request. The server can choose to allow or block the preflight request.

If the server allows the preflight request, it will set an `Access-Control-Allow-Methods` header in the response. The value of the `Access-Control-Allow-Methods` header is a comma-separated list of HTTP methods that the server allows.

If the server allows the preflight request and the request method is `GET`, `HEAD`, or `POST`, the server will set an `Access-Control-Allow-Headers` header in the response. The value of the `Access-Control-Allow-Headers` header is a comma-separated list of HTTP headers that the server allows.

## CORS and Security

CORS is a security mechanism that can be used to protect your API from malicious requests. By enabling CORS, you can specify which origins are allowed to make cross-origin requests to your API.

## Conclusion

In this article, we've covered what CORS is, how it works, and why it's important. We've also shown how to enable CORS on your server.