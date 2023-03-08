---
title: MySQL A Beginner's Guide for Planners and Marketers: 101
description: 
published: true
date: 2023-02-06T16:34:13.355Z
tags: 
editor: markdown
dateCreated: 2023-02-06T16:34:07.578Z
---

- [MySQL Una guía para principiantes para planificadores y especialistas en marketing: 101***Spanish** document is available*](/es/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-a-beginner-s-guide-for-planners-and-marketers-101)
{.links-list}
- [MySQL 规划人员和营销人员初学者指南：101***Chinese Simplified** document is available*](/zh/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-a-beginner-s-guide-for-planners-and-marketers-101)
{.links-list}
- [MySQL 플래너 및 마케터를 위한 초보자 가이드: 101***Korean** document is available*](/ko/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-a-beginner-s-guide-for-planners-and-marketers-101)
{.links-list}


MySQL is a powerful database management system used by web applications to store data. It is one of the most popular database systems in use today.

MySQL is a relational database management system (RDBMS). This means that it stores data in tables that are related to each other. For example, a table of customer data might be related to a table of order data.

MySQL is a free and open source software. This means that it is available for anyone to use and modify.

MySQL is a popular choice for web applications because it is fast, reliable, and easy to use.

In this guide, we will learn the basics of MySQL. We will cover the following topics:

- Installing MySQL
- Creating a Database
- Creating Tables
- Inserting Data
- Querying Data
- Backup and Restore

## Installing MySQL

MySQL can be installed on Windows, macOS, and Linux. It can also be installed on a server running another operating system, such as FreeBSD.

The easiest way to install MySQL on Windows is to use the MySQL Installer. This will install all of the components that we need, including the MySQL Server, MySQL Workbench, and the MySQL Notifier.

Download the MySQL Installer from the MySQL website:

https://dev.mysql.com/downloads/installer/

Run the installer and follow the prompts. When prompted, choose the following options:

- Install MySQL Server
- Configure MySQL Server now

The Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose a password for the MySQL root user. This is the user that has full access to all of the MySQL databases.

On the next page, choose the following options:

- Install As Windows Service
- Include Bin Directory in Windows PATH

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking
- Enable Strict Mode

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the following options:

- Install As Windows Service: Yes
- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Port Number: 3306
- Enable TCP/IP Networking: Yes
- Enable Strict Mode: Yes

On the next page, choose the following options:

- Default Character Set: utf8
- Install MySQL Test Suite: Yes

On the next page, choose the following options:

- MySQL Notifier: Not Required
- MySQL Workbench: Not Required

On the next page, choose the following options:

- Create An Anonymous Account: No
- Enable Strict Password Validation: No

On the next page, choose the following options:

- Run MySQL Server as a Windows Service: Yes
- Launch the MySQL Server automatically: Yes

On the next page, choose the following options:

- Include Bin Directory in Windows PATH: Yes

On the next page, choose the following options:

- Configure MySQL Server now: Yes

The MySQL Server Configuration Wizard will start. On the first page, choose the following options:

- Server Type: Development Machine
- Database Usage: Multifunctional Database
- Transactional Database Support: InnoDB
- Non-Transactional Database Support: MyISAM

On the next page, choose the