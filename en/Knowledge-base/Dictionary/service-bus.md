---
title: Service Bus
description: 
published: true
date: 2023-03-04T14:32:37.199Z
tags: 
editor: markdown
dateCreated: 2023-03-04T14:32:35.814Z
---

- [Service Bus***Korean** document is available*](/ko/Knowledge-base/Dictionary/service-bus)
{.links-list}


# Service Bus

## Overview

A service bus is a messaging infrastructure that enables communication between different applications, services, and systems. It provides a reliable and scalable way to exchange messages asynchronously, decoupling the sender and receiver from each other. Service bus is used in distributed computing environments where different components of an application need to communicate with each other.

## Description

A service bus is a middleware that facilitates communication between different applications. It acts as a message broker that receives messages from a sender and routes them to the appropriate receiver. The sender and receiver can be different applications or different components of the same application. 

Service bus provides a way to exchange messages asynchronously, which means the sender and receiver don't have to be available at the same time. The sender can send a message to the service bus and continue its work without waiting for a response. The service bus will store the message and deliver it to the receiver when it becomes available. This decouples the sender and receiver from each other, making the system more flexible and scalable.

Service bus also provides features like message queuing, message routing, and message transformation. Message queuing allows messages to be stored in a queue until they are processed by the receiver. Message routing enables messages to be sent to the appropriate receiver based on their content or other criteria. Message transformation allows messages to be converted from one format to another, enabling communication between systems that use different message formats.

Service bus can be implemented using different technologies like JMS, AMQP, or MQTT. Microsoft Azure Service Bus and Amazon Web Services (AWS) Simple Queue Service (SQS) are popular examples of service bus implementations.

## History

The concept of a service bus has been around for a long time. In the early days of distributed computing, message-oriented middleware (MOM) was used to facilitate communication between different applications. MOM provided features like message queuing, message routing, and message transformation.

With the advent of web services and service-oriented architecture (SOA), the concept of a service bus evolved. SOA introduced the idea of services, which are self-contained, modular components that can be accessed over a network. Service bus became an essential component of SOA, enabling communication between different services.

## Features

Service bus provides the following features:

- Asynchronous messaging: Enables communication between sender and receiver without requiring them to be available at the same time.
- Message queuing: Stores messages in a queue until they are processed by the receiver.
- Message routing: Sends messages to the appropriate receiver based on their content or other criteria.
- Message transformation: Converts messages from one format to another, enabling communication between systems that use different message formats.
- Scalability: Enables the system to handle a large number of messages and users.
- Reliability: Ensures that messages are delivered to the receiver even if the sender or receiver is temporarily unavailable.
- Security: Provides features like authentication, authorization, and encryption to ensure secure communication.

## Example

Suppose you have an e-commerce website that needs to notify customers when their orders are shipped. You can use a service bus to implement this functionality. When a customer places an order, the website sends a message to the service bus containing the order details and the customer's email address. The service bus stores the message in a queue and sends a notification email to the customer when the order is shipped. The email service retrieves the message from the queue and sends the email to the customer.

## Pros and Cons

Pros:

- Decouples sender and receiver, making the system more flexible and scalable.
- Enables asynchronous messaging, which improves performance and responsiveness.
- Provides features like message queuing, message routing, and message transformation, which simplify communication between different applications.
- Improves reliability by ensuring that messages are delivered even if the sender or receiver is temporarily unavailable.
- Provides security features like authentication, authorization, and encryption.

Cons:

- Service bus adds complexity to the system, requiring additional infrastructure and maintenance.
- Service bus can introduce latency and overhead, which can affect performance.
- Service bus can be a single point of failure, which can affect the entire system.

## Controversy

There is no controversy surrounding service bus.

## Related Technology

Service bus is related to the following technologies:

- Message-oriented middleware (MOM): Provides similar features to service bus, enabling communication between different applications.
- Enterprise service bus (ESB): Provides additional features like protocol transformation, service orchestration, and service mediation.
- Web services: Enables communication between different applications using standardized protocols like SOAP and REST.

## Digression

Service bus is an essential component of modern distributed computing systems. It enables communication between different applications, services, and systems, making the system more flexible and scalable. Service bus provides features like message queuing, message routing, and message transformation, which simplify communication between different applications. Service bus is used in various industries like e-commerce, finance, healthcare, and transportation. 

## Others

Service bus is a critical component of modern distributed computing systems. It enables communication between different applications, services, and systems, making the system more flexible and scalable. Service bus provides features like message queuing, message routing, and message transformation, which simplify communication between different applications. Service bus is used in various industries like e-commerce, finance, healthcare, and transportation.