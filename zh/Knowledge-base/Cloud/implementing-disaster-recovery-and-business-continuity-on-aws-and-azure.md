---
title: 在 AWS 和 Azure 上实施灾难恢复和业务连续性
description: 
published: true
date: 2023-02-01T14:58:18.379Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:58:16.797Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Implementing Disaster Recovery and Business Continuity on AWS and Azure***English** version of this document is available*](/en/Knowledge-base/Cloud/implementing-disaster-recovery-and-business-continuity-on-aws-and-azure)
{.links-list}


  ### 在 AWS 和 Azure 上实施灾难恢复和业务连续性

  在发生灾难时，实施良好的灾难恢复 (DR) 和业务连续性计划 (BCP) 对于保持业务正常运行至关重要。虽然有许多不同的方法来实施 DR 和 BCP，但使用来自 Amazon Web Services (AWS) 和 Microsoft Azure 等提供商的云服务可能是一个不错的选择。

  基于云的 DR 和 BCP 可以提供许多优于传统本地解决方案的优势。例如，可以根据需要快速配置和扩展云服务，这有助于确保您的 DR 和 BCP 解决方案能够满足您的业务需求，即使在发生大规模灾难时也是如此。此外，可以通过互联网连接从任何地方访问云服务，如果您的本地基础设施在灾难中受损或毁坏，这将是一个主要优势。

  但是，在 AWS 和 Azure 上实施 DR 和 BCP 可能是一个挑战。在本文中，我们将概述在这两个云平台上实施 DR 和 BCP 的一些关键注意事项。

  #### AWS 和 Azure 上的灾难恢复注意事项

  在 AWS 或 Azure 上规划 DR 时，需要牢记几个关键注意事项：

  - **可用区：** AWS 和 Azure 都在每个区域提供多个可用区 (AZ)。 AZ 是物理上独立的数据中心，通过低延迟网络连接。在任一平台上规划 DR 时，选择具有多个 AZ 的区域非常重要，这样您的应用程序和数据就可以跨多个数据中心进行复制。

  - **区域：** AWS 和 Azure 都在全球提供多个区域。在为您的 DR 解决方案选择区域时，选择一个在地理上远离您的主要区域的区域很重要。这将有助于确保您的 DR 解决方案不会受到影响您的主要区域的同一灾难的影响。此外，选择满足您的业务合规性和数据主权要求的区域也很重要。

  - **VPC：** AWS 和 Azure 都提供虚拟私有云 (VPC)，可用于将您的应用程序和数据与公共互联网隔离开来。在任一平台上规划 DR 时，请务必在每个区域创建一个 VPC 以用于您的 DR 解决方案。这将有助于确保您的灾难恢复解决方案不会受到影响公共互联网的网络中断或安全漏洞的影响。

  - **网络：** AWS 和 Azure 都提供了多种网络选项，包括 VPN、Direct Connect 和 ExpressRoute。在任一平台上规划 DR 时，选择满足您的性能和可用性要求的网络选项非常重要。

  - **存储：** AWS 和 Azure 都提供了多种存储选项，包括对象存储、块存储和文件存储。在任一平台上规划 DR 时，选择满足您的性能和可用性要求的存储选项非常重要。

  - **数据库：** AWS 和 Azure 都提供了多种数据库选项，包括关系数据库、NoSQL 数据库和内存数据库。在任一平台上规划 DR 时，选择满足您的性能和可用性要求的数据库选项非常重要。

  - **安全性：** AWS 和 Azure 都提供了多种安全选项，包括防火墙、入侵检测和预防以及数据加密。在任一平台上规划 DR 时，选择满足您的合规性和数据主权要求的安全选项非常重要。

  - **成本：** AWS 和 Azure 都提供多种定价选项，包括即用即付、预留实例和承诺使用折扣。在任一平台上规划 DR 时，选择满足您的预算和业务要求的定价选项非常重要。

  #### AWS 上的灾难恢复

  Amazon Web Services (AWS) 提供多种服务，可用于实施灾难恢复 (DR) 和业务连续性 (BCP) 解决方案。在本节中，我们将概述一些可用于 DR 和 BCP 的关键 AWS 服务。

  - **AWS CloudFormation：** AWS CloudFormation 是一项允许您使用模板创建和管理 AWS 资源的服务。 CloudFormation 模板可用于为您的灾难恢复解决方案预置和配置 AWS 资源。

  - **AWS Elastic Beanstalk：** AWS Elastic Beanstalk 是一项允许您在 AWS 上部署和管理 Web 应用程序的服务。 Elastic Beanstalk 可用于为您的 DR 解决方案部署和管理 Web 应用程序。

  - **AWS Lambda：** AWS Lambda 是一项服务，让您无需预置或管理服务器即可运行代码。 Lambda 可用于为您的 DR 解决方案运行代码。

  - **AWS OpsWorks：** AWS OpsWorks 是一项服务，可让您自动部署和管理 AWS 资源。 OpsWorks 可用于为您的灾难恢复解决方案自动部署和管理 AWS 资源。

  - **AWS Storage Gateway：** AWS Storage Gateway 是一项允许您将本地存储系统连接到 AWS 的服务。 Storage Gateway 可用于将本地存储系统连接到 AWS，以用于您的 DR 解决方案。

  - **AWS CloudTrail：** AWS CloudTrail 是一项允许您监控 AWS API 调用的服务。 CloudTrail 可用于监控 DR 解决方案的 AWS API 调用。

  - **AWS Config：** AWS Config 是一项允许您跟踪 AWS 资源更改的服务。 Config 可用于跟踪 DR 解决方案对 AWS 资源的更改。

  - **AWS CloudWatch：** AWS CloudWatch 是一项允许您监控 AWS 资源的服务。 CloudWatch 可用于监控灾难恢复解决方案的 AWS 资源。

  - **AWS Trusted Advisor：** AWS Trusted Advisor 是一项提供有关如何优化 AWS 资源的建议的服务。 Trusted Advisor 可用于提供有关如何优化 DR 解决方案的建议。

  - **AWS 服务目录：** AWS 服务目录是一项允许您管理 AWS 资源的服务。 Service Catalog 可用于为您的 DR 解决方案管理 AWS 资源。

  - **AWS Identity and Access Management：** AWS Identity and Access Management (IAM) 是一项允许您管理用户和权限的服务。 IAM 可用于管理 DR 解决方案的用户和权限。

  - **AWS Key Management Service：** AWS Key Management Service (KMS) 是一项允许您管理加密密钥的服务。 KMS 可用于管理 DR 解决方案的加密密钥。

  - **AWS CloudHSM：** AWS CloudHSM 是一项允许您管理硬件安全模块的服务。 CloudHSM 可用于管理 DR 解决方案的硬件安全模块。

  - **AWS Directory Service：** AWS Directory Service 是一项允许您管理 Active Directory 的服务。目录服务可用于管理 DR 解决方案的 Active Directory。

  - **AWS Certificate Manager：** AWS Certificate Manager 是一项允许您管理 SSL/TLS 证书的服务。 Certificate Manager 可用于管理 DR 解决方案的 SSL/TLS 证书。

  - **AWS WAF：** AWS WAF 是一项允许您管理 Web 应用程序防火墙的服务。 WAF 可用于管理 DR 解决方案的 Web 应用程序防火墙。

  - **AWS Shield：** AWS Shield 是一项可让您保护应用程序免受 DDoS 攻击的服务。 Shield 可用于保护您的应用程序免受 DR 解决方案的 DDoS 攻击。

  - **AWS Inspector：** AWS Inspector 是一项允许您评估 AWS 资源安全性的服务。 Inspector 可用于评估灾难恢复解决方案的 AWS 资源的安全性。

  - **AWS Artifact：** AWS Artifact 是一项允许您管理合规性文档的服务。 Artifact 可用于管理 DR 解决方案的合规性文档。

  #### Azure 上的灾难恢复

  Microsoft Azure 提供了多种服务，可用于实施灾难恢复 (DR) 和业务连续性 (BCP) 解决方案。在本节中，我们将概述一些可用于 DR 和 BCP 的关键 Azure 服务。

  - **Azure Site Recovery：** Azure Site Recovery 是一项允许您复制和恢复 Azure VM 的服务。 Site Recovery 可用于为 DR 解决方案复制和恢复 Azure VM。

  - **Azure 备份：** Azure 备份是一项允许您备份和还原 Azure VM 的服务。备份可用于为您的 DR 解决方案备份和还原 Azure VM。

  - **Azure 存储：** Azure 存储是一项允许您在云中存储和访问数据的服务。存储可用于存储 DR 解决方案的数据。

  - **Azure SQL 数据库：** Azure SQL 数据库是一项允许您在云中运行关系数据库的服务。 SQL 数据库可用于为 DR 解决方案运行关系数据库。

  - **Azure Cosmos DB：** Azure Cosmos DB 是一项允许您在云中运行 NoSQL 数据库的服务。 Cosmos DB 可用于为您的 DR 解决方案运行 NoSQL 数据库。

  - **Azure Table Storage：** Azure Table Storage 是一项允许您将数据存储在云中的服务。表存储可用于存储 DR 解决方案的数据。

  - **Azure Blob Storage：** Azure Blob Storage 是一项允许您将数据存储在云中的服务。 Blob 存储可用于存储 DR 解决方案的数据。

  - **Azure 文件存储：** Azure 文件存储是一项允许您将数据存储在云中的服务。文件存储可用于存储 DR 解决方案的数据。

  - **Azure 虚拟网络：** Azure 虚拟网络是一项允许您创建和管理虚拟网络的服务。虚拟网络可用于为您的 DR 解决方案创建和管理虚拟网络。

  - **Azure Load Balancer：** Azure Load Balancer 是一项允许您在多个 VM 之间分配流量的服务。负载均衡器可用于为您的 DR 解决方案在多个 VM 之间分配流量。

  - **Azure Traffic Manager：** Azure Traffic Manager 是一种服务，可让您将流量路由到不同的 Azure 资源。流量管理器可用于将流量路由到 DR 解决方案的不同 Azure 资源。

  - **Azure DNS：** Azure DNS 是一项允许您管理 DNS 记录的服务。 DNS 可用于管理 DR 解决方案的 DNS 记录。

  - **Azure Active Directory：** Azure Active Directory 是一项允许您管理用户和权限的服务。 Active Directory 可用于管理 DR 解决方案的用户和权限。

  - **Azure Key Vault：** Azure Key Vault 是一项允许您管理加密密钥的服务。 Key Vault 可用于管理 DR 解决方案的加密密钥。

  - **Azure 信息保护：** Azure 信息保护是一项允许您保护数据的服务。信息保护可用于保护 DR 解决方案的数据。

  - **Azure 安全中心：** Azure 安全中心是一项服务，可让您监控和管理 Azure 资源的安全性。安全中心可用于监控和管理灾难恢复解决方案的 Azure 资源的安全性。

  - **Azure Monitor：** Azure Monitor 是一项允许您监视 Azure 资源的服务。 Monitor 可用于监控 DR 解决方案的 Azure 资源。

  - **Azure Policy：** Azure Policy 是一项允许您管理和执行合规性策略的服务。策略可用于管理和执行 DR 解决方案的合规性策略。

  - **Azure Blueprints：** Azure Blueprints 是一项允许您创建和管理 Azure 资源的服务。蓝图可用于为您的 DR 解决方案创建和管理 Azure 资源。

  - **Azure 资源管理器：** Azure 资源管理器是一项允许您管理 Azure 资源的服务。 Resource Manager 可用于管理 DR 解决方案的 Azure 资源。

  ### 结论

  实施灾难恢复 (DR) 和业务连续性 (BCP) 可能是一项挑战。但是，使用来自 Amazon Web Services (AWS) 和 Microsoft Azure 等提供商的云服务可能是一个不错的选择。在本文中，我们概述了在 AWS 和 Azure 上实施 DR 和 BCP 的一些关键注意事项。