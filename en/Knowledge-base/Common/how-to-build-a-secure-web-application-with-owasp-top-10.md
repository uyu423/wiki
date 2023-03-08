---
title: How to Build a Secure Web Application with OWASP Top 10
description: 
published: true
date: 2023-02-27T06:32:45.192Z
tags: 
editor: markdown
dateCreated: 2023-02-27T06:32:37.590Z
---

- [OWASP Top 10으로 보안 웹 애플리케이션을 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-secure-web-application-with-owasp-top-10)
{.links-list}


# How to Build a Secure Web Application with OWASP Top 10

The Open Web Application Security Project (OWASP) Top 10 is a classification of the most common attacks on the web. It has been updated every few years since its inception in 2004, with the most recent version released in 2017.

Despite its name, the OWASP Top 10 is not a list of the 10 most common attacks. Rather, it is a prioritized list of security risks that web application developers should be aware of. The list is meant to be used as a guide for developers to help them build more secure applications.

## Injection

Injection flaws allow attackers to execute malicious SQL queries or code in the back-end database. This can be used to delete or modify data, or even gain access to sensitive information.

To prevent injection flaws, developers should:

- Use parameterized queries instead of concatenating user input into SQL queries
- Use stored procedures
- Escape special characters in user input

## Broken Authentication and Session Management

Broken authentication and session management flaws allow attackers to gain access to resources or data they should not have access to. This can be done by stealing cookies, session IDs, or using default or easily guessed passwords.

To prevent broken authentication and session management flaws, developers should:

- Use strong passwords and password policies
- Use two-factor authentication
- Use session timeouts
- Invalidate session ID after logout
- Use SSL/TLS

## Cross-Site Scripting (XSS)

Cross-site scripting (XSS) flaws allow attackers to inject malicious code into webpages, which is then executed by unsuspecting users who visit the page. This can be used to steal information, like passwords and cookies, or to redirect users to malicious sites.

To prevent XSS flaws, developers should:

- Escape special characters in user input
- Use a web application firewall (WAF)

## Broken Access Control

Broken access control flaws allow unauthorized users to access or modify data they should not have access to. This can be done by bypassing authentication or authorization checks, or by changing the URL to access a restricted resource.

To prevent broken access control flaws, developers should:

- Use proper authentication and authorization controls
- Use least privilege principle
- Avoid using wildcard permissions

## Security Misconfiguration

Security misconfiguration is a broad category of flaws that occur when web applications are not properly configured. This can include leaving the default configuration, leaving servers and applications exposed, or not properly setting file permissions.

To prevent security misconfiguration flaws, developers should:

- Follow best practices for web application security
- Use a web application firewall (WAF)
- Harden the server configuration

## Insecure Cryptographic Storage

Insecure cryptographic storage flaws occur when sensitive data, like passwords and credit card numbers, are not properly encrypted. This can lead to the data being compromised if the database is breached.

To prevent insecure cryptographic storage flaws, developers should:

- Use strong encryption algorithms
- Use proper key management

## Insufficient Authorization and Authentication

Insufficient authorization and authentication flaws occur when web applications do not properly check if a user is authorized to access a resource or perform an action. This can be done by not properly checking permissions, or by using easily guessed passwords.

To prevent insufficient authorization and authentication flaws, developers should:

- Use strong passwords and password policies
- Use two-factor authentication
- Use proper authorization controls

## Insufficient Cryptography

Insufficient cryptography flaws occur when web applications use weak encryption algorithms or do not properly encrypt sensitive data. This can lead to the data being compromised if the database is breached.

To prevent insufficient cryptographic storage flaws, developers should:

- Use strong encryption algorithms
- Use proper key management

## Tampering with Data

Data tampering flaws allow attackers to modify data, which can be used to delete data, change prices, or add counterfeit items to a shopping cart.

To prevent data tampering flaws, developers should:

- Use digital signatures
- Hash sensitive data
- Use proper encryption

## Cross-Site Request Forgery (CSRF)

Cross-site request forgery (CSRF) flaws allow attackers to execute actions on behalf of a user without their knowledge or consent. This can be done by tricking the user into clicking a malicious link or loading a malicious webpage.

To prevent CSRF flaws, developers should:

- Use proper authentication and authorization controls
- Use CSRF tokens
- Use same-site cookies

## External Resources

- [https://www.owasp.org/index.php/Top\_10-2017\_Top\_10](https://www.owasp.org/index.php/Top_10-2017_Top_10)
- [https://www.owasp.org/index.php/SQL\_Injection](https://www.owasp.org/index.php/SQL_Injection)
- [https://www.owasp.org/index.php/Broken\_Authentication\_and\_Session\_Management](https://www.owasp.org/index.php/Broken_Authentication_and_Session_Management)
- [https://www.owasp.org/index.php/Cross-Site\_Scripting\_(XSS)](https://www.owasp.org/index.php/Cross-Site_Scripting_(XSS))
- [https://www.owasp.org/index.php/ Broken\_Access\_Controls](https://www.owasp.org/index.php/Broken_Access_Controls)
- [https://www.owasp.org/index.php/Security\_Misconfiguration](https://www.owasp.org/index.php/Security_Misconfiguration)
- [https://www.owasp.org/index.php/ Insufficient\_Authorization\_and\_Authentication](https://www.owasp.org/index.php/Insufficient_Authorization_and_Authentication)
- [https://www.owasp.org/index.php/ Insufficient\_Cryptography](https://www.owasp.org/index.php/Insufficient_Cryptography)
- [https://www.owasp.org/index.php/ Tampering\_with\_Data](https://www.owasp.org/index.php/Tampering_with_Data)
- [https://www.owasp.org/index.php/ Cross-Site\_Request\_Forgery\_(CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))