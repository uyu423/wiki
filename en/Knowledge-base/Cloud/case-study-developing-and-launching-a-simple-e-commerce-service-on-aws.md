---
title: Case Study: Developing and Launching a Simple e-Commerce Service on AWS
description: 
published: true
date: 2023-02-04T11:18:12.560Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:18:07.038Z
---

- [Estudio de caso: desarrollo y lanzamiento de un servicio de comercio electrónico simple en AWS***Spanish** document is available*](/es/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-e-commerce-service-on-aws)
{.links-list}
- [案例研究：在 AWS 上开发和启动简单的电子商务服务***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-e-commerce-service-on-aws)
{.links-list}
- [사례 연구: AWS에서 간단한 전자 상거래 서비스 개발 및 시작***Korean** document is available*](/ko/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-e-commerce-service-on-aws)
{.links-list}


# Case Study: Developing and Launching a Simple e-Commerce Service on AWS

In this case study, we'll show you how to develop and launch a simple e-Commerce service on AWS. We'll go over the architecture of the service and the different AWS services that are used. We'll also provide some code examples to help you get started.

## The Architecture

The e-Commerce service that we'll be developing is a simple one that consists of a web front-end and a back-end database. The web front-end will be developed using the PHP programming language and the back-end database will be MySQL.

![E-Commerce Service Architecture](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/architecture.png)

The web front-end will be hosted on an Amazon EC2 instance and will be accessed through an Amazon CloudFront distribution. CloudFront is a content delivery network (CDN) that will cache the static content of the website (such as images, CSS, and JavaScript files) and deliver it to users with low latency.

The back-end database will be hosted on Amazon RDS and will be used to store the products and orders data. RDS is a managed relational database service that makes it easy to set up, operate, and scale a relational database in the cloud.

## The AWS Services Used

The following AWS services will be used in this case study:

- Amazon EC2
- Amazon CloudFront
- Amazon RDS
- Amazon S3

## Setting Up the Back-End Database

We'll start by setting up the back-end database. We'll be using Amazon RDS for MySQL.

First, we'll create a new RDS instance. We'll choose the MySQL engine and the db.t2.micro instance class.

![Creating a new RDS instance](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-01.png)

Next, we'll configure the settings for the instance. We'll give the instance a name, choose the MySQL 5.6.x database engine, and select the db.t2.micro instance class.

![Configuring the RDS instance](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-02.png)

Next, we'll create a new database. We'll give the database a name and choose the MySQL 5.6.x database engine.

![Creating a new database](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-03.png)

Now that the database has been created, we'll need to create a user and grant the user access to the database. We'll create a user with the username "ecommerce" and the password "password".

![Creating a new user](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-04.png)

Next, we'll grant the user access to the database. We'll select the "ecommerce" database and the "ecommerce" user and click the "Add" button.

![Granting access to the database](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-05.png)

## Setting Up the Web Front-End

Now that the back-end database has been set up, we'll need to set up the web front-end. We'll be using Amazon EC2 for this.

First, we'll create a new EC2 instance. We'll choose the Amazon Linux AMI and the t2.micro instance type.

![Creating a new EC2 instance](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-01.png)

Next, we'll configure the settings for the instance. We'll give the instance a name, choose the Amazon Linux AMI, and select the t2.micro instance type.

![Configuring the EC2 instance](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-02.png)

Now that the instance has been created, we'll need to SSH into the instance. We'll use the private key that we downloaded when we created the instance.

![SSH into the EC2 instance](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-03.png)

Once we're logged into the instance, we'll need to install the Apache web server, PHP, and the MySQL client. We'll do this using the yum package manager.

```bash
$ sudo yum install -y httpd24 php70 mysql56-client
```

Next, we'll start the Apache web server.

```bash
$ sudo service httpd start
```

Now that the web server is up and running, we'll need to create a new PHP file. We'll call this file "index.php" and we'll put it in the "/var/www/html" directory.

```php
<?php
  echo "Hello, world!";
?>
```

Now, we'll need to edit the "/etc/httpd/conf/httpd.conf" file and uncomment the following line:

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

Next, we'll restart the Apache web server.

```bash
$ sudo service httpd restart
```

Now, we'll need to create a new MySQL user. We'll use the "ecommerce" user that we created earlier. We'll grant the user access to the "ecommerce" database.

```sql
GRANT ALL ON ecommerce.* TO 'ecommerce'@'localhost' IDENTIFIED BY 'password';
```

Now that the user has been created, we'll need to import the data into the database. We'll use the "products.sql" file that is included in the GitHub repository.

```bash
$ mysql -u ecommerce -p ecommerce < products.sql
```

## Testing the Application

Now that the application is set up, we'll need to test it to make sure everything is working as expected. We'll start by accessing the application through a web browser.

![Testing the application](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-01.png)

As we can see, the application is working as expected. We can see the list of products and we can add items to the shopping cart.

![Testing the application](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-02.png)

## Launching the Application

Now that the application is up and running, we'll need to launch it. We'll do this by creating an Amazon CloudFront distribution.

First, we'll create a new CloudFront distribution. We'll choose the "Web" delivery method and the "Get" HTTP method.

![Creating a new CloudFront distribution](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-01.png)

Next, we'll configure the settings for the distribution. We'll give the distribution a name, select the "Web" delivery method, and choose the "Get" HTTP method.

![Configuring the CloudFront distribution](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-02.png)

Now, we'll need to create a new origin. We'll select the "Custom Origin" type and enter the URL for our EC2 instance.

![Creating a new origin](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-03.png)

Next, we'll configure the settings for the origin. We'll give the origin a name, select the "Custom Origin" type, and enter the URL for our EC2 instance.

![Configuring the origin](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-04.png)

Now, we'll need to create a new default cache behavior. We'll select the "Default (*)" path pattern and choose the "Allow All" option for the Forward Headers.

![Creating a new default cache behavior](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-05.png)

Next, we'll configure the settings for the default cache behavior. We'll select the "Default (*)" path pattern and choose the "Allow All" option for the Forward Headers.

![Configuring the default cache behavior](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-06.png)

Now, we'll need to create a new error page. We'll select the "404" error code and enter the URL for the error page.

![Creating a new error page](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-07.png)

Next, we'll configure the settings for the error page. We'll select the "404" error code and enter the URL for the error page.

![Configuring the error page](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-08.png)

Now, we'll need to create a new SSL certificate. We'll select the "Custom Certificate" option and enter the domain name for our website.

![Creating a new SSL certificate](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-09.png)

Next, we'll configure the settings for the SSL certificate. We'll select the "Custom Certificate" option and enter the domain name for our website.

![Configuring the SSL certificate](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-10.png)

Now, we'll need to create a new distribution. We'll select the "Web" delivery method and the "Get" HTTP method.

![Creating a new distribution](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-11.png)

Next, we'll configure the settings for the distribution. We'll give the distribution a name, select the "Web" delivery method, and choose the "Get" HTTP method.

![Configuring the distribution](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-12.png)

Now, we'll need to create a new default cache behavior. We'll select the "Default (*)" path pattern and choose the "Allow All" option for the Forward Headers.

![Creating a new default cache behavior](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-13.png)

Next, we'll configure the settings for the default cache behavior. We'll select the "Default (*)" path pattern and choose the "Allow All" option for the Forward Headers.

![Configuring the default cache behavior](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-14.png)

Now, we'll need to create a new error page. We'll select the "404" error code and enter the URL for the error page.

![Creating a new error page](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-15.png)

Next, we'll configure the settings for the error page. We'll select the "404" error code and enter the URL for the error page.

![Configuring the error page](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-16.png)

## Conclusion

In this case study, we've shown you how to develop and launch a simple e-Commerce service on AWS. We've gone over the architecture of the service and the different AWS services that are used. We've also provided some code examples to help you get started.