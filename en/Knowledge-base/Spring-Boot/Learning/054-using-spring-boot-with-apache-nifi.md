---
title: 054: Using Spring Boot with Apache Nifi
description: 
published: true
date: 2023-02-03T01:23:42.085Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:23:37.387Z
---

- [054: Uso de Spring Boot con Apache Nifi***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/054-using-spring-boot-with-apache-nifi)
{.links-list}
- [054：将 Spring Boot 与 Apache Nifi 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/054-using-spring-boot-with-apache-nifi)
{.links-list}
- [054: Apache Nifi와 함께 Spring Boot 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/054-using-spring-boot-with-apache-nifi)
{.links-list}


# Using Spring Boot with Apache Nifi

Spring Boot is a popular Java-based framework used for creating microservices. Apache NiFi is a powerful dataflow tool that can be used to process and route data.

In this post, we'll show how to use Spring Boot with Apache NiFi. We'll cover the following topics:

* Setting up a Spring Boot project
* Configuring Apache NiFi
* Creating a Spring Boot service
* Testing the dataflow

## Setting up a Spring Boot project

The first thing we need to do is create a new Spring Boot project. We can use the [Spring Initializr](https://start.spring.io/) to generate a project with the necessary dependencies.

For this example, we'll need the following dependencies:

* Web - for creating a web application
* H2 - for the in-memory database

Once we have the project set up, we can start configuring Apache NiFi.

## Configuring Apache NiFi

Apache NiFi needs to be configured to use the Spring Boot service we'll be creating. We'll need to add the following to the NiFi configuration:

* A Processor for invoking the Spring Boot service
* A Connection Pool for the Processor
* A Controller Service for the Connection Pool

We can use the NiFi GUI to configure these settings. First, we'll add the Processor:

![Add Processor](https://i.imgur.com/Lb6qyFW.png)

Next, we'll add the Connection Pool:

![Add Connection Pool](https://i.imgur.com/vH8X3zJ.png)

Finally, we'll add the Controller Service:

![Add Controller Service](https://i.imgur.com/g4SVfyi.png)

## Creating a Spring Boot service

Now that we have Apache NiFi configured, we can create the Spring Boot service. The service will be a simple web application that exposes a REST endpoint.

The endpoint will take a JSON payload and return a response. The response will be the same JSON payload with a generated ID.

Here's the code for the service:

```java
@RestController
public class DataController {

    @PostMapping("/data")
    public ResponseEntity<String> data(@RequestBody String data) {
        // Generate ID
        String id = UUID.randomUUID().toString();
        // Return response
        return ResponseEntity.ok().body(id);
    }
}
```

## Testing the dataflow

Now that we have the service up and running, we can test the dataflow. We'll use the NiFi GUI to send a JSON payload to the endpoint.

First, we'll create a new FlowFile:

![Create FlowFile](https://i.imgur.com/TGiukC5.png)

Next, we'll add the JSON payload:

![Add JSON Payload](https://i.imgur.com/l0v4tqO.png)

Finally, we'll trigger the Processor and check the response:

![Trigger Processor](https://i.imgur.com/JY4fZUO.png)

![Check Response](https://i.imgur.com/5AFw8gG.png)

As we can see, the response contains the generated ID.

## Conclusion

In this post, we've shown how to use Spring Boot with Apache NiFi. We've set up a simple dataflow that invokes a Spring Boot service and returns a response.

If you're interested in learning more about NiFi, be sure to check out the [official documentation](https://nifi.apache.org/docs.html).