---
title: Understanding Event Sourcing in Infrastructure Development
description: 
published: true
date: 2023-01-31T08:36:22.616Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:36:19.134Z
---

- [인프라 개발의 이벤트 소싱 이해***Korean** version of this document is available*](/ko/Knowledge-base/Backend/understanding-event-sourcing-in-infrastructure-development)
{.links-list}
- [インフラストラクチャ開発におけるイベント ソーシングについて***Japanese** version of this document is available*](/ja/Knowledge-base/Backend/understanding-event-sourcing-in-infrastructure-development)
{.links-list}
- [了解基础设施开发中的事件溯源***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Backend/understanding-event-sourcing-in-infrastructure-development)
{.links-list}


This article is for IT developers who want to understand what event sourcing is and how it can be used to streamline infrastructure development.



Event sourcing is a term that is becoming more and more commonplace in IT development conversations. But what is it? Event sourcing is the practice of building an application bylogging all changes to the application state as a sequence of events. 

This sequence of events is often called an event log. Event logs have a number of advantages: 

1. They offer a complete history of changes to the application state. 
2. They can be used to reconstruct the current state of the application at any given point in time. 
3. They can be used to replay changes to the application state, which is useful for debugging or auditing purposes. 

Event sourcing has a number of benefits for developers: 

1. It makes it easier to debug applications, since all changes are logged and can be traced back to their original causes. 
2. It makes it easier to audit applications, since all changes are logged and can be traced back to their original causes. 
3. It makes it easier to add new features to applications, since developers can replay the event log to see how the application state changes in response to various events. 

Event sourcing has a number of drawbacks: 

1. It can be difficult to implement event sourcing in an existing application. 
2. It can be difficult to maintain event logs, since they can grow large over time. 
3. It can be difficult to query event logs, since they are often stored in a linear format.

Despite these drawbacks, event sourcing has become a popular technique for building applications, especially in the area of microservices. This is because event sourcing offers a number of benefits for microservice architecture, including: 

1. Improved debugging, since each microservice can maintain its own event log. 
2. Improved auditing, since each microservice can maintain its own event log. 
3. Improved scalability, since each microservice can maintain its own event log. 
4. Improved modularity, since each microservice can maintain its own event log. 

If you're interested in learning more about event sourcing, there are a number of resources available online, including: 

1. [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html) - A comprehensive guide to event sourcing from Martin Fowler. 
2. [A Practical Introduction to Event Sourcing](https://www.infoq.com/articles/introduction-to-event-sourcing) - A practical introduction to event sourcing from InfoQ. 
3. [Event Sourcing](https://www.microservices.com/articles/event-sourcing/) - A guide to event sourcing from Microservices.com.