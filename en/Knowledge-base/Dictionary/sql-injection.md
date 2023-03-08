---
title: SQL Injection
description: 
published: true
date: 2023-02-07T07:17:48.554Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:17:42.089Z
---

- [SQL Injection***Japanese** document is available*](/ja/Knowledge-base/Dictionary/sql-injection)
{.links-list}
- [SQL Injection***Spanish** document is available*](/es/Knowledge-base/Dictionary/sql-injection)
{.links-list}
- [SQL Injection***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/sql-injection)
{.links-list}
- [SQL Injection***Korean** document is available*](/ko/Knowledge-base/Dictionary/sql-injection)
{.links-list}


# Overview
SQL Injection is a type of cyber attack that involves malicious code being inserted into a database query. It is used to gain access to or modify sensitive data stored in a database.

# Description
SQL Injection is a form of attack that exploits vulnerabilities in database queries. It is a type of injection attack where malicious SQL code is inserted into a query to gain access to or modify sensitive data. The attacker can use this access to steal data, modify data, or even delete data from the database.

SQL Injection attacks can be used to bypass authentication mechanisms, execute arbitrary code, and even gain access to the underlying operating system. The attacker can also use SQL Injection to modify database records, such as changing a user's password or deleting records.

SQL Injection attacks are usually performed by sending malicious input to a web application. This input is then processed by the application and passed to the database. If the application does not properly validate the input, the malicious code can be executed by the database.

# History
SQL Injection attacks have been around since the early days of the internet. In 1998, the first publically reported SQL Injection attack occurred on a web application developed by a company called Security Dynamics. Since then, SQL Injection attacks have become increasingly common and sophisticated.

# Features
SQL Injection attacks are typically performed by sending malicious input to a web application. The malicious input is then processed by the application and passed to the database. If the application does not properly validate the input, the malicious code can be executed by the database.

SQL Injection attacks can be used to bypass authentication mechanisms, execute arbitrary code, and even gain access to the underlying operating system. The attacker can also use SQL Injection to modify database records, such as changing a user's password or deleting records.

# Example
An example of an SQL Injection attack is an attacker sending malicious input to a web application. The malicious input is then processed by the application and passed to the database. If the application does not properly validate the input, the malicious code can be executed by the database.

For example, an attacker could send the following input to a web application:

```
SELECT * FROM users WHERE username='admin' OR '1'='1'
```

This input would cause the application to execute the following query:

```
SELECT * FROM users WHERE username='admin' OR '1'='1'
```

This query would return all of the users in the database, regardless of their username.

# Pros and Cons
SQL Injection attacks have both pros and cons. On the one hand, they can be used to gain access to sensitive data or modify records in the database. On the other hand, they can also be used to cause significant damage to a system, such as deleting data or executing arbitrary code.

# Controversy
SQL Injection attacks are a controversial topic in the security community. Some argue that they are a necessary evil, as they can be used to gain access to sensitive data and modify records in the database. Others argue that they should be avoided at all costs, as they can be used to cause significant damage to a system.

# Related Technology
SQL Injection attacks are related to other types of cyber attacks, such as Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF). These attacks can also be used to gain access to sensitive data or modify records in the database.

# Digression
SQL Injection attacks are a type of attack that can be used to gain access to or modify sensitive data stored in a database. They have been around since the early days of the internet and have become increasingly common and sophisticated. While they can be used to gain access to sensitive data or modify records in the database, they can also be used to cause significant damage to a system.

# Others
SQL Injection attacks can be prevented by properly validating user input. This can be done by using prepared statements and parameterized queries, which ensure that the user-supplied input is treated as data and not as executable code. Additionally, web applications should be tested for vulnerabilities and patched regularly to prevent SQL Injection attacks.