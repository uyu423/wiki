---
title: REST
description: 
published: true
date: 2023-02-17T18:09:15.123Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:17:31.225Z
---

- [REST***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/rest)
{.links-list}
- [REST***Japanese** version of this document is available*](/ja/Knowledge-base/Dictionary/rest)
{.links-list}
- [REST***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/rest)
{.links-list}


# Overview

Representational State Transfer (REST) is an architectural style for designing distributed systems, such as web services. It is based on the principles of client-server architecture and stateless communication. 

# History

REST was first proposed by Roy Fielding in 2000 as part of his doctoral dissertation. He argued that existing architectures, such as RPC and SOAP, were overly complex and did not reflect the way the web worked.

# Description

REST is based on the idea that the client and server can communicate using a uniform interface. This interface is based on the principles of **HTTP**, a protocol used for exchanging data between computers on the web. It is designed to be **stateless**, meaning that each request from the client is treated as an independent transaction, and the server does not maintain any information about the client between requests.

The main components of the REST architecture are **resources**, **representations**, and **actions**. Resources are the fundamental elements of the system, such as users or books. Representations are the data that is exchanged between the client and the server, such as HTML documents or JSON objects. And actions are the operations that can be performed on the resources, such as creating, updating, or deleting them.

REST relies on the concept of **hypermedia**. This is the idea that the server can provide links to other related resources in the response. For example, a response to a request for a book might include a link to the author's profile page. This allows the client to access additional information without having to make additional requests.

# Digression

REST also enables the use of **caching**, which can improve the performance of the system by reducing the amount of data that needs to be transferred between the client and the server.

REST also supports the concept of **versioning**, which allows new versions of the API to be released without breaking existing clients. This is achieved by including version information in the URL, and by supporting multiple versions of the API simultaneously.

# Related Links 
- [RESTful Web Services*O'Reilly Media*](https://www.oreilly.com/library/view/restful-web-services/9780596155860/)
- [REST API Tutorial*REST API Tutorial*](https://restapitutorial.com/)
- [Introduction to REST*Google Developers*](https://developers.google.com/drive/api/v3/about-rest)
{.links-list}