---
title: AWS Elastic Beanstalk: Deploying and Scaling a Simple Web Application
description: 
published: true
date: 2023-02-09T12:18:17.267Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:18:10.846Z
---

- [AWS Elastic Beanstalk: implementación y escalado de una aplicación web simple***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-elastic-beanstalk-deploying-and-scaling-a-simple-web-application)
{.links-list}
- [AWS Elastic Beanstalk：部署和扩展简单的 Web 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-elastic-beanstalk-deploying-and-scaling-a-simple-web-application)
{.links-list}
- [AWS Elastic Beanstalk: 간단한 웹 애플리케이션 배포 및 확장***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-elastic-beanstalk-deploying-and-scaling-a-simple-web-application)
{.links-list}


# AWS Elastic Beanstalk: Deploying and Scaling a Simple Web Application

AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with popular web application frameworks such as Java, .NET, PHP, Node.js, Python, Ruby on Rails, and Docker on AWS.

Elastic Beanstalk reduces the complexity of managing the underlying resources of your web application, such as Amazon EC2 instances, load balancers, and Auto Scaling groups. It also provides a unified experience for monitoring your web application's health and performance.

In this article, we will show you how to deploy a simple web application on AWS Elastic Beanstalk. We will also demonstrate how easy it is to scale your web application horizontally (by adding more Amazon EC2 instances) and vertically (by increasing the size of your Amazon EC2 instances).

## Prerequisites

Before you begin, you will need the following:

* An AWS account. If you don't have one, you can create one for free [here](https://aws.amazon.com/getting-started/).
* A web application that can be deployed on an Amazon EC2 instance. For this article, we will use a simple Node.js web application.
* An Amazon S3 bucket to store your web application's source code.

## Deploying Your Web Application on AWS Elastic Beanstalk

To deploy your web application on AWS Elastic Beanstalk, create an Elastic Beanstalk environment and upload your application's source code to an Amazon S3 bucket. Then, Elastic Beanstalk will create an Amazon EC2 instance, load your web application on it, and configure it to serve traffic.

### Creating an Elastic Beanstalk Environment

To create an Elastic Beanstalk environment, open the Elastic Beanstalk console and click on "Create New Application".

![create-new-application](https://i.imgur.com/lpY7B0m.png)

Enter a name for your application and click "Create".

![enter-name-for-application](https://i.imgur.com/fvqQYxo.png)

On the next page, select the web server platform you want to use. For this article, we will use "Node.js".

![select-platform](https://i.imgur.com/LJNcuAO.png)

On the next page, select the Amazon EC2 instance type you want to use. For this article, we will use the "t2.micro" instance type.

![select-ec2-instance-type](https://i.imgur.com/VkzM8JZ.png)

On the next page, select the Amazon S3 bucket you want to use to store your web application's source code.

![select-s3-bucket](https://i.imgur.com/y4FtJjl.png)

Click "Deploy" to deploy your web application on AWS Elastic Beanstalk.

![deploy-application](https://i.imgur.com/BKW738u.png)

Elastic Beanstalk will now create an Amazon EC2 instance, load your web application on it, and configure it to serve traffic.

### Uploading Your Application's Source Code to Amazon S3

Now that you have created an Elastic Beanstalk environment, you need to upload your web application's source code to the Amazon S3 bucket you selected.

To do this, open the Amazon S3 console and select the bucket you want to use. Then, click on the "Upload" button.

![upload-button](https://i.imgur.com/TXrQ8oA.png)

On the next page, select the files you want to upload and click "Upload".

![select-files-to-upload](https://i.imgur.com/F3gG0CY.png)

Your web application's source code is now stored in the Amazon S3 bucket.

## Accessing Your Web Application

Once your web application has been deployed on AWS Elastic Beanstalk, you can access it by going to the environment's URL.

To find the environment's URL, open the Elastic Beanstalk console and click on the environment you created. Then, click on the "Overview" tab. The environment's URL is displayed at the top of the page.

![environment-url](https://i.imgur.com/vzMJO4F.png)

## Scaling Your Web Application

AWS Elastic Beanstalk makes it easy to scale your web application horizontally (by adding more Amazon EC2 instances) and vertically (by increasing the size of your Amazon EC2 instances).

To scale your web application horizontally, open the Elastic Beanstalk console and click on the environment you created. Then, click on the "Configuration" tab.

![configuration-tab](https://i.imgur.com/J3GfUxz.png)

On the next page, click on the "Capacity" tab.

![capacity-tab](https://i.imgur.com/pLJgJw6.png)

On the next page, select the number of Amazon EC2 instances you want to use and click "Apply".

![select-number-of-instances](https://i.imgur.com/X3XWqlr.png)

Elastic Beanstalk will now add the desired number of Amazon EC2 instances to your environment.

To scale your web application vertically, open the Elastic Beanstalk console and click on the environment you created. Then, click on the "Configuration" tab.

![configuration-tab](https://i.imgur.com/J3GfUxz.png)

On the next page, click on the "Capacity" tab.

![capacity-tab](https://i.imgur.com/pLJgJw6.png)

On the next page, select the Amazon EC2 instance type you want to use and click "Apply".

![select-ec2-instance-type](https://i.imgur.com/IHLv4jO.png)

Elastic Beanstalk will now reconfigure your environment to use the desired Amazon EC2 instance type.

## Monitoring Your Web Application

AWS Elastic Beanstalk provides a unified experience for monitoring your web application's health and performance.

To view your web application's health and performance metrics, open the Elastic Beanstalk console and click on the environment you created. Then, click on the "Monitoring" tab.

![monitoring-tab](https://i.imgur.com/VxKG0zJ.png)

On the next page, you will see a dashboard with various metrics about your web application, such as request count, response time, and CPU utilization.

![monitoring-dashboard](https://i.imgur.com/ZDGxK5M.png)

You can also view your web application's access logs and error logs. To do this, open the Elastic Beanstalk console and click on the environment you created. Then, click on the "Logs" tab.

![logs-tab](https://i.imgur.com/D4Y4lkO.png)

On the next page, you will see a list of your web application's access logs and error logs.

![logs](https://i.imgur.com/rAFwUOI.png)

## Updating Your Web Application

To update your web application, simply upload the updated version of your web application's source code to the Amazon S3 bucket you are using. Elastic Beanstalk will automatically detect the changes and deploy the updated version of your web application.

## Deleting Your Web Application

To delete your web application, open the Elastic Beanstalk console and click on the environment you created. Then, click on the "Actions" dropdown menu and select "Delete environment".

![delete-environment](https://i.imgur.com/VxJN4jO.png)

On the next page, enter a name for the environment you are about to delete and click "Delete".

![enter-environment-name](https://i.imgur.com/uvaYG4Y.png)

Elastic Beanstalk will now delete your web application.

## Conclusion

In this article, we have shown you how to deploy a simple web application on AWS Elastic Beanstalk. We have also demonstrated how easy it is to scale your web application horizontally (by adding more Amazon EC2 instances) and vertically (by increasing the size of your Amazon EC2 instances). Finally, we have also shown you how to monitor your web application's health and performance.