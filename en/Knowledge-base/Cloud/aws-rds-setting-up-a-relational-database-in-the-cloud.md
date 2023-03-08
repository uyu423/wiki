---
title: AWS RDS: Setting Up a Relational Database in the Cloud
description: 
published: true
date: 2023-02-17T18:17:33.371Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:25:34.337Z
---

- [AWS RDS: 클라우드에서 관계형 데이터베이스 설정***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-rds-setting-up-a-relational-database-in-the-cloud)
{.links-list}
- [AWS RDS: クラウドでのリレーショナル データベースのセットアップ***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/aws-rds-setting-up-a-relational-database-in-the-cloud)
{.links-list}
- [AWS RDS：在云中设置关系数据库***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-rds-setting-up-a-relational-database-in-the-cloud)
{.links-list}



# AWS RDS: Setting Up a Relational Database in the Cloud

AWS Relational Database Service (RDS) is a managed database service that supports multiple database engines, including MySQL, MariaDB, Oracle, Microsoft SQL Server, and PostgreSQL. RDS makes it easy to set up, operate, and scale a relational database in the cloud.

In this article, we will walk you through the process of setting up a MySQL database on AWS RDS. We will also provide some tips on how to secure your database, as well as how to troubleshoot common issues that you may encounter.

## Creating a MySQL Database on AWS RDS

Before you can create a MySQL database on AWS RDS, you will need to create an Amazon Web Services (AWS) account. If you do not already have an AWS account, you can create one at http://aws.amazon.com/.

Once you have created your AWS account, you can launch the RDS console by going to the Amazon RDS home page and clicking on the "Launch DB Instance" button.

On the next page, you will need to select the "MySQL" engine and then choose the "Standard Create" option.

![standard create option](https://i.imgur.com/1ly7YUV.png)

On the next page, you will need to provide a name for your database instance, as well as the username and password that you will use to connect to the database.

![database instance](https://i.imgur.com/LxhmJN7.png)

You will also need to choose the size of your database instance, as well as the region where it will be located. For this example, we will use the "db.t2.micro" instance type and the "US East (N. Virginia)" region.

![database instancetype](https://i.imgur.com/rVg0U6Z.png)

On the next page, you will need to choose whether you want to enable billing alerts and tagging for your database instance. For this example, we will enable both options.

![database instance tagging](https://i.imgur.com/eiU3Qnl.png)

On the next page, you will need to specify the settings for your database instance. For this example, we will use the default settings.

![database instance settings](https://i.imgur.com/xk0tU8S.png)

On the next page, you will need to review the settings for your database instance and then click on the "Launch DB Instance" button.

![database instance review](https://i.imgur.com/TGiukmn.png)

Your database instance will now be created and will be available in a few minutes.

## Connecting to Your MySQL Database

Once your database instance has been created, you can connect to it using any MySQL-compatible client, such as the MySQL Workbench. To connect to your database instance, you will need to provide the following information:

- **Endpoint**: This is the URL of your database instance. You can find this information in the "Connectivity & security" section of the RDS console.

- **Port**: The default port for MySQL is 3306.

- **Username**: The username that you specified when you launched your database instance.

- **Password**: The password that you specified when you launched your database instance.

![database instance connectivity](https://i.imgur.com/CnjNJTV.png)

You should now be able to connect to your database and run SQL queries.

## Securing Your MySQL Database

It is important to secure your MySQL database to prevent unauthorized access. AWS RDS makes it easy to secure your database by providing a firewall that can be used to control access to your database instance.

To add a new rule to the firewall, go to the "Security groups" section of the RDS console and click on the "Edit inbound rules" button.

![database instance security groups](https://i.imgur.com/Jz4U3vN.png)

On the next page, you will need to specify the type of rule, as well as the source and destination for the rule. For this example, we will allow access to our database instance from any source (0.0.0.0/0).

![database instance security groups rule](https://i.imgur.com/taY0TGi.png)

You can now click on the "Save rules" button to save your changes.

## Troubleshooting MySQL Database Issues

There are a few common issues that you may encounter when setting up or using your MySQL database on AWS RDS.

- **Connection issues**: If you are having trouble connecting to your database, make sure that you are using the correct endpoint, port, and credentials. You can also try temporarily disabling the firewall to see if that is the cause of the issue.

- **Slow performance**: If you are experiencing slow performance, make sure that you are using the correct instance type for your workload. You may also need to increase the size of your database instance.

- **1040 error**: If you are receiving the "1040 - Too many connections" error, you will need to increase the size of your database instance.