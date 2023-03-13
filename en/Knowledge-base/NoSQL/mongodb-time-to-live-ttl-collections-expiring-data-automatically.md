---
title: MongoDB Time-To-Live (TTL) Collections: Expiring Data Automatically
description: 
published: true
date: 2023-03-13T22:33:10.958Z
tags: 
editor: markdown
dateCreated: 2023-03-13T22:33:10.958Z
---

- [MongoDB TTL(Time-To-Live) 컬렉션: 자동으로 데이터 만료***Korean** document is available*](/ko/Knowledge-base/NoSQL/mongodb-time-to-live-ttl-collections-expiring-data-automatically)
{.links-list}

## Introduction

As a developer, dealing with expired data can be a real headache. There are various approaches to handle this issue, such as creating a script to remove the expired data and scheduling it to run periodically. However, these solutions can be time-consuming and error-prone. MongoDB provides a built-in feature called Time-To-Live (TTL) collections that automatically removes expired documents from a collection. In this article, we will explore MongoDB TTL collections in detail and learn how to use them to simplify the task of removing expired data.

## What are MongoDB TTL Collections?

MongoDB TTL collections are a way to automatically remove documents from a collection after a certain amount of time has passed since their creation or update. This feature can be really useful in cases where we have data that is only relevant for a certain period of time, like session data, log data, or temporary data.

To use this feature, we need to create an index on the collection with the `expireAfterSeconds` option set to the number of seconds after which the document should expire. Once this is done, MongoDB will automatically remove expired documents from the collection once every minute.

## Creating TTL Indexes

To create a TTL index, we can use the `createIndex()` method on the collection object. The index should be created on the field that contains the expiration time of the documents.

Suppose we have a collection called `logs` that contains log data and we want to automatically remove documents that are older than a day. We can create a TTL index on the `createdAt` field with an expiration time of 86400 (which is the number of seconds in a day) using the following command:

```{javascript}
db.logs.createIndex({createdAt: 1}, {expireAfterSeconds: 86400})
```

This will create a TTL index on the `createdAt` field of the `logs` collection, and MongoDB will remove any document whose `createdAt` field is older than 24 hours.

## Updating TTL Indexes

If we want to update the TTL index, for example, to change the expiration time, we need to drop the existing index and create a new one with the updated options.

To drop an index, we can use the `dropIndex()` method on the collection object. Suppose we want to update the `logs` collection to remove documents that are older than a week. We can drop the existing TTL index using the following command:

```{javascript}
db.logs.dropIndex({createdAt: 1})
```

Once the index is dropped, we can create a new TTL index with the updated options:

```{javascript}
db.logs.createIndex({createdAt: 1}, {expireAfterSeconds: 604800})
```

This will create a new TTL index on the `createdAt` field of the `logs` collection, and MongoDB will remove any document whose `createdAt` field is older than 7 days.

## Considerations

There are a few things to consider when working with MongoDB TTL collections:

### Time Zone

MongoDB uses the Coordinated Universal Time (UTC) time zone to compare the expiration time of documents with the current time. This means that if the expiration time is set to a local time, we need to convert it to UTC before creating the index.

### Precision

MongoDB performs TTL expiration checks every minute, which means that documents may expire up to 60 seconds after the specified expiration time. If precise expiration is required, we can use the `expireAfter` field instead of the `expireAfterSeconds` option to set the exact expiration time for each document.

### Performance

TTL indexes can have an impact on the performance of our application, especially when dealing with large collections. This is because MongoDB needs to perform periodic scans of the collection to remove expired documents. To minimize the impact on performance, we can consider creating the TTL index on a subset of the collection or using a capped collection.

## Conclusion

In this article, we have explored MongoDB TTL collections and how they can be used to automatically remove expired documents from a collection. We have seen how to create and update TTL indexes and discussed some considerations when working with them. By using TTL collections, we can simplify the task of removing expired data and focus on more important aspects of our application.

## External Resources

- [TTL Indexes - MongoDB Documentation](https://docs.mongodb.com/manual/core/index-ttl/)
- [MongoDB TTL Indexes: How They Work](https://www.mongodb.com/blog/post/mongodb-time-to-live-ttl-collections-how-they-work)
- [MongoDB Performance Best Practices](https://docs.mongodb.com/manual/administration/performance-best-practices/)