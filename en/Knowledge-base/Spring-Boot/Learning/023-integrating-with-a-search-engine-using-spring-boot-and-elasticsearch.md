---
title: 023: Integrating with a search engine using Spring Boot and Elasticsearch
description: 
published: true
date: 2023-02-03T15:32:41.452Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:32:36.514Z
---

- [023: Integración con un motor de búsqueda usando Spring Boot y Elasticsearch***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/023-integrating-with-a-search-engine-using-spring-boot-and-elasticsearch)
{.links-list}
- [023：使用 Spring Boot 和 Elasticsearch 与搜索引擎集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/023-integrating-with-a-search-engine-using-spring-boot-and-elasticsearch)
{.links-list}
- [023: Spring Boot 및 Elasticsearch를 사용하여 검색 엔진과 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/023-integrating-with-a-search-engine-using-spring-boot-and-elasticsearch)
{.links-list}


# Integrating with a search engine using Spring Boot and Elasticsearch

In this post, we'll learn how to integrate a Spring Boot application with a search engine using Elasticsearch.

## What is Elasticsearch?

Elasticsearch is a distributed, RESTful search and analytics engine built on Apache Lucene. It provides a powerful set of features for implementing full-text search and analytics on large data sets.

## Why use Elasticsearch?

Elasticsearch is a popular choice for implementing a search engine due to its ease of use, scalability, and performance.

## Setting up Elasticsearch

Before we can start using Elasticsearch, we need to set it up.

There are two ways to set up Elasticsearch:

1. Download and install Elasticsearch from the [official website](https://www.elastic.co/downloads/elasticsearch).
2. Use the [Docker image](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html).

We'll use the Docker image in this post.

## Running Elasticsearch

To run the Elasticsearch Docker image, use the following command:

```
$ docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.4.0
```

This will start a container running Elasticsearch 7.4.0 on port 9200.

## Connecting to Elasticsearch

Now that Elasticsearch is up and running, we can start using it in our Spring Boot application.

To connect to Elasticsearch from Spring Boot, we need to add the following dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

This dependency will add the necessary libraries for connecting to and using Elasticsearch in our application.

## Configuring Elasticsearch

Once we have the `spring-boot-starter-data-elasticsearch` dependency in our project, we need to configure Elasticsearch.

We can configure Elasticsearch by adding the following properties to our `application.properties` file:

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=docker-cluster
```

This will configure our application to connect to the Elasticsearch cluster running on `localhost:9300`.

## Creating a Spring Boot application

Now that we have Elasticsearch set up and configured, we can create a Spring Boot application that uses it.

We'll start by creating a `User` class:

```java
@Document(indexName = "user", type = "user")
public class User {

    @Id
    private String id;

    private String name;

    private Integer age;

    // getters and setters
}
```

This class represents a user in our application. Notice that we've annotated it with `@Document`. This tells Spring Data Elasticsearch that this is a document that should be indexed in Elasticsearch.

We've also annotated the `id` field with `@Id`. This tells Spring Data Elasticsearch that this is the unique identifier for this document.

Next, we'll create a `UserRepository` interface:

```java
public interface UserRepository extends ElasticsearchRepository<User, String> {

}
```

This interface extends `ElasticsearchRepository`, which provides us with a powerful set of methods for interacting with Elasticsearch.

Finally, we'll create a `UserService` class:

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public void saveUser(User user) {
        userRepository.save(user);
    }

    public void deleteUser(User user) {
        userRepository.delete(user);
    }

    public Iterable<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User getUserById(String id) {
        return userRepository.findById(id).orElse(null);
    }
}
```

This class provides methods for creating, retrieving, and deleting users in our application. Notice that we've annotated it with `@Service`. This tells Spring that this is a service bean that should be managed by the Spring container.

We've also annotated the `userRepository` field with `@Autowired`. This tells Spring to inject an instance of `UserRepository` into this field when the bean is created.

## Creating and indexing documents

Now that we have our Spring Boot application set up, we can start creating and indexing documents in Elasticsearch.

We'll start by creating a `User` instance:

```java
User user = new User();
user.setId("1");
user.setName("John Doe");
user.setAge(20);
```

Next, we'll save this user to our database:

```java
userService.saveUser(user);
```

This will save the user to our database and index the document in Elasticsearch.

## Searching for documents

Once we have documents indexed in Elasticsearch, we can start searching for them.

Elasticsearch provides a powerful query DSL (domain-specific language) for searching for documents.

We can use the `search()` method on our `UserRepository` to execute a search query:

```java
SearchQuery searchQuery = new NativeSearchQueryBuilder()
        .withQuery(QueryBuilders.queryStringQuery("John Doe"))
        .build();

List<User> users = userRepository.search(searchQuery).getContent();
```

This query will search for all documents that contain the phrase "John Doe".

The `search()` method returns a `SearchResponse` object, which contains the results of the search query. We can use the `getContent()` method to get a list of `User` objects that match the search query.

## Updating documents

We can also use Elasticsearch to update documents.

To update a document, we first need to retrieve it from the database:

```java
User user = userService.getUserById("1");
```

Next, we'll update the document:

```java
user.setAge(21);
```

Finally, we'll save the updated document to the database:

```java
userService.saveUser(user);
```

This will update the document in the database and in Elasticsearch.

## Deleting documents

We can also use Elasticsearch to delete documents.

To delete a document, we first need to retrieve it from the database:

```java
User user = userService.getUserById("1");
```

Next, we'll delete the document:

```java
userService.deleteUser(user);
```

This will delete the document from the database and from Elasticsearch.

## Conclusion

In this post, we've learned how to integrate a Spring Boot application with a search engine using Elasticsearch. We've also learned how to create, index, update, and delete documents in Elasticsearch.