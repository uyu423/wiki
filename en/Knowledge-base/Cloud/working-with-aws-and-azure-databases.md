---
title: Working with AWS and Azure Databases
description: 
published: true
date: 2023-02-17T04:18:22.173Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:17:31.093Z
---

- [Trabajar con bases de datos de AWS y Azure***Spanish** document is available*](/es/Knowledge-base/Cloud/working-with-aws-and-azure-databases)
{.links-list}
- [使用 AWS 和 Azure 数据库***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/working-with-aws-and-azure-databases)
{.links-list}
- [AWS 및 Azure 데이터베이스 작업***Korean** document is available*](/ko/Knowledge-base/Cloud/working-with-aws-and-azure-databases)
{.links-list}


# Working with AWS and Azure Databases

This guide provides an overview of working with databases in the cloud using Amazon Web Services (AWS) and Microsoft Azure. It covers the key differences between the two platforms, offers tips on designing cloud-based databases, and provides practical information and real-world solutions for IT development.

## AWS vs Azure Databases

There are several key differences between AWS and Azure databases that are important to consider when designing a cloud-based database solution.

### Cost

AWS offers a pay-as-you-go pricing model, with no upfront costs, while Azure charges a monthly fee.

### Storage

AWS offers unlimited storage for all database types, while Azure limits storage to 10 GB for SQL databases and 50 GB for NoSQL databases.

### Backup and recovery

AWS offers automatic backup and recovery for all database types, while Azure only offers this for SQL databases.

### Scalability

AWS offers horizontal scalability for all database types, while Azure only offers vertical scalability for SQL databases.

## Tips for designing cloud-based databases

There are several important factors to consider when designing a cloud-based database.

### Storage

Consider the storage requirements of the database and whether unlimited storage is necessary. If not, Azure may be a more cost-effective option.

### Backup and recovery

If automatic backup and recovery is not a requirement, Azure may be a more cost-effective option.

### Scalability

Consider the scalability requirements of the database. If horizontal scalability is not a requirement, Azure may be a more cost-effective option.

## Practical information and real-world solutions

The following sections provide practical information and real-world solutions for working with databases in the cloud.

### Creating a database in AWS

To create a database in AWS, use the Amazon RDS console.

1. On the Amazon RDS console, select **Create database**.

2. Select the database engine you want to use.

3. Specify the database configuration details.

4. Select the instance size.

5. Select the storage type.

6. Configure the security settings.

7. Review the database configuration.

8. Select **Create database**.

### Creating a database in Azure

To create a database in Azure, use the Azure portal.

1. On the Azure portal, select **Create a resource**.

2. Select **Databases**.

3. Select the database engine you want to use.

4. Specify the database configuration details.

5. Select the instance size.

6. Select the storage type.

7. Configure the security settings.

8. Review the database configuration.

9. Select **Create**.

### Connecting to a database in AWS

To connect to a database in AWS, use the Amazon RDS console.

1. On the Amazon RDS console, select the database you want to connect to.

2. Select the **Connections** tab.

3. Select **Create new connection**.

4. Specify the connection details.

5. Select **Create connection**.

6. Copy the connection string.

7. Paste the connection string into your application code.

### Connecting to a database in Azure

To connect to a database in Azure, use the Azure portal.

1. On the Azure portal, select the database you want to connect to.

2. Select the **Overview** tab.

3. Select **Show connection string**.

4. Copy the connection string.

5. Paste the connection string into your application code.

## External resources

For more information on working with AWS and Azure databases, see the following resources:

- [AWS Database Services](https://aws.amazon.com/databases/)
- [Azure Database Services](https://azure.microsoft.com/en-us/services/database/)
- [Designing Cloud-Based Relational Databases](https://aws.amazon.com/articles/17286/designing-cloud-based-relational-databases/)
- [Designing Cloud-Based NoSQL Databases](https://aws.amazon.com/articles/16989/designing-cloud-based-nosql-databases/)