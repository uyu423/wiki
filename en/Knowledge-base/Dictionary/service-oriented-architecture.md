---
title: Service-Oriented Architecture
description: 
published: true
date: 2023-01-31T05:43:43.715Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:43:38.546Z
---

- [Service-Oriented Architecture***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/service-oriented-architecture)
{.links-list}
- [Service-Oriented Architecture***Japanese** version of this document is available*](/ja/Knowledge-base/Dictionary/service-oriented-architecture)
{.links-list}
- [Service-Oriented Architecture***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/service-oriented-architecture)
{.links-list}


# Overview

Service-Oriented Architecture (SOA) is an architectural style used in software development to create applications and services that are highly modular, scalable, and easy to maintain. It is based on loosely coupled services that communicate via web service protocols such as Simple Object Access Protocol (SOAP). This type of architecture is used to develop distributed software applications that are independent of platform, language, and hardware.

# History

Service-Oriented Architecture (SOA) was first proposed by computer scientist and software engineer David Chappell in the early 2000s as an alternative to the traditional monolithic architecture which had become increasingly difficult to maintain. Chappell developed SOA as a more modular and scalable approach to software development.

In the years that followed, SOA gained momentum and became widely adopted by many organizations. It allowed for a more efficient use of resources and enabled the development of services that could be used across multiple platforms and languages.

# Description

In a service-oriented architecture, applications are broken down into smaller, independent services which can be loosely coupled and deployed independently. These services communicate with each other via web service protocols such as Simple Object Access Protocol (SOAP). This allows for a more modular and scalable approach to software development and makes it easier to maintain applications.

Services in a service-oriented architecture are often based on a business process which is implemented as a workflow. This workflow is then broken down into individual services which can be reused across multiple applications.

For example, a workflow for creating an invoice might include a service for creating the invoice, another service for generating a PDF version of the invoice, and a service for sending the invoice to the customer. Each of these services can then be used in other applications, such as an accounting system or a customer service system.

# Example

Let's take a look at a simple example of a service-oriented architecture.

Imagine you're building a web-based application to help people save money on their energy bills. This application would require access to data from multiple sources such as energy providers, usage data, and customer information.

In a service-oriented architecture, you could create separate services for each of these data sources. For example, the energy provider service would provide data on energy prices, the usage data service would provide data on energy usage, and the customer information service would provide data on customer demographics.

These services could then be integrated into the web application and used to generate reports and other information for the user. This makes it easier to maintain the application and ensures that any changes to one service don't affect the other services.

# Pros and Cons

The primary benefit of service-oriented architecture is that it allows for a more modular approach to software development. This makes it easier to maintain applications and allows developers to reuse components across multiple applications. It also makes it easier to scale applications as services can be deployed independently.

However, there are some potential drawbacks to using a service-oriented architecture. For example, it can be difficult to maintain a consistent state across multiple services, and there can be conflicts between services if they are not properly designed. Additionally, services can be costly to maintain as they require regular updates and testing.

# Related Links

- [What is Service-Oriented Architecture (SOA)? (English) *Techopedia*](https://www.techopedia.com/definition/28817/service-oriented-architecture-soa)
- [Service-Oriented Architecture (English) *Wikipedia*](https://en.wikipedia.org/wiki/Service-oriented_architecture)
- [Service-Oriented Architecture (Français) *Wikipedia*](https://fr.wikipedia.org/wiki/Architecture_orient%C3%A9e_services) 
{.links-list}