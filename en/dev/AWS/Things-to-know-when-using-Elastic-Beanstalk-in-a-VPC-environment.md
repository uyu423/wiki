---
title: Things to know when using Elastic Beanstalk in a VPC environment
description: 
published: true
date: 2023-02-17T18:00:22.965Z
tags: aws, elasticbeanstalk, elasticip, english, vpc
editor: markdown
dateCreated: 2022-12-24T20:49:42.720Z
---

- [VPC 환경에서 Elastic Beanstalk 을 사용해야할 때 알아둬야할 것들***Korean** version of this document is available*](/ko/dev/AWS/Things-to-know-when-using-Elastic-Beanstalk-in-a-VPC-environment)
{.links-list}

> Creating a Custom VPC while building a project in AWS
> However, I had trouble connecting to the external Internet while building the ElasticBeanstalk environment in VPC.
> Organized the VPC settings to be checked in relation to it
> (The cases below assume that EC2 is in a public subnet without Load Balancer)
{.is-info}


# ElasticBeanstalk

## Configuration - Network

- instance - assign a public IP address :white_check_mark:


# VPCs

## VPC settings

### DNS Settings

- Enable DNS checking :white_check_mark:
- Enable DNS hostname :white_check_mark:

## Subnet settings

> The configuration below refers to the setting in which all cases communicate only through Internet <-> Public Subnet <-> Private Subnet. {.is-info}

![1_ife_uuqvwijo-oiplrcfba.png](/1_ife_uuqvwijo-oiplrcfba.png =700x){.align-center}

### For Public Subnets

- **Routing Table** (Routing Table)
   - Check if the CIDR of the subnet parent VPC is registered
   - Check if `0.0.0.0/0` is registered as an internet gateway
- **Network ACL** (Network ACL)
   - Make sure all traffic (type) is registered as `0.0.0.0/0` (source) `Allow`
  
#### Add Public Subnet :fire::fire:

> When creating a VPC, even if it is created as a public subnet, the settings below are not set as default values.
> As a result, when a new EC2 instance is created in ElasticBeanstalk, public IP allocation does not occur, causing EC2 to fail to communicate with ElasticBeanstalk.
>
> > **The EC2 instances failed to communicate with AWS Elastic Beanstalk**, either because of configuration problems with the VPC or a failed EC2 instance. Check your VPC configuration and try launching the environment again.{.is-danger}
>
> This issue takes the most time :rage:
> If you check **Auto-assigned IP setting** below, Public IP <small>(Elastic IP)</small> is normally assigned to the instance when EC2 instance is created in ElasticBeanstalk.


- Automatically assigned IP settings
   - Enable automatic assignment of public IPv4 addresses :white_check_mark:

### For Private Subnets

> Private Subnet communicates only with Public Subnet without connecting to the external Internet.
> If NAT is set, private subnet resources can be accessed from the outside if necessary, but this is not set. (NAT is very expensive)
> > If you create a load balancer in a public subnet and EC2 in a private subnet, EC2 can access AWS services by using the endpoint function of the VPC. See [here](https://wiki.yowu.dev/en/dev/AWS/VPC-endpoint-settings-when-running-ElasticBeanstalk-EC2-instances-in-a-private-subnet)
{.is-info}




- **Routing Table** (Routing Table)
   - Check if the CIDR of the subnet parent VPC is registered
   - (If you need access to specific AWS resources such as S3) Check if a VPC endpoint (vpce) is set up
  
> **Maintenance Tricks**
> - If you connect a specific IP to the Internet gateway when setting up the routing table and set a public IP on an instance such as EC2, you can access resources in the private subnet only with the specific IP.
  
- **Network ACL** (Network ACL)
   - Make sure all traffic (type) is registered as `0.0.0.0/0` (source) `Allow`

## Security Group Settings

> Configure them appropriately according to the AWS resources you use. I configured a Security Group for EC2 and RDS only.
> Inbound rules are configured differently depending on the ports used by AWS resources, and all outbound rules are the same, allowing all TCP traffic `0.0.0.0/0`.
{.is-info}

- `ec2-sg` inbound (webserver only)
   - Allow 32 PORT (HTTP) as `0.0.0.0/0`
   - Allow 443 PORT (HTTPS) as `0.0.0.0/0`
- `rds-sg` inbound (database only)
   - Allow `ec2-sg` 3306 PORT (for MySQL/MariaDB)

> **Maintenance Tricks**
> - As in the routing table, you can set to allow all traffic with a subnetmask of 32 only from a specific IP.

---

# References

- [VPC-endpoint-settings-when-running-ElasticBeanstalk-EC2-instances-in-a-private-subnet*WIKI.YOWU.DEV*](/en/dev/AWS/VPC-endpoint-settings-when-running-ElasticBeanstalk-EC2-instances-in-a-private-subnet)
- [Elastic Beanstalk – In a VPC*notes.webutvikling.org*](https://notes.webutvikling.org/elastic-beanstalk-in-a-vpc/)
- [The EC2 instances failed to communicate with AWS Elastic Beanstalk, either because of configuration problems with the VPC or a failed EC2 instance. Check your VPC configuration and try launching the environment again.*reddit.com*](https://www.reddit.com/r/aws/comments/3edgsp/the_ec2_instances_failed_to_communicate_with_aws/)
- [How do I troubleshoot errors that occur when Amazon EC2 instances fail to communicate with Elastic Beanstalk?*AWS Documetation*](https://aws.amazon.com/en/premiumsupport/knowledge-center/elastic-beanstalk-instance-failure/)
- [NAT gateways are too expensive*Reddit*](https://www.reddit.com/r/aws/comments/w3zrwz/nat_gateways_are_too_expensive/)
{.links-list}