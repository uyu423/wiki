---
title: AWS Elastic IPs: Allocating Static IP Addresses for Cloud Resources
description: 
published: true
date: 2023-02-06T19:17:42.147Z
tags: 
editor: markdown
dateCreated: 2023-02-06T19:17:36.386Z
---

- [IP elásticas de AWS: asignación de direcciones IP estáticas para recursos en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-elastic-ips-allocating-static-ip-addresses-for-cloud-resources)
{.links-list}
- [AWS 弹性 IP：为云资源分配静态 IP 地址***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-elastic-ips-allocating-static-ip-addresses-for-cloud-resources)
{.links-list}
- [AWS 탄력적 IP: 클라우드 리소스에 고정 IP 주소 할당***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-elastic-ips-allocating-static-ip-addresses-for-cloud-resources)
{.links-list}


# AWS Elastic IPs: Allocating Static IP Addresses for Cloud Resources

Elastic IP addresses are static IP addresses designed for dynamic cloud computing. An elastic IP address is associated with your AWS account. With an elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.

An elastic IP address is a public IP address that you can allocate to an instance or a network interface. If you associate an elastic IP address with an instance that already has a public IP address, the instance's original public IP address is replaced with the elastic IP address. If you associate an elastic IP address with a network interface, the IP address is associated with the primary private IP address of the network interface.

You can allocate a new elastic IP address while creating an instance using the Amazon EC2 console. You can also allocate a new elastic IP address from your existing pool of elastic IP addresses. You can associate an elastic IP address with an instance or a network interface at any time.

If you disassociate an elastic IP address from an instance, the instance is assigned a new public IP address from the Amazon EC2 pool of public IP addresses. If you disassociate an elastic IP address from a network interface, the primary private IP address of the network interface is reassigned from the elastic IP address to another private IP address from the IP address pool of the subnet.

## Allocating an Elastic IP Address

To allocate an elastic IP address using the Amazon EC2 console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. In the navigation pane, choose **Elastic IPs**.

3. Choose **Allocate new address**.

4. Choose **Allocate**.

5. Choose **Close**.

Your elastic IP address is now allocated and ready to be associated with an instance or network interface.

## Associating an Elastic IP Address with an Instance

To associate an elastic IP address with an instance using the Amazon EC2 console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. From the instances list, select the instance.

3. Choose **Actions**, **Networking**, **Change Elastic IP Address**, **Associate Elastic IP Address**.

4. Select the elastic IP address from the list, and then choose **Associate**.

Your instance is now associated with the elastic IP address.

## Associating an Elastic IP Address with a Network Interface

To associate an elastic IP address with a network interface using the Amazon EC2 console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. In the navigation pane, choose **Network Interfaces**.

3. Select the network interface, and then choose **Action**, **Networking**, **Change Elastic IP Address**, **Associate Elastic IP Address**.

4. Select the elastic IP address from the list, and then choose **Associate**.

Your network interface is now associated with the elastic IP address.

## Disassociating an Elastic IP Address

To disassociate an elastic IP address from an instance or network interface using the Amazon EC2 console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. In the navigation pane, choose **Elastic IPs**.

3. Select the check box next to the elastic IP address that you want to disassociate.

4. Choose **Actions**, **Networking**, **Change Elastic IP Address**, **Disassociate Elastic IP Address**.

5. When prompted for confirmation, choose **Yes, Disassociate**.

The elastic IP address is now disassociated from the instance or network interface.

## Releasing an Elastic IP Address

You can release an elastic IP address when you no longer need it. To release an elastic IP address using the Amazon EC2 console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. In the navigation pane, choose **Elastic IPs**.

3. Select the check box next to the elastic IP address that you want to release.

4. Choose **Actions**, **Networking**, **Change Elastic IP Address**, **Release Elastic IP Address**.

5. When prompted for confirmation, choose **Yes, Release**.

The elastic IP address is now released and no longer associated with your AWS account.

## Additional Information

For more information about elastic IP addresses, see the following:

- Elastic IP Addresses in the Amazon EC2 User Guide for Linux Instances
- Elastic IP Addresses in the Amazon EC2 User Guide for Windows Instances

## External Resources

- Amazon EC2: Elastic IP Addresses (EIPs)
- AWS IP Address Planning
- How To Use AWS Elastic IPs