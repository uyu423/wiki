---
title: Hypervisor
description: 
published: true
date: 2023-02-17T18:15:51.914Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:57:41.069Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Hypervisor***English** version of this document is available*](/en/Knowledge-base/Dictionary/hypervisor)
{.links-list}


# 개요
**하이퍼바이저**는 물리적 서버에서 가상 머신(VM)을 생성하고 실행하는 소프트웨어 기반 가상화 기술입니다. 여러 운영 체제와 응용 프로그램을 동일한 하드웨어에서 실행할 수 있으므로 가상화된 컴퓨팅 환경을 만들 수 있습니다.

# 역사
가상화 개념은 1960년대와 1970년대 **시분할** 시스템의 개발과 함께 도입되었습니다. 이러한 시스템을 통해 여러 사용자가 동일한 컴퓨팅 리소스에 액세스할 수 있어 리소스를 효율적으로 사용할 수 있습니다. 최초의 상용 하이퍼바이저인 IBM의 DIS/VMS는 1978년에 출시되었습니다.

# 설명
하이퍼바이저는 물리적 하드웨어와 운영 체제 사이에 있는 소프트웨어 계층입니다. 여러 게스트 운영 체제를 동일한 물리적 서버에서 실행할 수 있으므로 가상화된 컴퓨팅 환경을 만들 수 있습니다. 하이퍼바이저는 물리적 서버에 **가상 머신**(VM)을 생성합니다. 각 VM에는 자체 운영 체제, 애플리케이션 및 데이터가 있어 동일한 서버의 다른 VM과 독립적으로 관리할 수 있습니다.

하이퍼바이저는 CPU, 메모리, 스토리지와 같은 물리적 서버의 리소스를 관리하고 VM에 할당합니다. 게스트 운영 체제가 서로 격리되고 물리적 하드웨어에 직접 액세스할 수 있도록 하는 **가상화 계층**도 제공합니다.

가장 일반적인 유형의 하이퍼바이저는 기존 운영 체제 위에서 실행되는 **호스팅된 하이퍼바이저**입니다. VMware ESXi 및 Microsoft Hyper-V를 예로 들 수 있습니다. 다른 유형은 물리적 하드웨어에서 직접 실행되는 **베어메탈 하이퍼바이저**입니다. VMware ESX 및 Microsoft Hyper-V 서버를 예로 들 수 있습니다.

# 관련된 링크들
- [하이퍼바이저란?*VMware*](https://www.vmware.com/resources/compatibility/what-is-a-hypervisor.html)
- [Hypervisor*Microsoft*](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/hypervisor-overview)
- [하이퍼바이저 유형: 종합 가이드*Ravello Systems*](https://ravellosystems.com/hypervisor-types-guide/)
{.links-list}