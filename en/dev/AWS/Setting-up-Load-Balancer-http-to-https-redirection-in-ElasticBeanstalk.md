---
title: Setting up Load Balancer http to https redirection in ElasticBeanstalk
description: Surprisingly, the http(80) -> https(443) redirect cannot be set in the EB configuration...;
published: true
date: 2023-02-17T18:00:25.712Z
tags: aws, ec2, elasticbeanstalk
editor: markdown
dateCreated: 2022-12-24T21:04:21.403Z
---

- [ElasticBeanstalk에서 Load Balancer http to https 리다이렉션 설정하기***Korean** version of this document is available*](/ko/dev/AWS/Setting-up-Load-Balancer-http-to-https-redirection-in-ElasticBeanstalk)
{.links-list}

> Assume that you are using an Application Load Balancer.

## You can't do that in ElasticBeanstalk configuration.

![스크린샷_2022-11-27_오전_5.23.05.png](/스크린샷_2022-11-27_오전_5.23.05.png =800x)

- In the load balancer settings of the ElasticBeanstalk configuration, there is no http -> https redirection setting even if you wash your eyes and look for it.

> But let's set the port 80 and 443 here
{.is-info}


## The solution is to manually configure EC2 - Load Balancer.

- Go to `EC2 - Load Balancer` and find the load balancer being used in the ElasticBeanstalk environment you want to configure.
- Move to the 'Listener' item of the found load balancer.
- 80 Change the port listener setting.
- Remove the `Forward` setting set as the default value, and set `Redirect` as a new one.
- You can set it as below.

![스크린샷_2022-11-27_오전_5.30.29.png](/스크린샷_2022-11-27_오전_5.30.29.png =600x)

---

- I don't know what ElasticBeanstalk doesn't have http -> https Redirect settings :(