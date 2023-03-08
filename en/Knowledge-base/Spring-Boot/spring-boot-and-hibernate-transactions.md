---
title: Spring Boot and Hibernate Transactions
description: 
published: true
date: 2023-02-07T23:32:31.147Z
tags: 
editor: markdown
dateCreated: 2023-02-07T23:32:29.489Z
---

- [Transacciones Spring Boot e Hibernate***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-and-hibernate-transactions)
{.links-list}
- [Spring Boot 和 Hibernate 事务***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-and-hibernate-transactions)
{.links-list}
- [스프링 부트와 하이버네이트 트랜잭션***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-and-hibernate-transactions)
{.links-list}


# Spring Boot and Hibernate Transactions

Transactions are a fundamental part of any database-backed application. In a nutshell, a transaction is a way to bundle one or more database operations into an atomic unit. Either all of the operations succeed, or none of them do.

There are many benefits to using transactions, including:

- Ensuring data consistency: if any of the operations in a transaction fail, the entire transaction is rolled back and the database is left in its original state.
- Allowing for better performance: database operations within a transaction can be batched together, which reduces the number of round-trips to the database and can improve performance.
- Improving concurrency: by isolating transactions from each other, it's possible to prevent one transaction from interfering with another.

In this article, we'll take a look at how to use transactions with Spring Boot and Hibernate. We'll start with a quick overview of the different types of transactions, and then we'll dive into some code examples.

## Types of Transactions

There are two main types of transactions: local and global.

A local transaction is one that is managed by a single resource, such as a database. In a local transaction, all of the operations must be done on the same database. If any of the operations fail, the entire transaction is rolled back and the database is left in its original state.

A global transaction is one that is managed by multiple resources, such as a database and a message queue. Global transactions are more complex than local transactions, but they offer the benefit of being able to roll back the entire transaction even if one of the resources fails.

## Using Transactions with Spring Boot

Spring Boot provides first-class support for transactions. In fact, transactions are so important that Spring Boot application will not start if it detects that the database is not configured for transactions.

When configuring transactions in Spring Boot, there are three things to keep in mind:

- The @Transactional annotation: this annotation is used to mark methods that should be run in a transaction.
- The PlatformTransactionManager: this is the component that actually manages the transaction. Spring Boot will automatically configure a PlatformTransactionManager bean for you if it detects that you're using a database.
- The transaction isolation level: this is the level of isolation that you want for your transactions. The different levels of isolation offer different guarantees about the consistency of your data.

The most common way to configure transactions in Spring Boot is to use the @Transactional annotation. This annotation can be added to a class or a method. When added to a class, it applies to all of the methods in the class. When added to a method, it only applies to that method.

The @Transactional annotation has a few optional parameters that can be used to customize its behavior. The most important of these is the isolation level. The isolation level is used to control how strictly the database enforces the ACID properties.

There are four isolation levels that are commonly used:

- READ UNCOMMITTED: This is the least strict isolation level. It allows concurrent transactions to read data that has not been committed by other transactions. This can lead to data inconsistency, but it offers the best performance.
- READ COMMITTED: This isolation level is more strict than READ UNCOMMITTED. It only allows concurrent transactions to read data that has been committed by other transactions. This prevents data inconsistency, but it can lead to performance problems.
- REPEATABLE READ: This isolation level is even more strict than READ COMMITTED. It only allows concurrent transactions to read data that has been committed by other transactions, and it also prevents them from reading data that has been modified by other transactions. This offers the best data consistency, but it can lead to performance problems.
- SERIALIZABLE: This is the most strict isolation level. It prevents concurrent transactions from reading or writing data that has been modified by other transactions. This offers the best data consistency, but it can lead to performance problems.

It's important to choose the right isolation level for your application. If you choose an isolation level that is too strict, you may see performance problems. If you choose an isolation level that is too lax, you may see data inconsistencies.

## Using Transactions with Hibernate

Hibernate is a popular ORM tool that is often used in conjunction with Spring. Hibernate also supports transactions, and it offers a few different ways to configure them.

The most common way to configure transactions in Hibernate is to use the @Transactional annotation. This annotation can be added to a class or a method. When added to a class, it applies to all of the methods in the class. When added to a method, it only applies to that method.

The @Transactional annotation has a few optional parameters that can be used to customize its behavior. The most important of these is the isolation level. The isolation level is used to control how strictly the database enforces the ACID properties.

Hibernate also supports programmatic transactions. This means that you can configure the transaction in code, rather than using an annotation. This is generally not recommended, as it makes the code more difficult to understand and maintain.

## Conclusion

In this article, we've looked at how to use transactions with Spring Boot and Hibernate. We've seen how to configure transactions using the @Transactional annotation, and we've also seen how to choose the right isolation level for our needs.